# SSL/TLS Email Server Demo on AWS EC2 using Amazon Linux 2023

- [SSL/TLS Email Server Demo on AWS EC2 using Amazon Linux 2023](#ssltls-email-server-demo-on-aws-ec2-using-amazon-linux-2023)
  - [Web server configuration](#web-server-configuration)
  - [Domain name configuration](#domain-name-configuration)
  - [SSL/TLS configuration for web server](#ssltls-configuration-for-web-server)
  - [SMTP server configuration](#smtp-server-configuration)
  - [IMAP server configuration](#imap-server-configuration)
  - [Certificate auto-renewal](#certificate-auto-renewal)

## Web server configuration

1. Lets update the packages

   ```
   sudo dnf update -y
   ```

2. Let's upgrade the updatable packages

   ```
   sudo dnf upgrade -y
   ```

3. Install NginX package

   ```
   sudo dnf install nginx -y
   ```

4. Verify NginX package installation

   ```
   sudo nginx -v
   ```

5. Start NginX

   ```
   sudo systemctl start nginx.service
   ```

6. Check NginX status

   ```
   sudo systemctl status nginx.service
   ```

7. Set NginX auto-start

   ```
   sudo systemctl enable nginx.service
   ```

8. Allow inbound http and https traffic

   ```
   sudo dnf install firewalld -y
   sudo systemctl start firewalld
   sudo systemctl enable firewalld
   sudo firewall-cmd --get-active-zones
   sudo firewall-cmd --zone=public --add-service=http
   sudo firewall-cmd --zone=public --add-service=https
   sudo firewall-cmd --permanent --zone=public --add-service=http
   sudo firewall-cmd --permanent --zone=public --add-service=https
   sudo firewall-cmd --reload
   ```

9. Test NginX home page through HTTP using our public IP address (**remember to update the public IP address**)

   ```
   curl 44.206.34.40
   ```

## Domain name configuration
## SSL/TLS configuration for web server
## SMTP server configuration
## IMAP server configuration
## Certificate auto-renewal
