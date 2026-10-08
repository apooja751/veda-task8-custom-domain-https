# AWS Configuration

## Region

Asia Pacific (Mumbai) — ap-south-1

## EC2

- Name: `veda-task8-web`
- OS: Amazon Linux 2023
- Instance Type: `t3.micro`
- Web Server: Nginx

## Target Group

- Name: `veda-task8-tg`
- Protocol: HTTP
- Port: 80
- Health Check Path: `/`

## Application Load Balancer

- Name: `veda-task8-alb`
- Type: Application
- Scheme: Internet-facing
- IP Address Type: IPv4

## Listeners

### HTTP

- Protocol: HTTP
- Port: 80
- Action: Redirect
- Destination: HTTPS
- Port: 443
- Status Code: 301

### HTTPS

- Protocol: HTTPS
- Port: 443
- Action: Forward
- Target Group: `veda-task8-tg`

## ACM

- Domain: `www.veda-task8.isroot.in`
- Validation: DNS
- Key: RSA 2048
- Status: Issued

## DNS

### CNAME

`www.veda-task8.isroot.in`

points to:

`veda-task8-alb-1918391427.ap-south-1.elb.amazonaws.com`
