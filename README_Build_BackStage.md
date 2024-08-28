# Build a Backstage App with Gloo Platform Portal Backstage Backend Plugin

Create your Backstage App using `my-backstage-app` as the name:
```sh
npx @backstage/create-app@latest
```
    
Change to your `app` directory:
```sh
cd my-backstage-app
```
    
Verify if you are able to run your Backstage app:
```sh
yarn dev
```
    
Follow this [guide](https://github.com/solo-io/platform-portal-backstage-plugin-backend/blob/main/plugins/platform-portal-backstage-plugin-backend/README.md) to install the plugin into your project.    

In step 2, also comment the following lines:
```
// kubernetes
//backend.add(import('@backstage/plugin-kubernetes-backend/alpha'));
``` 
    
In step 3, here is a sample below:
```
glooPlatformPortal:
  backend:
    portalServerUrl: ${PORTAL_SERVER_URL}
    clientId: ${CLIENT_ID}
    clientSecret: ${CLIENT_SECRET}
    tokenEndpoint: ${TOKEN_ENDPOINT}
    debugLogging: ${PORTAL_DEBUG_LOGGING}
    syncTimeout:
      hours: 0
      minutes: 1
      seconds: 0
      milliseconds: 0
    syncFrequency:
      hours: 0
      minutes: 0
      seconds: 10
      milliseconds: 0
```

Then, build the docker image for Kubernetes deployment:    
In your BackStage app's root directory:   
*Note: replace gmflau/backstage-backend:1.0.0 with your own docker image name and release number.*
```sh
yarn || true
yarn tsc || true
yarn build:all
docker build -f ./packages/backend/Dockerfile --tag gmflau/backstage-backend:1.0.0 .
docker push gmflau/backstage-backend:1.0.0
```