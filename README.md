# Drone Deployment with MySQL on Kubernetes

Before anything else I want to give a shoutout to my personal hero and role model, [Kelsey Hightower](https://twitter.com/kelseyhightower) [github](https://github.com/kelseyhightower) [youtube](https://www.youtube.com/user/MadHatterConfigMgmt). I got lucky enough to catch one of his demos in Charleston and speak to him after which was what inspired me to start open sourcing some projects to share with the community. Check out some of his videos sometime, I guarantee they'll be some of the most entertaining technical talks you've witnessed.

## Prerequisites

If you don't have a Kubernetes cluster to work with yet, check out my [local-kubernetes-bootstrap](https://github.com/stevenaldinger/local-kubernetes-bootstrap) repo to get started locally with Minikube or go dive into [Google Container Engine](https://cloud.google.com/container-engine/) for a hosted solution.

Make sure you have [Gogs git service deployed](https://github.com/stevenaldinger/k8s-gogs) prior to deploying [drone](https://github.com/drone/drone) or pods will crash when nothing can connect to the [vcs service](https://betterexplained.com/articles/a-visual-guide-to-version-control/).

## Quickstart

`kubectl apply -f ./k8s`

## Usage

Forward port 8000 (or any other) on your local machine to port 8000 of the drone server pod.

`kubectl port-forward drone-server-0 8000:8000 -n cicd`

The `drone` dashboard will be available at [http://localhost:8000](http://localhost:8000). You will be able to login with the same credentials configured for the `Gogs` git service. By default this will be **username**: `gogs`, **password**: `gogs`. After logging in, click on the `Activate repositories` link on the left side of the dashboard and you'll see a sample repository anxiously waiting for you to start tinkering with. Click on the switch icon to _unleash the beast_. Optional configuration can be accessed through the `cog` icon next to the switch if you want. Otherwise, you're done.

Congratulations! You're up and running with your very own Kubernetes cluster complete with a private git repository and continuous integration and deployment available for every project you ever work on from here on out. Time to configure [your first drone.io pipeline!](http://readme.drone.io/usage/getting-started/)

## Contributing

Any contributions are extremely welcome and appreciated. If you see ways to improve the deployments and know how to make it happen, open up a pull request with a brief description of what you did and I'll gladly take a look and merge it in. If you see ways to improve the deployments and don't know how to make it happen, don't be shy about creating a new issue and I'll try to tackle it when I have some time.

Any questions you come up with are also important contributions if they're made publicly where others can stumble across them. I'm still learning so may not have a good answer for you immediately but I promise you won't be ignored.

# TODO / Known Issues:

1. Using a `secret` to set the MySQL database config variables prevents it from properly setting up the database and user for some reason. For the time being the password is just deployed in a `configmap`, although this is insecure.
