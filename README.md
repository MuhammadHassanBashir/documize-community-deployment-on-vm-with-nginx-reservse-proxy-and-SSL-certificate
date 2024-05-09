# Documize-community-deployment-on-vm-with-nginx-reservse-proxy-and-SSL-certificate

## RUN DOCKER COMPOSE

- sudo docker-compose up -d
- sudo docker ps   # till here your documize container , postgress , should be running. 

##  Nginx and Reverse proxy installation on vm

### Nginx installation

- sudo apt update
- sudo apt install nginx
- sudo systemctl start nginx  

### Reverse proxy
  
- sudo nano /etc/nginx/sites-available/docs_disearch.conf

  server {
  listen 80;  
  server_name docs.disearch.ai;

  location / {
      proxy_pass http://localhost:5001;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;
  }  
  }

- sudo ln -s /etc/nginx/sites-available/docs_disearch.conf /etc/nginx/sites-enabled/

- sudo nginx -t

- sudo systemctl restart nginx

### Applyin SSL Certificate

- snap version
- sudo apt policy snapd
- sudo apt install snapd
- sudo snap install core; sudo snap refresh core
- sudo apt-get remove certbot
- sudo snap install --classic certbot
- sudo ln -s /snap/bin/certbot /usr/bin/certbot
- sudo certbot --version
- sudo certbot --nginx  

after this give your "email address" then enter "yes" and then enter "no" and select the domin by giving no which you want to add certificate.      after that check           domain on browser. you will get ssl certificate against your domian.
