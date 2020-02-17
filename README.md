# Daniel Johansson Udagram Microservice

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into four parts:
1. [The Simple Frontend](/udacity-c3-frontend)
A basic Ionic client web application which consumes the RestAPI Backend. 
2. A Nginx reverse proxy that dispatches requests to feed & user services
2. [The RestAPI Feed Backend](/udacity-c3-restapi-feed), a Node-Express feed microservice.
3. [The RestAPI User Backend](/udacity-c3-restapi-user), a Node-Express user microservice.

## Steps that have been made
1. Install Travis plugin to github
2. Create Postgres DB in AWS and open up VPC for remote access (for testing)
3. Create S3 bucket and enable CORS
4. Build Frontend and Backend services and push to docker hub (with ionic build, npm run build and finally the comtainer iwth docker build)
5. Run images locally with: docker-compose up
6. Create EKS cluster and config: aws eks --region eu-north-1 update-kubeconfig --name <cluster name>
7. Check EKS config: "kubectl config view" and test connection: "kubectl get svc"
8. Apply AWS secrets
9. Deploy images to cluster: kubectl apply -f "config deploy yaml"
10. List pods and images; kubectl get pod  AND  kubectl get svc
11. Debug: kubectl describe pod "podname" kubectl logs "podname"
12. Expose frontend to internet from cluster: kubectl expose deployment frontend --type=LoadBalancer --name=internet
13. Add rolling update
kubectl set image deployments/backend-feed backend-feed=57192472048/udacity-restapi-feed:v2
kubectl set image deployments/backend-user backend-user=57192472048/udacity-restapi-user:v2
kubectl set image deployments/frontend frontend=57192472048/udacity-frontend:v2
kubectl set image deployments/reverseproxy reverseproxy=57192472048/reverseproxy


### Installing Node and NPM
This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (NPM is included) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

### Installing Ionic Cli
The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI can be found in the [Ionic Framework Docs](https://ionicframework.com/docs/installation/cli).

### Installing project dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the root of this repository. After cloning, open your terminal and run:
```bash
npm install
```
>_tip_: **npm i** is shorthand for **npm install**

### Setup Backend Node Environment
You'll need to create a new node server. Open a new terminal within the project directory and run:
1. Initialize a new project: `npm init`
2. Install express: `npm i express --save`
3. Install typescript dependencies: `npm i ts-node-dev tslint typescript  @types/bluebird @types/express @types/node --save-dev`
4. Look at the `package.json` file from the RestAPI repo and copy the `scripts` block into the auto-generated `package.json` in this project. This will allow you to use shorthand commands like `npm run dev`


### Configure The Backend Endpoint
Ionic uses enviornment files located in `./src/enviornments/enviornment.*.ts` to load configuration variables at runtime. By default `environment.ts` is used for development and `enviornment.prod.ts` is used for produciton. The `apiHost` variable should be set to your server url either locally or in the cloud.

***
### Running the Development Server
Ionic CLI provides an easy to use development server to run and autoreload the frontend. This allows you to make quick changes and see them in real time in your browser. To run the development server, open terminal and run:

```bash
ionic serve
```

### Building the Static Frontend Files
Ionic CLI can build the frontend into static HTML/CSS/JavaScript files. These files can be uploaded to a host to be consumed by users on the web. Build artifacts are located in `./www`. To build from source, open terminal and run:
```bash
ionic build
```
***