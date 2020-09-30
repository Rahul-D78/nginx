##How to set up nginx in ubuntu(focal-fossa)
1.After copying all the files we have to point our domain name to the new server.craete a record in our hoisting providers dns settings by pointing the domain name.
  ```sudo cp /home/rahul/Documents/. /var/www/ ```
2.Define the ip address and the domain name in the /etc/hosts file.

------If you are doing it for a remote server then jsut do root@(IP of remote server)-----
  ``` sudo vi /etc/hosts --> 0.0.0.0 smaple.com ```

3.Move the static files into the server.sice we cannot deliver our files if the server doesnot have it.

4.All the files are getting copied securely
  ```scp -r * 0.0.0.0:/var/www/demo```
here inside the demo folder all my static files are present.

5.change the permission
  ```sudo chmod -R 777 * ```

6.configure our nginx service to server to our website
  1st. move to the nginx folder and check the files available
  ```cd /etc/nginx```

7.About sites available ---> contains all the indivisual config files for our website static files.

8.About sites-enable ---> contains the links to the config files that nginx is going to read and run.

9.Let's create a file in the sites-availabe and then we goona create a symbolic link to that file in the sites-enable folder and tell nginx to run it.

10.define the config in sudo vi sites-available/demo file
server {
listen 80 default_server;
listen [::] default_server;
root /var/www/demo;
index index.html;
server_name demo;
location / {
try_files $uri $uri/ =404
}
}

---------------The request that i have requested for sample.com that should be
served by this perticular block. --------------------------

11.Now we have to tell the sites-enable to enable it.(Symbolic link)
``` sudo ln -s /etc/nginx/sites-available/demo /etc/nginx/sites-enabled/demo ```

12.In My case we have configure our website to run on the por 80 and ngnix is also running on the port 80 so for change this change the default file in the enable folder and remove it put somewhere else.

```sudo mv /etc/nginx/sites-enabled/default /etc/rahul/home ```

13.restart the nginx server
``` sudo systemctl restart nginx ```

