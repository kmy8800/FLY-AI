# 

### Rest Client
- Node.js, Python, java ... 등 웹을 통해 Azure Resouce Manager로 요청

### Azure Bash

-Resource Group 생성
```bash
az group create --location westus --name myRG
```

-Virtual Machine 생성
```bash
az vm create -n MyVM -g MyRG --image UbuntuLT --generate-ssh-keys --location koreacentral
```

### Azure CLI
- Azure cloud shell을 windows shell, linux bash에서 사용할 수 있도록함
- Azure CLI 설치
- https://docs.microsoft.com/ko-kr/cli/azure/install-azure-cli

```bash
az login
```

### Azure

- metric 대시보드에 저장 -> 공유 대시보드에서 확인가능(Grafana도 가능)
- 잠금 -> 삭제 잠금으로 실수로 인한 삭제를 방지
- 구독 1개 당 테넌트 1개
- [구독 -> 액세스 제어 -> 역할 할당]을 통해 권한 부여 가능(소유자, 기여자 등)

### Azure IaaS
- 로드밸런스(부하분산기)가 소프트웨어적으로 서버에 가하는 부하를 일정한 규칙(옵션)에 따라 분산시켜줌

-IPv4: 32bit, 
