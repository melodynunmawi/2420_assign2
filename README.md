## Install all requirement before starting assignment
      - WSL and DigitalOcean droplets
      - Ubuntu 22.10 or 22.04
      - Windows Terminal
      - Volta to install node
      - Fastify for your NodeJS server
      
**Step one**

## Create DO infrastructure
        - VPC: vpc-2420
        - Inbound Rules: HTTP ans SSH

![image](https://user-images.githubusercontent.com/59521385/205427992-af24d34c-93b2-459c-8ba8-b768a1bf1979.png)

   Please click this lick for [VPC Infrastructure set up](https://vimeo.com/775412708/4a219b37e7)
## Create new regular user

![image](https://user-images.githubusercontent.com/59521385/205428145-5ba57a68-5155-4cd6-a810-d2dacd9226a4.png)

  **Create a new regular user on both of your droplets, you can use the same user-name and     password for both droplets, this will make your life easier.**

## Install Caddy Web Server
   - install link below in both of your droplets
   
username@droplet:~$ wget https://github.com/caddyserver/caddy/releases/download/v2.6.2/caddy_2.6.2_linux_amd64.tar.gz

   - extract the file by use 
  username@droplet:~$ tar -xvf caddy_2.6.2_linux_amd64.tar.gz  

![image](https://user-images.githubusercontent.com/59521385/205428288-92516da8-86bf-4a25-b1ce-a0610f3ca710.png)


 ## Write a web app
          - create new directory on WSL and called 2420-assign-two. 
          - Inside of this directory create 2 new directories **html** and **src**.
          - Inside of the html directory create an index.html page
            Inside of your index.html document create a simple but complete html document 
            (include a doctype, head, body… all the stuff an html document should have).
          - Inside of the src directory create a new node project.
                - `npm init` 
                - `npm i fastify` to install fastify.
          - Create an index.js file and add in the fastify hello world example.

**Test your server locally (WSL) and move both your html and src directory to both of your droplets servers.**

username@wsl:~$ cd 2420-assign-two/src && curl https://get.volta.sh | bash

username@wsl:~/2420-assign-two/src$ source ~/.bashrc

username@wsl:~/2420-assign-two/src$ volta install node

username@wsl:~/2420-assign-two/src$ npm init

username@wsl:~/2420-assign-two/src$ npm install fastify


![image](https://user-images.githubusercontent.com/59521385/205428737-a38c895a-ae92-4a19-9e34-b72518507a22.png)

![image](https://user-images.githubusercontent.com/59521385/205428784-e4fba462-16e0-45da-8162-b45942e2956f.png)


```jsx
// Require the framework and instantiate it
const fastify = require('fastify')({ logger: true })

// Declare a route
fastify.get('/api', async (request, reply) => {
  return { hello: 'Server x' }
})

// Run the server!
const start = async () => {
  try {
    await fastify.listen({ port: 3000 })
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()
```
   Test your server locally, and go to the provided link.
   username@wsl:~/2420-assign-two/src$ node index.js
 ![image](https://user-images.githubusercontent.com/59521385/205429015-a498dbd0-a0c0-49ea-a16c-e3edf052589e.png)


**Step five**

Write your Caddyfile or Nginx server block on your local machine

In addition to the basic server block that we created last week you are going to add a reverse proxy server.

Your reverse proxy server should forward 

localhost:5050 (http:/127.0.0.1:5050). These are both localhost.

When someone visits your load balancers ip address api.
ie http://134.0.34.138/api they should see the hello world message from your node server.

**Step six**

install node and npm with Volta. npm will be installed alongside the version of node that you install.

You will need to source your .bashrc after installing Volta to install node. Volta will add two lines of code to your .bashrc so that your shell knows where volta is and where volta will install node and npm.

**Step seven**

write a service file on your local machine to start your node application.
Your service file should restart the service on failure (see link below.

Your service file should require a configured network. 

see `man systemd.special` and search for network for how to do this.

remember that you will need to use the full path to your application and the node binary.
