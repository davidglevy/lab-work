# Minikube Cluster

After a long long time trying to ignore Kubernetes, I'm going
to acknowledge it's likely better than trying to install a
baremetal install lab. I still feel like it is introducing a
very high amount of abstraction on top of a more traditional
setup - which ironically may make the setup more complex.

## Instructions

I'm following these instructions:
https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download

## Non-Privileged User

In order to run Docker without forcing it to ignore warnings, I'm going to create a user
"minikube".

adduser minikube

## We also need to add minikube to Docker so it can use the driver.
groupadd docker
usermod -aG docker minikube

## Running Minikube
I'm still getting docker errors running Minikube. Something about docker not returning healthy.

What is strange is that docker still appears to be working as I can run the hello world successfully.

When I run `minikube start` I see:

```
  - docker: Not healthy: "docker version --format {{.Server.Os}}-{{.Server.Version}}:{{.Server.Platform.Name}}" exit status 1: permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.47/version": dial unix /var/run/docker.sock: connect: permission denied
```

Turns out the docker daemon was running as root - which k8s was borking out about. So if we want Docker to run as non root that's a thing, fixing it I just changed ownership on the socket but not sure if that will persist through reboots.

```
chown root:docker /var/run/docker.sock
```

Now minikube is running successfully. Simple.
