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

  **Create a new regular user on both of your droplets, you can use the same user-name and     password for both droplets, this will make your life easier.

**Step three** 

Install a Web server on both of your droplets. Don’t configure them yet.

If you used Nginx for the week 12 lab use Caddy for the Assignment. If you used Caddy for the week 12 lab use Nginx for the assignment.

**Step four**

Write your “web app”. Since we are more interested in the server configuration than writing a web app, hello world works for this assignment. 

Create a new directory on your local machine (WSL for the windows people) 2420-assign-two might be a good name for this directory.

Inside of this directory create 2 new directories **html** and **src**.

Inside of the html directory create an index.html page

Inside of your index.html document create a simple but complete html document (include a doctype, head, body… all the stuff an html document should have).

Inside of the src directory create a new node project.

`npm init` 

`npm i fastify` to install fastify.

create an index.js file and add in the fastify hello world example.

**You will need to alter this file slightly to work with the rest of the assignment. Figuring out what you need to change is part of the assignment.**

Test your server locally and move both your html and src directory to both of your servers.

```jsx
// Require the framework and instantiate it
const fastify = require('fastify')({ logger: true })

// Declare a route
fastify.get('/', async (request, reply) => {
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
