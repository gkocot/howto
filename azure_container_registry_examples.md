# Resource group & Azure Container Registry name
devops-jenkins-aci-prd-rg devopsACIContainerRegistry

# Working with ACR
List repositories in an Azure Container Registry.
```
$ az acr repository list --name devopsACIContainerRegistry
[
  ...
  "jenkins/gateway-agent",
  "jenkins/gk-agent",
]
```

Show tags for a repository in an Azure Container Registry.
```
$ az acr repository show-tags --name devopsACIContainerRegistry --repository jenkins/gk-agent
[
  "1-S83969",
  "2-S83969",
  "latest-S83969"
]
```

Get the attributes of a repository or image in an Azure Container Registry.
```
$ az acr repository show --name devopsACIContainerRegistry --image jenkins/gk-agent:latest-S83969
{
  "changeableAttributes": {
    "deleteEnabled": true,
    "listEnabled": true,
    "readEnabled": true,
    "writeEnabled": true
  },
  "createdTime": "2022-06-08T12:48:45.6572078Z",
  "digest": "sha256:84af91655223eeb724dd018e0fa0cafaeb6ca8d21680afcc0a36bf4c85319a55",
  "lastUpdateTime": "2022-06-08T13:06:57.5425096Z",
  "name": "latest-S83969",
  "signed": false
}
```

az container create -g devops-jenkins-aci-prd-rg --name gktest1 --image jenkins/gk-agent:latest-S83969
