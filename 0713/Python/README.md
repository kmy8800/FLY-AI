# Python
### python venv
- python -m venv <venv-name>

- activate venv
```shell
<venv>/Scripts/Activate.ps1
```
```bash
source <venv>/Scripts/activate
```


### Dependency management (종속성 관리)

- requirements.txt
```bash
pip freeze  # make requirements.txt file
```

package c>=1, <=2.0
package a
package b
와 같은 상황일 때 

- Pipenv
- 다른 종속성을 갖는 프로젝트 개발환경 (static binding)
- pip file(requirements.txt 대체 파일)과 Pipfile.lock(결정 빌드 지원)을 생성


```bash
pip install pipenv
```
```bash
pipenv install numpy
pipenv install flask==0.12.1
pipenv install pytest --dev  / 운영이 아닌 개발에만 적용되도록 지정
```

### PyInstaller
- Distributing Python Application
- https://sdldocs.github.io/pyinstaller
                   
```bash
   pip install pyinstaller
                   
   pyinstall cli.py
```

                   
                   
                   
                   asdasd
