# 

### Rest Client
- Node.js, Python, java ... 등 웹을 통해 Azure Re souce Manager로 요청

### Azure Bash

Resource Group 생성
```bash
az group create --location westus --name myRG
```

Virtual Machine 생성
```bash
az vm create -n MyVM -g MyRG --image UbuntuLTs --generate-ssh-keys --location koreacentral
```
