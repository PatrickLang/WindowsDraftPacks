# Windows Draft Packs
This is a work-in-progress set of [Draft](http://draft.sh) packs tailored to Windows applications. The long-term goal is to make Draft able to detect whether an app is for Windows, Linux, or another OS and apply the right pack. For now, this repo has Windows-only packs that you can pass to `draft create`.

- packs/**CSharpWindowsNetFx** - this is based off of https://github.com/Azure/draft/pull/893
- packs/**CSharpWindowsNetCore** - this is based off https://github.com/Azure/draft/tree/master/packs/csharp 


## Tools needed

- [Draft](http://draft.sh) v0.16.0+ - `choco install draft`
- [Helm](http://helm.sh) v2.11.0+ - `choco install kubernetes-helm`


## Setting up Draft


```powershell
$ENV:KUBECONFIG=(gci .\kubeconfig.json).FullName

draft init
draft pack-repo add https://github.com/PatrickLang/WindowsDraftPacks

# get sources from ...

```



## Running an app

This is based off the Windows sample in [dotnet/dotnet-docker](https://github.com/dotnet/dotnet-docker/tree/master/samples/aspnetapp/aspnetapp), [Dockerfile.nanoserver](https://raw.githubusercontent.com/dotnet/dotnet-docker/master/samples/aspnetapp/Dockerfile.nanoserver-sac2016)

