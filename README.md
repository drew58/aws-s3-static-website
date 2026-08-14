# AWS S3 Static Website

## Project Overview

A static portfolio website deployed using Amazon S3.

## AWS Services Used

- Amazon S3
- IAM / Bucket Policy

## Architecture

User → Amazon S3 → Website

## What I Learned

- Creating an S3 bucket
- Uploading objects to S3
- Configuring bucket permissions
- Creating an S3 bucket policy
- Hosting static website content
- Understanding public access and security

## Technologies

- HTML
- CSS
- Amazon S3

## Screenshots

## Project Status

Completed

## Project 2: EC2 Web Server Deployment

### Objective

Deploy my existing portfolio website on an Amazon EC2 Linux server and make it publicly accessible over HTTP.

### Architecture

```text
Internet user
     │
     ▼
Public IPv4 address (HTTP port 80)
     │
     ▼
EC2 Security Group
- HTTP (port 80): Anywhere
- SSH (port 22): My IP only
     │
     ▼
Amazon EC2 instance
- Amazon Linux 2023
- Apache HTTP Server (httpd)
     │
     ▼
Portfolio website files
/var/www/html/
```

### AWS Services and Resources Used

- **Amazon EC2** — hosted the web server and portfolio website.
- **Amazon EBS** — attached **8 GiB** of storage to the EC2 instance.
- **Security Group** — controlled inbound network traffic.
- **Public IPv4 address** — allowed the website to be reached from the internet.
- **RSA key pair (`.pem`)** — securely authenticated SSH access to the instance.

### Instance Configuration

| Setting | Configuration |
|---|---|
| Operating system | Amazon Linux 2023 |
| Instance type | `t3.micro` |
| Free Tier status | Free Tier eligible |
| Storage | 8 GiB Amazon EBS |
| Web server | Apache HTTP Server (`httpd`) |
| Website protocol | HTTP |

### Implementation Steps

1. Created an EC2 instance running Amazon Linux 2023 using the `t3.micro` instance type.
2. Configured an 8 GiB EBS volume for the instance.
3. Created and downloaded an RSA `.pem` key pair.
4. Configured the Security Group:
   - Allowed SSH on port 22 only from my IP address.
   - Allowed HTTP on port 80 from anywhere so visitors could access the website.
5. Connected to the instance from Windows Git Bash using SSH and the `.pem` key.
6. Installed Apache using `dnf`.
7. Transferred my existing portfolio files from my local computer to the EC2 instance using `scp`.
8. Copied the website files into Apache’s web root directory:

   ```bash
   sudo cp -r /tmp/* /var/www/html/
   ```

9. Restarted Apache to serve the deployed files:

   ```bash
   sudo systemctl restart httpd
   ```

10. Opened the EC2 public IPv4 address in a browser and verified that the portfolio website loaded successfully.

### Security Considerations

- SSH access was limited to **My IP** rather than being open to the public.
- HTTP was open to the internet on port 80 so the website could be accessed publicly.
- The private `.pem` key is not uploaded to this repository and should be kept secure.
- The project used HTTP for learning purposes. A production deployment should use HTTPS with a domain name and TLS certificate.

### Testing and Result

The deployment was tested by visiting the EC2 instance’s public IPv4 address in a web browser. The portfolio website loaded successfully from the Apache web server running on Amazon EC2.

![Portfolio website successfully served from Amazon EC2](images/ec2-portfolio-live.png)

### Cost Control and Cleanup

This was a learning project using a Free Tier eligible instance type. To avoid unnecessary AWS charges after documenting the project:

- Terminate the EC2 instance when it is no longer needed.
- Confirm that associated resources, including EBS volumes and public IP-related resources, are not left running unnecessarily.
- Review the AWS Billing dashboard regularly.

### Lessons Learned

Through this project, I gained practical experience with:

- Launching and configuring an Amazon EC2 instance.
- Using Amazon Linux 2023 and basic Linux administration.
- Connecting securely to a server with SSH and an RSA key pair.
- Configuring EC2 Security Group rules.
- Installing and managing Apache with `dnf` and `systemctl`.
- Transferring website files with `scp`.
- Deploying static website files to `/var/www/html`.
- Understanding the difference between public IP access, SSH access, and HTTP web traffic.
- Managing cloud resources with cost awareness.





