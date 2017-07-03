# Drone Deployment with MySQL

## Prerequisites

Make sure `gogs` git repository is deployed prior to deploying `drone` or `drone` will crash when it can't connect to the `vcs` service.

## Quickstart

`kubectl apply -f .`

## Usage

Its common for the drone server pod to need a reboot after MySQL finishes deploying.

Run `kubectl delete po/drone-server-0 -n cicd` to delete the pod and let the `statefulset` automatically recover. Then you should be safe to forward the port and start working with `drone`.

`kubectl port-forward drone-server-0 8000:8000 -n cicd`

The `drone` dashboard will be available at [http://localhost:8000](http://localhost:8000)

`Drone` will be configure with the same credentials set up in `gogs` automatically.

Click on settings in the top right, and then `Account`. Flip the switch on any repositories detected to enable `drone`.
