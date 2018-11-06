---
title: Setup a blog with Hexo and Nginx
tags:
  - hexo
  - nginx
  - nodejs
  - blog
categories:
  - [Web Development]
  - [Tutorial]
date: 2018-10-29 21:01:53
---


Hexo is a fast, simple & powerful blog framework powered by Node.js. In this article I will explain how I setup this blog using Hexo, Nodejs and Nginx on Ubuntu 16.04.

<!-- more -->

## Requirements
* Nodejs
* Nginx

## Installing Hexo (locally)
Use node to install the hexo command line interface

```
npm install hexo-cli -g
```

Scaffold a new hexo blog

```
hexo init <name of blog>
```

Run a local server to visit your blog on `http://localhost:4000`

```
hexo serve
```

For development purposes it is recommende to install `hexo-server` and `hexo-browsersync` for auto reloading when there are changes detected.

```
npm install hexo-server —-save
npm install hexo-browsersync —-save
```

Now you can run `hexo server`  instead of `hexo serve`  to watch for changes and let browsersync auto reload to reflect the changes made.

## Setup GIT Deployment
Hexo is a static site generator. To deploy your resources you need to generate the static resources and deploy it on your server. We will generate and push our static resources to github which we then can pull and server on our server running nginx.

### Update the Hexo config file

1. Create a new (public) repository on github and copy the url.
2. Open the hexo config file `_config.yml`
3. Make the following deploy changes:

```
...
#Deployment
deploy:
  type: git
  repo: https://github.com/username/repo_name.git
  branch: master
```

### Generate and deploy
You can now generate the static files and use the deploy command to push the static resources to your git repository.

```
#recommended, clear cache
hexo clean
#generate static resources
hexo generate
#push to git
hexo deploy
```

## Nginx setup
Create a public folder where you can pull the static resources from the git repro and server the website.

`mkdir -p /var/www/yourblog/public`

Create or add a basic server block (like virtualhost for apache) to your nginx configuration

```
server {
        listen 80;
        listen [::]:80;

        root /var/www/yourblog/public;
        index index.html index.htm index.nginx-debian.html;

        server_name yourblog.com www.yourblog.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

Restart nginx

`sudo systemctl restart nginx`

Pull your static resources from github in your public folder to publish your blog. To update new content you need to repeat the deployment step and pull the changes in your server. Alternatively you can use git hooks and a bare repo to optimize the deplyoment workflow using a bash script.

## Installing a theme
Themes can be found in the `themes` folder of yout hexo installation. Checkout https://hexo.io/themes/index.html for an overview. You can install the themes inside the themes folder using:

```
git clone <repo_url> themes/<theme-name>
```

Activate theme by modifying `theme` inside `_config.yml` to `theme-name`. This blog uses the NexT theme (https://github.com/theme-next/hexo-theme-next).

## Resources
* Hexojs docs -  https://hexo.io/docs/
* Hexo themes - https://hexo.io/themes/index.html
* Nginx server blocks - https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04
