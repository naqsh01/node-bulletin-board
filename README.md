# Git

If you are using Git, you can clone the example project from GitHub:


## Git Clone

Use [git](https://git-scm.com/downloads) to git CLI.

```
git clone https://github.com/dockersamples/node-bulletin-board
cd node-bulletin-board/bulletin-board-app
```


## Define a container with Dockerfile
After downloading the project, take a look at the file called Dockerfile in the bulletin board application. Dockerfiles describe how to assemble a private filesystem for a container, and can also contain some metadata describing how to run a container based on this image.

For more information about the Dockerfile used in the bulletin board application, see Sample Dockerfile.

## Build and test your image
Now that you have some source code and a Dockerfile, it’s time to build your first image, and make sure the containers launched from it work as expected.

Make sure you’re in the directory node-bulletin-board/bulletin-board-app in a terminal or PowerShell using the cd command. Run the following command to build your bulletin board image:


```
docker build --tag bulletinboard:1.0 .
```

You’ll see Docker step through each instruction in your Dockerfile, building up your image as it goes. If successful, the build process should end with a message 
` Successfully tagged bulletinboard:1.0. `

## Run your image as a container
Run the following command to start a container based on your new image:
```
docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
```

There are a couple of common flags here:

--publish asks Docker to forward traffic incoming on the host’s port 8000 to the container’s port 8080. Containers have their own private set of ports, so if you want to reach one from the network, you have to forward traffic to it in this way. Otherwise, firewall rules will prevent all network traffic from reaching your container, as a default security posture.
--detach asks Docker to run this container in the background.
--name specifies a name with which you can refer to your container in subsequent commands, in this case bb.

Visit your application in a browser at `localhost:8000`. You should see your bulletin board application up and running. At this step, you would normally do everything you could to ensure your container works the way you expected; now would be the time to run unit tests, for example.

Once you’re satisfied that your bulletin board container works correctly, you can delete it:

```
docker rm --force bb
```

