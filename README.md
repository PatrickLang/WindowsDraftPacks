
## Tools needed

- [Draft](http://draft.sh) v0.16.0+ - `choco install draft`
- [Helm](http://helm.sh) v2.11.0+ - `choco install kubernetes-helm`



```powershell
$ENV:KUBECONFIG=(gci .\kubeconfig.json).FullName

draft init
draft pack-repo add 

```