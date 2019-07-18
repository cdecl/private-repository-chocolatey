## Chocolatey Private Repository

### 1. Chocolatey Private Repository 
- chocolatey.server 패키지 설치 : https://chocolatey.org/packages/chocolatey.server  
```bat
$ choco install chocolatey.server
```

- Install : https://chocolatey.org/docs/how-to-set-up-chocolatey-server  
	- Setup with PowerShell Script 항목을 파일로 저장후 실행 (IIS 세팅)


### 2. 패키지 관리
유료 버전의 경우 choco downlaod 라는 명령이 지원되나, Free 버전은 지원되지 않으므로
Chocolatey 사이트 패키지 관리에서 Download 를 통해서 별도 다운로드를 해야함

#### 2-1. 패키지 업로드
- chocolatey.server 설치된 패키지의 web.config 항목에 apikey강제나 apikey 값을 관리
- 필요에 의해 수정 

```json
    <add key="requireApiKey" value="true" />
    <add key="apiKey" value="chocolateyrocks" />
```

```bat
$ choco push -s http://localhost/chocolatey python.3.7.3.nupkg -k "chocolateyrocks"
```

#### 2-2. 패키지 수동 
- 아래 위치에 .nupkg 파일을 위치 시키면 일정시간 이후 폴더로 풀어짐

```json
 <add key="packagesPath" value="~/App_Data/Packages" />
```


### 2. Private Repository 패키지 설치 
- Source Repository 지정 설치 

```bat
$ choco install -s http://localhost/chocolatey git python vscode 
```

- Source Repository 추가 

```bat
# 위치 지정 - git, python, vscode 설치 
$ choco source add --name=private_repo --source=http://localhost/chocolatey

# 디폴트 위치 참조 - git, python, vscode 설치 
$ choco install git python vscode 
```

- Source Repository List 확인

```bat
$ choco list -s http://localhost/chocolatey 
Chocolatey v0.10.11
7zip 19.0
git 2.21.0
python 3.7.3
vscode 1.32.3
4 packages found.
```
