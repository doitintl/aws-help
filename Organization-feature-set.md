# What Organization-level features are you using in AWS?

You may have one or multiple AWS accounts.

 - If you have mulitple AWS accounts, perform following actions in the [payer/management account](Payer-And-Member-Accounts.md). 
 - If you have multiple payer/management accounts, preform these actions in all payer/management accounts. 
 - If you do not have access to your payer/management account or it belongs to a different business entity or company, let your DoIT contact know.

<br/><br/>

After logging into AWS Console, load this [page](https://us-east-1.console.aws.amazon.com/organizations/v2/home/settings). You will see something like following.

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
