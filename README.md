# html_with_nginx
Deploy a static html app in nginx and access with instance IP in ubuntu

**Commands to be run in the instance**
sudo apt update
sudo apt install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
systemctl status nginx

http://<INSTANCE_PUBLIC_IP>  to access the nginx page as verification

Now Create a html app
mkdir html_app
cd html_app
vim index.html


sudo rm -rf /var/www/html/*        ## deletes the files in the html folder of nginx
sudo mv ~/html_app/* /var/www/html/  ## moves the files from html_app to the html folder of the nginx

##Provides necessary access to the files
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html

**Configure Nginx (Optional)**
sudo nano /etc/nginx/sites-available/html_app
Add the following:
server {
    listen 80;
    server_name _;

    root /var/www/html;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }
}

Save and exit (CTRL + X, then Y, then Enter).

sudo ln -s /etc/nginx/sites-available/html_app /etc/nginx/sites-enabled/

sudo systemctl restart nginx

**Open a browser and visit:**
http://<INSTANCE_PUBLIC_IP>



