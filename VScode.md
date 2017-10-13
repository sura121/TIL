##VScode 기본세팅

**언어 세팅**

	IDE툴에서 사용하고자 하는 언어를 세팅합니다. VScode에서 툴을 다운로드 받으면 디폴트로 보인 브라우저의 Locale정보를 이용하여 언어가 세팅 되어 집니다. 언어를 바꾸고 싶다면 Ctrl + P를 누른 다음 > Configure Language 에서 원하는 언어로 바꾸면 됩니다.
    
##VScode 프로젝트 설정

 1.build.gradle을 사용.
 2.vscode의 build command(ctrl+shitf+b)로 c:\> gradle compilejava
 3.그리고 F5를 눌러서 debugger를 시작.
 4.자동으로 launch.json이 만들어진다.
 5.이 launch.json의 jdkPath를 설정.

**build.gradle**
```
apply plugin : 'java'
```

**task.json 설정**
```
{
    "version": "0.1.0",
    "isShellCommand": true,
    "isBackground": true,
    "showOutput": "always",
    "suppressTaskName": true,
    "tasks": [
        {
            "taskName": "build",
            "command": "c:/Program Files/Java/jdk1.8.0_121/bin/javac.exe",
            "args": ["-g", "${file}"],
            "isBuildCommand": false
        },
        {
            "taskName": "build-gradle",
            "command": "c:/Program Files/gradle/gradle-3.4/bin/gradle.bat",
            "showOutput": "always",
            "args": ["compileJava"],
            "isBuildCommand": true
        }
    ]
}
```

**launch.json :F5(start debugging)을 누르면, launch.json이 만들어진다. jdkPath부분만 추가로 설정해 주면 된다. java.exe의 path를 적으면 된다.**

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Java",
            "type": "java",
            "request": "launch",
            "stopOnEntry": true,
            "cwd": "${fileDirname}",
            "startupClass": "${fileBasename}",
            "options": [
                "-classpath",
                "\"${fileDirname};.\""
            ],
            "jdkPath": "c:/Program Files/Java/jdk1.8.0_121/bin"
        },
       ...
}

```

**VScode 특징**

폴더 단위로 개발환경을 달리 꾸밀 수 있다.
폴더는 일종의 프로젝트 단위다. 예를 들어 A라는 폴더에는 C++ 프로젝트 B라는 폴더에서는 파이썬 프로젝트가 진행중이라고 하면. 그러면. .vscode라는 폴더를 A와 B각각에 두어 이 폴더에 환경 세팅을 위한 설정파일들을 만들어 넣어두면 된다. 

1.환경설정 파일에는 빌드를 하는 방법에 대한 설정(tasks.json)
2.사용자 환경설정(setting.json)
3.환경 변수 설정(launch.json)과 같은 파일들이 있다.

 이 파일들을 .vscode폴더에 넣어두면 VSCode가 A또는 B라는 폴더를 열어볼 때 .vscode에 있는 환경설정파일을 읽어들인다. 이렇게 읽어 들인 환경 설정은 기본 설정보다 우위에 있다.

![](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile27.uf.tistory.com%2Fimage%2F25195D4858FEBE3C28703A)

 - 기본적으로 task.json이 있어야 빌드가 가능하다. 폴더만 만들고 빌드 테스트를 위한 간단한 소스를 작성하고 빌드를 위하여(Ctr+shift+b)를 눌러보면 정의된 빌드 작업이 없다고 나타 날 수도 있다. 이 문구가 뜨는 이유는 task.json이 없기 때문이다.

![](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F21127A5058FECA3F1DB0EF)

 - 빌드 작업 구성(Ctr+p 누르고 > 명령 표시 및 실행으로 빌드 작업 구성을 찾으면 된다.)을 누르면 명령 팔레트가 뜨는데 Other를 선택하면 기본적으면 .vscode 와 task.json 이 만들어 진다.

![](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F2124D34C58FECBC411192B)

 찾아보니 버전이 업데이트 되어 0.2.0 버전의 task.json과 launch.json 설정 방법이 조금 씩 달라 졌습니다.
 
 ![](https://github.com/Microsoft/vscode-docs/raw/master/docs/languages/images/java/java-debug.gif)
 
  - mainClass 설정만 하면 됩니다.
`task.json 과 launch.json 사용자 설정시(Usersetting)에는 사용자가 설정한 setting.json이 생깁니다.` 
##VScode gitignore 파일

```
.vscode/*
!.vscode/settings.json
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json
```
