# Windows Draft Packs
This is a work-in-progress set of [Draft](http://draft.sh) packs tailored to Windows applications. The long-term goal is to make Draft able to detect whether an app is for Windows, Linux, or another OS and apply the right pack. For now, this repo has Windows-only packs that you can pass to `draft create`.

- CSharpDotNetFx - this is based off of https://github.com/Azure/draft/pull/893
- CSharpDotNetCore - TODO


## Tools needed

- [Draft](http://draft.sh) v0.16.0+ - `choco install draft`
- [Helm](http://helm.sh) v2.11.0+ - `choco install kubernetes-helm`



```powershell
$ENV:KUBECONFIG=(gci .\kubeconfig.json).FullName

draft init
draft pack-repo add 

```