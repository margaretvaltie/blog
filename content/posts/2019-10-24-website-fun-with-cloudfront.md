---
title: Website fun with CloudFront
author: mvaltie
date: 2019-10-24T11:57:06+00:00
url: /2019/10/24/website-fun-with-cloudfront/
categories:
  - Chicago

---
I, like most people, have more domains than websites. I get more brilliant ideas for website and projects than I have index.html files to actually build those websites.

For a good static site, there should be S3 based resources plus some fancy footwork to make sure the site displays well and is secure. I had the S3 buckets set up for ChicagoAWS.com but just didn't get around to setting up the right networking and SSL cert. A conversation with Eric Hamacher at <a href="https://midwestcommunityday.com/become-a-sponsor/" target="_blank" rel="noopener noreferrer">AWS Community Day Midwest</a> reminded me to get on it!

For ChicagoAWS.com I had the S3 based static site set up, or steps 1 and 2 in the <a href="https://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html" target="_blank" rel="noopener noreferrer">AWS guide online.</a>

<img class="alignnone size-medium wp-image-2302" src="http://blog.margaretmvaltierra.com/wp-content/uploads/2019/10/S3_website_contents-300x117.png" alt="" width="300" height="117" />  
The part I was missing was a CloudFront distribution and an SSL cert to give the website https instead of http. I'd struggled with that part in the AWS guide and just gave up. Thanks to some pointers from Eric, I added SSL for all my websites. Here's how.

I use AWS as a Domain Registar, or the Route53 service. When I setup my domains in Route 53 I created Hosted Zones already, and they come with 2 record sets: SOA and NS. Here's how my little S3 website looked in Route53:

<img class="alignnone size-medium wp-image-2300" src="http://blog.margaretmvaltierra.com/wp-content/uploads/2019/10/hosted_zone_step1-300x111.png" alt="AWS  Registar Route 53" width="300" height="111" /> 

**Certificate Manager**

To use SSL to get that HTTPS, I had to create the DNS-validated certificate in [AWS Certificate Manager][1]. For some ACM voodoo, your certs must be in US-East-1 (N. Virginia) to work for static websites. All I know is it doesn't work if you don't use us-east-1.  Here I provision a public certificate and click “Request a Certificate.” Depending on your use case, wildcards and multiple domains for 1 cert might cause headaches later but I want to jam in all the possible domains for this cert. You cannot edit ACM certs after creation. I added the main domain name (chicagoaws.com) as well as [*].chicagoaws.com in case I want to use the certificate with any potential subdomain. 

<img class="alignnone size-medium wp-image-2296" src="http://blog.margaretmvaltierra.com/wp-content/uploads/2019/10/cert_request-300x131.png" alt="AWS ACM certificate request" width="300" height="131" /> 

Now I have to validate the domains. For each domain, there's a big blue button "Create Record in Route 53" that makes a CNAME record in Route 53. Give it a few minutes to update. 

**CloudFront** 

While the cert is updating, I can set up a CloudFront distribution. I chose a new Web distro. For the Origin the S3 bucket should pop up: chicagoaws.com.s3.amazonaws.com. Keep other settings the same, scroll down and select "Redirect HTTP to HTTPS"

<img class="alignnone size-medium wp-image-2298" src="http://blog.margaretmvaltierra.com/wp-content/uploads/2019/10/CF_create_distro3-300x120.png" alt="" width="300" height="120" /> 

Scroll down a bit more to add all those domain names in the text box "Alternate Domain Names (CNAMEs)". Below that is the radio button to add that fancy new ACM cert. Select "Custom SSL Certificate" and the cert should pop into the space: 

<img class="alignnone size-medium wp-image-2301" src="http://blog.margaretmvaltierra.com/wp-content/uploads/2019/10/route53_Anames-300x147.png" alt="CloudFront Domain as A record alias" width="300" height="147" /> 

Route 53 will take another few minutes to update. After lunch I came back and found Chicagoaws.com has a nice little lock icon in Chrome and www. and chicagoaws.com resolve to https now. Excellent!

**Pro tips:** make sure your ACM certificate is in us-east-1 no matter where S3 buckets live. After creating the CloudFront distro, remember to update Route 53 to remove CNAMEs and add in the A name records. 

## Bonus reading

  * [DNS cheatsheet][2] from Chris Achard
  * Mike Malone: [If you’re not using SSH certificates you’re doing SSH wrong][3]
  * so many great visuals, including a [Zine on Networking][4], from [@b0rk][5] 
  * If you’re not using SSH certificates you’re doing SSH wrong from Mike at [SmallStep][3]
  * [][4]

 [1]: https://aws.amazon.com/certificate-manager/
 [2]: https://chrisachard.com/cheatsheets/dns-cheatsheet.pdf
 [3]: https://smallstep.com/blog/use-ssh-certificates/
 [4]: https://wizardzines.com/zines/networking/
 [5]: https://twitter.com/b0rk