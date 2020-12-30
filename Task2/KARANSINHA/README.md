# This is the completed task detail.
 *I have deployed the repo (fuzzy_happiness_bookmark](https://github.com/GlitchBrain/fuzzy-happiness-bookmarks.git) in a DigitalOcean droplet*

 ## access the site at http://157.230.191.146/

 # Steps I have taken to complete the task :
 >initialize a VM in DigitalOcean with ubuntu image, 1 GB ram/cpu with size 25 gb.
 >fork the original fuzzy_happiness_bookmark 
 >git clone the forked repo in my server
 >install nvm 
 >install latest nodejs and npm
 >install nginx server
 >install pm2 via npm
 >make changes in the `/etc/nginx/sites-available/default` 
    `location / {}` to 
    `location / {
                proxy_pass http://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header upgrade $htp_upgrade;
                proxy_set_header Connection 'upgrade'
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade; }`
 > go to the root directory of the fuzzy_happiness_bookmark git cloned and execute the following commands
  * ` npm install `
  * `touch .env`
  * `echo "DBURI" >> .env`
  * `npm start`
  * `pm2 start app.js`
  * `sudo ufw allow 3000/tcp`

  
