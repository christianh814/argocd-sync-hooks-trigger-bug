# ArgoCD 3.4.1 sync hook bug

This repo intends to reproduce the bug in ArgoCD 3.4.1 where Sync hooks do not trigger when a code update triggers an automated sync happens.


## How to reproduce the bug

1. Fork/Clone this repository (if you want to test by changing the image version backa nd forth)
1. Deploy this application (sample application.yaml manifest provided)
1. Wait for everything to deploy and install
1. Update the spec of the deployment. I've personally tested it by changing the image tag of the `go-httpbin` image from `2.18.3` to `2.22.1` and swap them back and forth each time to trigger a new deploy
1. Wait (or refresh the app) to trigger the automated sync. In ArgoCD versions < 3.4.1 the `PreSync` and `PostSync` hooks trigger. In ArgoCD 3.4.1 the hooks are ignored and the deployment is updated instantly.


## Demo GIFs

Expected Behavior (tested with ArgoCD 3.3.9 and 3.2.5)

<img width="1568" height="800" alt="Image" src="https://github.com/user-attachments/assets/cfb450dc-eabc-4433-a55a-acb31f767fb0" />

Broken Behavior (tested with ArgoCD 3.4.1)

![brokendemo](https://cdn.zappy.app/c8cae15b965c5920a92ae570efae8754.gif)
