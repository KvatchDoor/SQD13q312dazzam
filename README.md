# testpage

docker build -t getting-started .

The docker build command uses the Dockerfile to build a new container image. You might have noticed that Docker downloaded a lot of “layers”. This is because you instructed the builder that you wanted to start from the node:18-alpine image. But, since you didn’t have that on your machine, Docker needed to download the image.

After Docker downloaded the image, the instructions from the Dockerfile copied in your application and used yarn to install your application’s dependencies. The CMD directive specifies the default command to run when starting a container from this image.

Finally, the -t flag tags your image. Think of this simply as a human-readable name for the final image. Since you named the image getting-started, you can refer to that image when you run a container.

The . at the end of the docker build command tells Docker that it should look for the Dockerfile in the current directory.


docker run -dp 127.0.0.1:3000:3000 getting-started
The -d flag (short for --detach) runs the container in the background. The -p flag (short for --publish) creates a port mapping between the host and the container.
The -p flag take a string value in the format of HOST:CONTAINER, where HOST is the address on the host, and CONTAINER is the port on the container.
The command shown here publishes the container’s port 3000 to 127.0.0.1:3000 (localhost:3000) on the host. 
Without the port mapping, you wouldn’t be able to access the application from the host.


docker build -t getting-started .
docker tag getting-started lafrog/getting-started:0.0.1
docker push lafrog/getting-started:0.0.1
docker run -dp 0.0.0.0:3000:3000 lafrog/getting-started:0.0.1
docker exec naughty_gagarin cat /data.txt
docker run -dp 0.0.0.0:3000:3000 --mount type=volume,src=todo-db,target=/etc/todos lafrog/getting-started:0.0.1

docker network create todo-app

docker run -d `
     --network todo-app --network-alias mysql `
     -v todo-mysql-data:/var/lib/mysql `
     -e MYSQL_ROOT_PASSWORD=secret `
     -e MYSQL_DATABASE=todos `
     mysql:8.0
	 
	 
	 
docker run -dp 127.0.0.1:3000:3000 -w /app -v "$(pwd):/app" --network todo-app -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=secret -e MYSQL_DB=todos node:18-alpine sh -c "yarn install && yarn run dev"
In powershell
docker exec -it <mysql-container-id> mysql -p todos
