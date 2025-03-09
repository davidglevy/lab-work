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
newgrp docker
usermod -aG docker minikube
