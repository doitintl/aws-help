
# How do I automatically move new Flexsave accounts to a Organization Unit (OU) of my choice?


After you have manually moved DoiT Flexsave accounts to a OU of your choice, you can use the following Lambda function to make the move auotmatic for new accounts.

# Install the following Lambda function in your Payer Account

- Fill in the ORG_ROOT and DESTINATION_OU or set them as environment variables and set with os.environ['ORG_ROOT'] and os.environ['DESTINATION_OU'] 


        import boto3

        ORG_ROOT = "XXX"
        DESTINATION_OU = "XXX"


        def handle_flexsave(event, context):
            details = event["detail"]

            if details["eventName"] == "AcceptHandshake":
                if "responseElements" in details and "handshake" in details["responseElements"]:
                    handshake = details["responseElements"]["handshake"]
                    if handshake["action"] == "INVITE" and handshake["state"] == "ACCEPTED":
                        account_id = next(
                            (
                                resource["value"]
                                for resource in handshake["resources"]
                                if resource["type"] == "ACCOUNT"
                            ),
                            None,
                        )
                        if account_id:
                            handle_account(account_id)
                            return
                        print(f"can't find account in payload")
                        return
            print("Not a relevant event")


        def handle_account(account_id):
            print(f"Processing event for account {account_id}")
            org_client = boto3.client("organizations")

            response = org_client.describe_account(AccountId=account_id)
            account_name = response["Account"]["Name"]

            if account_name.startswith("fs"):
                org_client.move_account(
                    AccountId=account_id,
                    SourceParentId=ORG_ROOT,
                    DestinationParentId=DESTINATION_OU,
                )
            else:
                print(f"Account {account_name} not associated with Flexsave")

# Following Permissions are required for this Lambda

- Lambda will require a role with the following Policy Document
- Replace ARNs with ARNs of the Lambda installled above

        {
        "Version": "2012-10-17",
        "Statement": [
            {
            "Sid": "LogOperations",
            "Effect": "Allow",
            "Action": ["logs:PutLogEvents", "logs:CreateLogStream", "logs:CreateLogGroup"],
            "Resource": [
                "arn:aws:logs:us-east-1:XXX:log-group:/aws/lambda/flexsave-move:*:*",
                "arn:aws:logs:us-east-1:XXX:log-group:/aws/lambda/flexsave-move:*"
            ]
            },
            {
            "Sid": "FlexsaveManagement",
            "Effect": "Allow",
            "Action": ["organizations:DescribeAccount", "organizations:MoveAccount"],
            "Resource": "*"
            }
        ]
        }

# Add an Eventbridge trigger
We assume you already have a CloudTrail Trail configured for management events, which means you simply need to add Eventbridge trigger with following filter, and point to your Lambda

        {
        "source": ["aws.organizations"],
        "detail-type": ["AWS API Call via CloudTrail"],
        "detail": {
            "eventSource": ["organizations.amazonaws.com"],
            "eventName": ["AcceptHandshake"]
        }
        }