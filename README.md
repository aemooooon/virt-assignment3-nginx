A Nginx Docker image use to Virtualization assignment 3

### Create an Nginx Container
1. In my local machine make a directory 'nginx' to serer as a build context. Place a dockerfile in it with the following:
```bash
FROM nginx:1.13
COPY flaskapp.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
```
2. Add flaskapp.conf file to the context with the following:
```bash
resolver 127.0.0.11 valid=1s;
server {
  set $alias "flaskapp";
  location / {
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_pass http://$alias:5000;
  }
  listen 80;
}
This will cause nginx to send proxy requests to a flaskapp host.
```
3. Initialize this directory as a GitHub repository, also create a repository on GitHub, and set up the remote link later on push it.
4. Build this image with the tag: `sudo docker build -t="aemooooon/nginx" .`
5. Push to DockerHub with command `sudo docker push aemooooon/nginx`
6. Go to my repository of DockerHub Builds/tab, set up Automated Builds
