### Work In Progress

A k8s deployment and service are specified in deployment.yaml. Here, the version of the container images is `{{.VERSION}}`
which will later be replaced by the value of the environment variable `PLUGIN_VERSION`.

The executable starts deployment and service initially and updates them accordingly if the called later.

This scenario is using or can use, respectively, the following images from docker hub:

stefanhans/webserver:1.0.0 (green)

stefanhans/webserver:1.0.1 (blue)

stefanhans/webserver:1.0.2 (yellow)

stefanhans/webserver:1.0.3 (red)

stefanhans/webserver:1.0.4 (gray)

All images are simply presenting one webpage and the versions change mainly the background color.

### Prerequisites:

Go, Docker, and Kubernetes, e.g. [minikube](https://github.com/kubernetes/minikube)

Build your Go executable, e.g. `GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o ./deploy`

Set the version and test (does the initial deployment)

    export PLUGIN_VERSION=1.0.0
    ./deploy

Edit the deployment.yaml (or don't)

Copy all files according to the Dockerfile, i.e. config, ca.crt, client.crt, client.key

Build the docker image, e.g. `docker build -t stefanhans/drone-deploy-ramped:0.0.1 .`

Test the docker image, e.g. `docker run -e PLUGIN_VERSION="1.0.5" --rm --network="host" stefanhans/drone-deploy-ramped:0.0.1`

---

Next steps - done:

- Getting a running drone pipeline :thumbsup:

- Check `--network="host"` regarding drone pipeline :thumbsup:


BTW: [source: stefanhans/webserver](https://github.com/stefanhans/Go4k8s/tree/master/Showcase/Images/test-webserver)
