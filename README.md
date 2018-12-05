# Windows Draft Packs
This is a work-in-progress set of [Draft](http://draft.sh) packs tailored to Windows applications. The long-term goal is to make Draft able to detect whether an app is for Windows, Linux, or another OS and apply the right pack. For now, this repo has Windows-only packs that you can pass to `draft create`.

- packs/**CSharpWindowsNetFx** - this is based off of https://github.com/Azure/draft/pull/893
- packs/**CSharpWindowsNetCore** - this is based off https://github.com/Azure/draft/tree/master/packs/csharp 


## Tools needed

- [Draft](http://draft.sh) v0.16.0+ - `choco install draft`
- [Helm](http://helm.sh) v2.11.0+ - `choco install kubernetes-helm`


## Setting up Draft

First, you need to finish setting up Draft, and getting the Windows Draft packs used to build & deploy Windows code.

```powershell
draft init
draft pack-repo add https://github.com/PatrickLang/WindowsDraftPacks
```

## Configure Draft for your Kubernetes cluster and container registry


```powershell
# Set KUBECONFIG for your cluster
$ENV:KUBECONFIG=(gci .\kubeconfig.json).FullName

# Change this to your username
# run docker login first
draft config set registry docker.io/patricklang
```


> TODO: Finish logging into Azure Container Register


## Building a sample project

```
cd \repos
git clone https://github.com/dotnet/dotnet-docker.git
cd dotnet-docker\samples\aspnetapp\aspnetapp
draft create -p CSharpWindowsNetCore
draft up
```



This will automatically build the code, push it to the container registry, and deploy it to the cluster

```
Draft Up Started: 'aspnetapp': 01CXYFNZHDP4ZT0F646FZ9FFKZ
aspnetapp: Building Docker Image: SUCCESS ⚓  (1.0010s)
aspnetapp: Pushing Docker Image: SUCCESS ⚓  (2.3559s)
aspnetapp: Releasing Application: SUCCESS ⚓  (42.7079s)
Inspect the logs with `draft logs 01CXYFNZHDP4ZT0F646FZ9FFKZ`
```

Since it's a Helm chart, you can also check the state with Helm

```
 helm list
NAME            REVISION        UPDATED                         STATUS          CHART                   APP VERSION     NAMESPACE
aspnetapp       1               Wed Dec  5 06:08:06 2018        DEPLOYED        aspnetapp-v0.0.1                        default
PS C:\temp\aspnetapp> helm status aspnetapp
LAST DEPLOYED: Wed Dec  5 06:08:06 2018
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Service
NAME                 AGE
aspnetapp-aspnetapp  6m

==> v1/Deployment
aspnetapp-aspnetapp  6m

==> v1/Pod(related)

NAME                                 READY  STATUS   RESTARTS  AGE
aspnetapp-aspnetapp-7b9449988-bfxt2  1/1    Running  0         6m


NOTES:

  http://aspnetapp. to access your application

```