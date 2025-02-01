# Steps to configure the EC2 instance

1. Create a Security Group that allows connections via SSH, HTTP and HTTPS.
2. Create the EC2 instance and link it to the created Security Group and associate it to the elastic IP created.
3. Connect to the EC2 instance using SSH, using the command: ssh -i path_to_pem ubuntu@publid_DNS_instance.
4. Install apache service with: sudo apt-get install apache2.
5. Download the zip file and unzip.
6. Open the packaje.json and include the "homepage" field with the DNS of the instance, something like "http://DNS_instance", since it will be deployed using HTTP and not HTTPS.
7. Install the required services (nodejs, npm, pm2).
8. Inside the folder of the project, execute "npm install" to install the dependencies.
9. After executing npm install and npm run build, the folder dist/ is created. 
10. Configure the virtual host, first of all by copying the default HTTP configuration file and creating a "react.conf" file.
11. Modify the "react.conf" file, by adding as a ServerName, the DNS of the EC2 instance; comment the DocumentRoot line, and add the ProxyPass to redirect connections to port 5173 (Vite's port).
12. Disable the default HTTP host, and enable the react.conf site.
13. Restart the apache server.
14. Move to the project folder and execute the command: "pm2 start npm --name "vite-server" -- run dev -- --host" to run the project.
15. Go the a web browser and type the DNS of the instance in the URL.
16. The app is displayed. 
