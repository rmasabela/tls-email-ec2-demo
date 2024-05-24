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

10. Create NginX configuration file for our domain (**remember to update the web site domain name**)
    
    ```
    sudo nano /etc/nginx/conf.d/www.rmasabel.net.conf
    ```

    And paste the contents for the file (**remember to update the domain name 02 times**)

    ```
    server {
        listen 80 default_server;
        listen [::]:80 default_server;
        root /var/www/html;
        server_name rmasabel.net www.rmasabel.net;
    }
    ```

    Finally, copy the contents of the default NginX site to the new path

    ```
    sudo mkdir /var/www
    sudo cp /usr/share/nginx/html /var/www -r
    ```

11. Now we should reload our NginX service using our updated settings

    ```
    sudo nginx -t && sudo nginx -s reload
    ```

12. Now, we must update our DNS configuration so we have two A records (for both the **default** and the **www** subdomains)

    ![DNS records should look like these](dns-records.png)

13. Test NginX home page through HTTP using our domain name via curl (**remember to update the domain name**)

    ```
    curl www.rmasabel.net
    ```

    The system will return the HTML code for our home page. I have customized the home page, so you should get the default NginX home page HTML code.

    ```
    <!DOCTYPE html>
    <html>
    <head>
    <title>&iexcl;El sitio de Richie!</title>
    <style>
    html { color-scheme: light dark; }
    body { width: 35em; margin: 0 auto;
    font-family: Tahoma, Verdana, Arial, sans-serif; }
    </style>
    </head>
    <body>
    <h1>&iexcl;El sitio de Richie!</h1>
    <p><img src="logo.png" alt="Logo" width="296" height="244"></p>

    <p>Consultor en DevOps, Agilidad Empresarial y tecnolog&iacute;as de Nube.<br/>
    Escr&iacute;beme <a href="mailto:ricardo.masabel@outlook.com?subject=Correo desde el sitio web">aqu&iacute;</a>.</p>

    <p><em>&iexcl;Gracias!</em></p>
    </body>
    </html>
    ```

    If we try our default subdomain (**remember to update the domain name again**), it should also work fine

    ```
    curl rmasabel.net
    ```

## SSL/TLS configuration for web server
## SMTP server configuration
## IMAP server configuration
## Certificate auto-renewal
