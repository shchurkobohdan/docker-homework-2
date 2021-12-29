#Example 1 is about bind mount
1. docker build -t example1:latest -f example-1/Dockerfile ./example-1
2. docker run --name bind-mount --mount type=bind,source=$(pwd)/example-1/source,target=/usr/share/nginx/html -p 8081:80 example1:latest
3. check localhost:8081 - You should see "This is example with bind mount!" text
4. if change something in example-1/source/index.html it should be reflected on the page in browser


#Example 2 is about volume mount
1. docker build -t example2:latest -f example-2/Dockerfile ./example-2
2. docker run --name volume-mount --mount type=volume,source=my-volume,target=/usr/share/nginx/html -p 8082:80 example2:latest
3. docker exec -it <container_id>> /bin/bash
4. echo '<!DOCTYPE html><html><head><title>Page Title</title></head><body><h1>This is example with volume mount!</h1></body></html>'>/usr/share/nginx/html/index.html
   root@cdd911862aad:/# bash: /usr/share/nginx/html/index.html (execute inside the container)
5. open localhost:8082 in browser - You should see "This is example with volume mount!" text