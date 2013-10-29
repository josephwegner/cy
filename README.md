cydoemus
========

Generates Cryptographically Secure Reusable Keys

# Install

## Dependencies
- Obviously, you need to install [node.js](http://nodejs.org).
- [MongoDB](http://www.mongodb.org/)
- You might need to install CoffeeScript globally.  I'm honestly not sure.  
`npm install coffee-script -g` *this might need some sudo magic*
- [Foreman](https://github.com/ddollar/foreman) is optional


## The Actual Server
1. Check it out  
`git clone git@github.com:josephwegner/cydoemus.git`

2. Get in there  
`cd cydoemus`

3. Install those modules  
`npm install`

4. Start that server   
If you're using foreman:  
`foreman start -f Procfile.local`  
If you're not using foreman:  
`mongod`   
then  
`coffee index`  

# Usage
For now, it just generates a random key.  And doesn't do anything with it.

# Deploy

Visit Digital Ocean
Boot up an instance with Ubuntu 13.04 x64
SSH in to your brand new server
Install dokku

    jesse@remote: wget -qO- \
   https://raw.github.com/progrium/dokku/master/bootstrap.sh \
 | sudo bash

    jesse@remote: touch /home/git/VHOST
    jesse@remote: echo <your_domain_name> > /home/git/VHOST

    jesse@local: cat ~/.ssh/id_rsa.pub| ssh user@<your_domain_name> "sudo gitreceive upload-key username"
    jesse@local: git clone https://github.com/waltzio/cy
    jesse@local: git remote add deploy git@<your_domain_name>:cy

    jesse@remote: mkdir /home/git/cy
    jesse@remote: vi /home/git/cy/ENV

        export CLEF_APP_ID=<YOUR_CLEF_APP_ID>
        export CLEF_APP_SECRET=<YOUR_CLEF_APP_SECRET>
        export MONGOLAB_URI=<MONGO_LAB_URI>
        export NODE_ENV=production
        export application_env=production
        export URL=<URL_OF_APP>
        export HOST=<URL_MINUS_PROTOCAL_AND_PORT>


    jesse@remote: cd /home/git/cy
    jesse@remote: mkdir ssl
    jesse@remote: touch server.crt (add actual SSL certificate)
    jesse@remote: touch server.key (add actual SSL private key)

    jesse@local: git push deploy master

Go to [http://localhost:3333/api/v0/keys](http://localhost:3333/api/v0/keys)