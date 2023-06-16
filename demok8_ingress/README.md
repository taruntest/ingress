# aspnet-docker
Simple demo of ASP.NET Core and Docker using .NET Core 3.1 LTS.

## Read the Article
To understand how to use this repo, make sure you read this article:   
[Creating ASP.NET Core websites with Docker](https://blog.hildenco.com/2020/10/how-to-create-aspnet-core-website-with.html)

## Requirements
In order to run this example, you'll need to have installed on your machine (Windows, Mac, Linux):
* Docker Desktop (or Docker on Linux)
* .NET Core SDK 3.1

## Running
The steps to run are:
1. clone this tool: `git clone https://github.com/VamsiGullapalli/dotnet-docker` 
2. cd into the folder: `cd dotnet-docker`
3. Build a docker image: `docker build . -t webapp`
4. Run a container with: `docker run -it -p 8080:80 webapp`
    #### `winpty docker run -it -p 8080:80 webapp`
5. Open your browser and navigate to: `localhost:8080`

## Azure ACR 
1. Login to azure account: `az login`
2. Login to acr Registry: `az acr login --name demoacrvamsi`
3. Tag the image built earlier: `docker tag vamsi demoacrvamsi.azurecr.io/vamsi001`
4. Push the image to acr registry with repository name: `docker push demoacrvamsi.azurecr.io/vamsi001`

## ACR AKS
1. Set this variable to the name of your ACR. The name must be globally unique.
    
    `az acr create -n demodotk8 -g myContainerRegistryResourceGroup --sku basic`
2. # Set this variable to the name of your ACR. The name must be globally unique.
   # Create an AKS cluster with ACR integration.

`az aks create -n demodotk8cluster -g demo --generate-ssh-keys --attach-acr demodotk8`

3. ### existing AKS
    # Attach using acr-name
    `az aks update -n demodotk8cluster -g demo --attach-acr <acr-name>`

    `az aks update -n demovamsi -g demo --attach-acr demoacrvamsi`

    # Attach using acr-resource-id
    `az aks update -n demodotk8cluster -g demo --attach-acr <acr-resource-id>`

## Deploy the sample image from ACR to AKS
1. # Ensure you have the proper AKS credentials.
    
    `az aks get-credentials -g demo -n demodotk8cluster`
2. # create deployment file and apply it
    `kubectl apply -f deploy.yaml`


az aks update -n demo001 -g demo --attach-acr dotnetdemok8
az aks get-credentials -g demo -n demo001


## Ingress
Enable ingress controller in Networking


