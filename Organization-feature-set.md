# Am I using AWS Organizations?

**If you have multiple AWS Accounts and are currently paying your AWS Invoice for all those accounts via one account, you are currently using Organizations.**

**If you have multiple AWS Accounts and are currently paying your AWS Invoice(s) via mulitple accounts, you may have a combination of accounts with and without Organizations. Please reach out to your DoiT contact to setup a review.**

**If you have only one AWS Account, follow these steps in that account.**

After logging in as root user, load this [page](https://us-east-1.console.aws.amazon.com/organizations/v2/home?region=us-east-1#)


If it shows a page like this, you are currently not using Organizations

![org](/images/no-org.png)    
<br/><br/>

If it shows a page similar to following, you are using Organizations.

![org](/images/org-one-account.png)    
<br/><br/><br/><br/>

# What Organization-level features are you using in AWS?

After logging into the [payer/management account](Payer-And-Member-Accounts.md), load this [page](https://us-east-1.console.aws.amazon.com/organizations/v2/home/settings). You will see something like the following.

![org](/images/org.png)    
<br/><br/>

Under Feature Set, it will display one of the following

a) Consolidated Features Only   
*This means you are not using any Organization-level features. You can skip next step if this is the case.*
   
b) Your organization has all features enabled   
*This means you could be potentially using some Organziation-level features. Follow next step to find which services are being used*

<br/><br/>
If it shows the following page, you are not currently in the payer account   
<br/>
![nopayer](/images/nopayer.png)    
<br/><br/><br/><br/>

If your Organization has all features enabled, navigate to this [page](https://us-east-1.console.aws.amazon.com/organizations/v2/home/services).
<br/><br/>
![service](/images/services.png)

Scroll through the page and take a note of features that has "Access enabled".
