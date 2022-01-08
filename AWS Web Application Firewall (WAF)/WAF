# Highly Configurable and Scalable, Cloud Native web application Layer-7 firewall giving you the first line of defense.

There are ***many security threats*** that exist today in a typical enterprise distributed application.
    
1.	**DDoS:** Flood Attacks (SYN Floods, UDP Floods, ICMP Floods, HTTP Floods, DNS Query Floods), Reflection Attacks
2.	**Application Vulnerabilities:** SQL Injections, Cross Site Scripting (XSS), Open Web Application Security Project (OWASP), Common Vulnerabilities and Exposures (CVE)
3.	**Bad Bots:** Crawlers, Content Scrapers, Scanners and Probes

Out of these, AWS WAF can be used to handle security threats such as SQL injections, Cross Site Scripting (XSS) in a typical web application.

The web application HTTP requests can be routed via AWS WAF and then will be forwarded to either one of the AWS services.
1.	AWS CloudFront (A Global Service)
2.	AWS API Gateway (A Regional Service)
3.	AWS Application Load Balancer (A Regional Service)

Logging and Monitoring of WAF are handled by Kinesis Firehose and CloudWatch respectively.
![image](https://user-images.githubusercontent.com/77272124/148635611-608e7c5f-dad8-4ff9-8a58-81cbb244db22.png)
***WAF Filtering and Monitoring HTTP requests***
## Web ACL
When WAF associating any of the above three AWS services, it associates with a Web ACL. A Web ACL is a fundamental component of WAF, which defines a set of rules for any of these services
![image](https://user-images.githubusercontent.com/77272124/148635634-a3cffa8d-c798-4fb1-b5f0-924d2f841052.png)
As mentioned, a Web ACL is a collection of rules. A rule is a collection of conditions
![image](https://user-images.githubusercontent.com/77272124/148635646-230ce9ea-9ae2-48b2-9cd1-2ee0edbb847d.png)

## How to create a Web ACL in WAF?
In order to demonstrate the WAF capability, it is always good to go through a simple scenario that can showcase its capability. Here, I am going to block a CloudFront distribution, which I created sometime ago. So, if you are trying this out, please make sure you have one of the services (CloudFront, API Gateway or ALB) is created already before trying this out.

## Task 1: Describe a Web ACL and associate it to AWS resources
Go to AWS WAF → Web ACLs → **Click Create Web ACL button**
![image](https://user-images.githubusercontent.com/77272124/148635661-497d741e-ec02-4bd8-b077-ebc2497fd13c.png)

Give a name to Web ACL and associate a Resource Type to it. Here we are associate a CloudFront distribution, which I have already created before. You can attach this to not only CloudFront but ALB and APIGateway as well.

If you select a CloudFront, then you need to select “Global” as the scope since it is a Global service. If you select either ALB ot API Gateway, you will have to select a region where the associate resource is located.

![image](https://user-images.githubusercontent.com/77272124/148635676-6c5f96fd-a9e9-4f3d-ac65-292f562d9f46.png)
Click Add AWS Resources button to associate the CloudFront Distribution that you created before
![image](https://user-images.githubusercontent.com/77272124/148635688-3cc4a889-6742-407b-8e54-6ced931f02dd.png)
Click Next button and you will get another page to add your rules to Web ACL. We will skip this for the moment allowing us to do it at a later stage.
Select Allow for Web ACL Action as well.
(Web ACL Action defines what you are going to do when the defined rule is active)
Leave Set Rule Priority as it is and click Next.
Leave Configure Metrics and click Next.
Finally review your selections and click Create Web ACL button.
The above will create a Web ACL without any rules. You can go back to Web ACL link and you will see the below. Make sure not to select a region and select Global (CloudFront) in the top drop down to see your created Web ACL 
![image](https://user-images.githubusercontent.com/77272124/148635693-e74a6af6-dce0-4b11-9b31-70660f724d65.png)

However, even if you see a created Web ACL, CloudFront propagation for this update will take a bit of time. You can see it if you visit the CloudFront console page. Give a little bit of time finish the CloudFront propagation before you start the next step.

## Task 2: Add a Condition to block my IP address
Go to AWS WAF → IP Sets → Click Create IP Set button.
Select IPV4 and give your IP address with /32 as the postfix. If you are not sure how to get your network’s public IP, you may type “What is my IP” on Google. It is that simple.
![image](https://user-images.githubusercontent.com/77272124/148635706-495c9e20-f933-4664-bbc2-d027728482d9.png)

## Task 3: Add a Rule to the created condition
In order to create a rule, you need to create a Rule Group.
Go to AWS WAF → Rule Group → Click Create Rule Groups button
![image](https://user-images.githubusercontent.com/77272124/148635714-c54fab05-0bdb-41f3-85c7-64f4dba6408c.png)
Click Next → Click Add Rule button →Set the following parameters to create a Rule
Rule Name → MyRule
If a Request → Select Matches the requirement
Statement (Inspect)→ Select Originates from an IP Address In
Statement (IP Set) → Select the IP Set that you created in Task 2
Action → Select Block
Click Next
Select the Rule Priority. This is not required here since you have only one rule.
Finally review your selections and click Create Rule Group to confirm your rule settings.

## Task 4: Add the created Rule Group / Rule to the Web ACL
Go to AWS WAF → Web ACL → Select the Web ACL that you have created → Click Rules tab (See Figure 10).
![image](https://user-images.githubusercontent.com/77272124/148635723-9fd524d8-a7c4-4ad8-8d49-5ae58304a164.png)

You can see the Web ACL still does not have its rules attached.
Click Add Rules button drop down → Select Add my own rules and rule groups
![image](https://user-images.githubusercontent.com/77272124/148635726-72450efe-7622-4a45-94f1-3da93ea812dc.png)
Give a name for the rule that you are specifying here 
Select the Rules Group that you created from the drop down and click Add rule button and then click Save.
Now we can see the added rule is attached to the Web ACL.
Now it is time to browse the web URL that you have blocked for 

your IP. If all fine, it will be similar to below screen 
![image](https://user-images.githubusercontent.com/77272124/148635735-ea328147-7dee-4ae1-911a-63e48ab4004c.png)

*If you want to remove the blocking, you can go to the Web ACL and delete the related Rule and try the web link again. After a few refresh attempts, you will get your site back.*


