# AWS-DNS-Management-for-Elastic-BeanStalk

### In my last article I showed 2 CI/CD pipelines one with AWS CodeStar and another with AWS Elastic BeanStalk and AWS CodePipeline.

### You can have a look on this for in detailed, step by step process to follow.



### :point_right: [CI/CD for PHP Projects with AWS](https://github.com/imranxpress/aws-ci-cd-laravel-project)

As Elastic BeanStalk gives us an application environment endpoint to see the output. And it doesn't give you any Name Server links to connect it with any other Domains within AWS or with other third party DNS services like Godaddy.

This seems to be a problem from Elastic BeanStalk and when I tried to connect my Domain with the Elastic BeanStalk application endpoint, it just don't get connected with my main domain but as a sud-domain I could configure it as a CNAME for my Domain in the DNS configuration.

![awsdns02](https://user-images.githubusercontent.com/47071968/184660281-d3e5c994-b95f-4110-be8f-e901382facd8.png)

With this configuration, now Elastic Beanstalk Application will get redirected to test.imran.com subdomain but what if I need to redirect it to imran.com directly!

Elastic BeanStalk doesn't support root domain redirection, we need to find a way around to do so.


Here is my solution for this problem. We will configure the Sub-domain as www.imran.com and so that Elastic BeanStalk can get redirected to this particular sub-domain. 


Now as per client requirement, we need to get it working for the root domain only. So for that we will write this part of code in serverside .htaccess file:

Add the following lines at the beginning of your website’s .htaccess file:

~~~
RewriteEngine On

RewriteCond %{HTTP_HOST} ^www.yourdomain.com [NC]


RewriteRule ^(.*)$ http://yourdomain.com/$1 [L,R=301]

~~~

Replace yourdomain.com with your actual domain name.

This will redirect your root domain to sub-domain to get the actual result form the Elastic BeanStalk application end point.

### Hope this way around helps you guys, if you face similar issue on DNS configuration for Elastic BeanStalk application endpoint.


