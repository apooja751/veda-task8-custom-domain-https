# VEDA Technology Cloud Computing Internship — Task 8

## Custom Domain and HTTPS for a Cloud-Hosted Application

This project was completed as part of the Cloud Computing Internship at VEDA Technology.

The objective of this task was to deploy a cloud-hosted web application, connect it to a custom domain using DNS, secure it using an AWS Certificate Manager (ACM) SSL/TLS certificate, and configure HTTP to HTTPS redirection.

---

## 📌 Task Objective

Point a custom domain to a cloud-hosted application and secure the application using HTTPS.

### Objectives

- Configure a cloud-hosted web application.
- Configure DNS for a custom domain.
- Configure an SSL/TLS certificate.
- Enable HTTPS using AWS Certificate Manager.
- Configure HTTP to HTTPS redirection.
- Understand automatic certificate renewal.
- Verify the application through the custom HTTPS domain.

---

## ☁️ AWS Services and Technologies Used

- Amazon EC2
- Amazon Linux 2023
- Nginx
- Application Load Balancer (ALB)
- Elastic Load Balancing Target Group
- AWS Certificate Manager (ACM)
- DNS management using isroot.in
- HTTPS / TLS
- GitHub

---

## 🏗️ Architecture

```text
                         Internet
                             │
                             │
                  https://www.veda-task8.isroot.in
                             │
                             ▼
                    DNS CNAME Record
                             │
                             ▼
              ┌──────────────────────────┐
              │  Application Load        │
              │  Balancer                │
              │  veda-task8-alb          │
              └──────────────────────────┘
                    │              │
             HTTP :80          HTTPS :443
                    │              │
                    │         ACM Certificate
                    │              │
                    └──────┬───────┘
                           ▼
                  Target Group
                 veda-task8-tg
                           │
                           ▼
                  Amazon EC2 Instance
                   veda-task8-web
                           │
                           ▼
                         Nginx
                           │
                           ▼
                    Web Application

```
## Application Details
**Custom Domain** www.veda-task8.isroot.in
**Application URL** https://www.veda-task8.isroot.in
**Load Balancer** veda-task8-alb
**Target Group** veda-task8-tg
**EC2 Instance** veda-task8-web
**Web Server** Nginx

## Implementation
**1. EC2 Instance**
An Amazon EC2 instance was created using Amazon Linux 2023.

 **Configuration:**
- Instance name: veda-task8-web
- Instance type: t3.micro
- Region: Asia Pacific (Mumbai)
- Web server: Nginx
  
**Nginx was installed and started using:**
sudo dnf install nginx -y
sudo systemctl enable --now nginx

**2. Application Deployment**
A custom HTML page was deployed to the Nginx web root:
/usr/share/nginx/html/

The application displays the VEDA Technology Cloud Computing Internship Task 8 page.

**3. Target Group**
An Application Load Balancer target group was created.
- Target Group: veda-task8-tg
- Protocol: HTTP
- Port: 80
- Health Check Path: /
The EC2 instance was registered with the target group and verified as healthy.

**4. Application Load Balancer**
An internet-facing Application Load Balancer was created.
- Name: veda-task8-alb
- Type: Application
- Scheme: Internet-facing
- IP Address Type: IPv4
The load balancer forwards traffic to the EC2 target group.

**5. DNS Configuration**
The free subdomain was created using isroot.in:
veda-task8.isroot.in

A CNAME record was configured for:
www.veda-task8.isroot.in

The CNAME points to the Application Load Balancer:
veda-task8-alb-1918391427.ap-south-1.elb.amazonaws.com

**6. SSL/TLS Certificate**
AWS Certificate Manager (ACM) was used to request a public SSL/TLS certificate.
Certificate domain:
www.veda-task8.isroot.in

Validation method:
DNS validation

Key algorithm:
RSA 2048

The ACM DNS validation record was added to the domain DNS configuration.
The certificate was then issued successfully.

**7. HTTPS Listener**
An HTTPS listener was configured on the Application Load Balancer.
Protocol: HTTPS
Port: 443

The ACM certificate for:
www.veda-task8.isroot.in

was attached to the HTTPS listener.
HTTPS traffic is forwarded to:
veda-task8-tg

**8. HTTP to HTTPS Redirect**
The HTTP listener on port 80 was configured to redirect HTTP traffic to HTTPS.
HTTP :80
     |
     v
HTTPS :443

**The redirect uses HTTP status code:** 301 - Permanently Moved

## Security Configuration
The Application Load Balancer security group allows:
| Protocol | Port |   Source  |
|----------|-----:|-----------|
| HTTP     | 80   | 0.0.0.0/0 |
| HTTPS    | 443  | 0.0.0.0/0 |
The EC2 security group allows HTTP traffic from the Application Load Balancer.

## Certificate Renewal
The SSL/TLS certificate is managed by AWS Certificate Manager.
The certificate uses DNS validation.
The ACM validation CNAME record should remain in the DNS configuration so that ACM can continue to validate the domain for automatic renewal.
If certificate renewal fails and the certificate expires, HTTPS connections can show certificate errors and secure access may become unavailable.

## Rollback
If the HTTPS configuration needs to be rolled back:
1. Open the Application Load Balancer.
2. Open Listeners and rules.
3. Select the HTTP:80 listener.
4. Edit the default action.
5. Change the action from HTTPS redirect back to forwarding.
6. Forward traffic to veda-task8-tg.
7. Save the changes.
   
## Verification
**The following checks were performed:**
- EC2 instance was running.
- Nginx web server was active.
- Target group health check was successful.
- Application Load Balancer was active.
- DNS CNAME was configured.
- ACM certificate was issued.
- HTTPS listener was configured on port 443.
- HTTP traffic was redirected to HTTPS using status code 301.
- The application was successfully accessed using the custom HTTPS domain.
**Final Application URL**
https://www.veda-task8.isroot.in

## Screenshots
The repository contains screenshots showing:
1. Free subdomain
2. EC2 instance
3. Nginx
4. Target group
5. Application Load Balancer
6. Target health
7. ALB HTTP application
8. DNS records
9. DNS CNAME
10. ACM pending validation
11. ACM validation DNS record
12. ACM certificate issued
13. ALB HTTPS listener
14. HTTP to HTTPS redirect
15. Final HTTPS application

## Conclusion
Task 8 was successfully completed by connecting a custom domain to a cloud-hosted application using DNS and securing the application with an AWS Certificate Manager SSL/TLS certificate. HTTPS was configured through the Application Load Balancer, and HTTP traffic was automatically redirected to HTTPS using a 301 redirect.
This task provided practical understanding of DNS configuration, TLS certificate management, HTTPS security, load balancing, and automatic certificate renewal in a cloud environment.

## Task Outcome
The cloud-hosted application was successfully connected to a custom domain and secured using an AWS-managed SSL/TLS certificate.

**The final application is accessible through:**
https://www.veda-task8.isroot.in

HTTP requests are redirected to HTTPS using a 301 redirect.
