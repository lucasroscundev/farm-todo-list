# Farm Stack Todo List Project

This project was built as a means to learn, based upon the FARM Stack FreeCodeCamp video.
The link to the mentioned video is: https://www.youtube.com/watch?v=PWG7NlUDVaA&t=2059s

My intentions for creating this project were to learn: FastAPI and React, improve my understanding of: Git, GitHub and Docker, and deploy the result using a free tool. This project will become a part of my portfolio.

## But what is FARM?
The acronym stands for FastAPI (backend), React (frontend), and Mongodb (database).

## What other tools are needed for this project ?
Docker, Git, GitHub (or your preferred tool, such as GitLab), Python.

## Tools I've used not in the tutorial
Vite, Podman (alternative for Docker, changed half way), Shadcdn (and Tailwindcss)...

## Deployment
Not sure yet, but I'm leaning towards a combination of Vercel for the frontend, and for the backend, well...
Maybe Supabase, railway, netlify, or even deploying everything with Vercel.
Not yet so knowledgeable to launch it in AWS, but I'll get there.

## Database creation on MongoDB
This part is where we create a cloud-based DB to connect to our application.
You have to login to MongoDB or create a new account, either way, you will create a new project and a cluster(for this case, the FREE option is more than enough).
Take note of the username and password, since they are needed for the app to connectto the DB. 
Also, copy the MongoDB URI from the website and paste the value into the .env file located at the root of the project(if you don't have a .env file yet, what are you waiting for? Create it). E.g. MONGODB_URI='<value copied adding password into the URI && a name before "?retryWrite">'.

## The compose.yaml file
We begin the file by attributing a name to the application.
Next, we create the nginx service, which will work as a reverse proxy for our use case. Notice nginx depends on backend && frontend.
The structure of the yaml file is not too complex, but details matter. This is mostly declarative, and the catch is that the tabs/spacing follows Python syntax. What do I mean ? If a statement is under another at a "lower level"/indented, it means it belongs to the upper variable/scope.
The explanation of how this works is a bit too lenghty for me to cover here, so here's a link to help. https://docs.docker.com/reference/compose-file/ -> Here, by going into the cards at the right(e.g. 'Services...') you can find more information and examples. Yaml official docs: https://yaml.org/spec/1.2.2/

## Nginx
We create a folder at root level, named nginx(standard naming, so if you use anotherreverse proxy, attribute its name to the folder).
Inside the folder, we create and nginx.conf file. It contains configurations for ournginx web server. Location <folder> is how we set the proxy. "/" is the root path, which is how we forward the requests to frontend service running in port 3000, and "/api" represents the path to forwarding to the backend, running on port 3001. Check the file to understand better. Here is the link to nginx docs: https://nginx.org/en/docs/ .

### Under Construction...
