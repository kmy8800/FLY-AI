# DVC

## DVC란
- Data Version Control
- Amazon S3, Microsoft Azure Blob Storage, Google Drive 등에 데이터를 저장하는 것을 관리

### 1. DVC 설치
- python 3.8이상 설치
```bash
sudo apt-get install python3.8
sudo apt-get update
sudo apt-get upgrade

ls -al /usr/bin/pytho

ls /usr/bin/ | grep python

sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.8 3
update-alternatives --config python
```

- git 설치
```bash
sudo apt install git
```

- DVC 설치
```bash
pip install dvc[all]==2.6.4

dvc --version
2.6.4
```
- dvc가 없다고 나올 경우, logout 후 다시 login (PATH 안잡혀서 발생하는 error)

### 2. DVC 저장소 세팅
```bash
mkdir dvc-tutorial
cd dvc-tutorial

git init

dvc init
```

### 3. DVC 기본 명령 1
#### 1) dvc로 버전을 tracking할 data 생성
```bash
mkdir data
cd data

vi demo.txt   # Hello AI!
cat demo.txt
```

#### 2) 데이터를 dvc로 tracking
```bash
cd ..

dvc add data/demo.txt

git add data.demo.txt.dvc data/.gitignore
```

#### 3) git commit
```bash
git commit -m "ADD demo.txt.dvc"
```

#### 4) remote storage 세팅
```bash
dvc remote add -d storage gdrive://<GOOGLE_DRIVE_FOLDER_ID>
```

#### 5) dvc config를 git commit
```bash
git add .dvc/config
git commit -m "add remote storage"
```

#### 6) dvc push
```bas
dvc push
# google login 후 인증
```

### 4. DVC 기본 명령 2
#### 1) dvc pull
```bash
rm -rf .dvc/cache/  # 캐시파일 삭제
rm -rf data/demo.txt  # 원본파일 삭제

dvc pull
```

#### 2) dvc checkout
- data 버전 변경
```bash
vi data/demo.txt  # 내용 변경

dvc add data/demo.txt

git add data/demo.txt.dvc
git commit -m "update demo.txt"

dvc push
```
- 이전 data 버전으로 되돌림
```bash
git log --oneline

#64fbdc5 (HEAD -> master) update demo.txt
#e08b419 add remote storage
#6d7c2eb ADD demo.txt.dvc

git checkout <COMMIT_HASH> data/demo.txt.dvc  # demo.txt.dvc 파일을 이전 버전으로 되돌림

dvc checkout  # demo.txt.dvc 내용을 참조하여 demo.txt 파일 버전 변경
```
