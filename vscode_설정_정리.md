
---

# 1. c_cpp_properties.json (인텔리센스 설정)

* 역할: VSCode의 코드 자동 완성, 에러 검출, 코드 점프(정의로 이동 등) 기능, 즉 인텔리센스(IntelliSense)가 올바르게 작동하기 위해 컴파일러의 위치와 C++ 표준 버전 등을 알려주는 파일입니다.
* 핵심 설정: compilerPath에 우리가 주력으로 사용하기로 한 Homebrew의 clang++ 경로를 명확하게 적어주는 것이 가장 중요합니다.

### 📝 `.vscode/c_cpp_properties.json` 내용:

```json
{
    "configurations": [
        {
            "name": "Mac",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [],
            "macFrameworkPath": [
                "/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/System/Library/Frameworks"
            ],
            "compilerPath": "/opt/homebrew/bin/clang++",
            "cStandard": "c17",
            "cppStandard": "c++17",
            "intelliSenseMode": "macos-clang-arm64"
        }
    ],
    "version": 4
}
```

---

# 2. tasks.json (빌드 설정)

* 역할: 소스 코드를 컴파일해서 실행 파일을 만드는 빌드(컴파일) 명령어를 정의하는 파일입니다. VSCode에서 `Cmd+Shift+B` 키를 누르면 여기에 정의된 명령이 실행됩니다.
* 핵심 설정:
  * `command`: 어떤 컴파일러를 쓸지 정합니다. (`/opt/homebrew/bin/clang++`)
  * `args`: 컴파일 옵션을 지정합니다.
    * `-g`: 디버깅 정보를 포함시킵니다. (필수)
    * `${file}`: 현재 열려있는 파일을 컴파일 대상으로 합니다.
    * `-o`: 결과물(실행 파일)의 이름을 지정합니다.
  * `label`: 이 빌드 작업의 이름입니다. `launch.json`에서 이 이름을 사용합니다.

### 📝 `.vscode/tasks.json` 내용:

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: clang++ build active file",
            "command": "/opt/homebrew/bin/clang++",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "compiler: /opt/homebrew/bin/clang++"
        }
    ]
}
```

---

# 3. launch.json (디버거 설정)

* 역할: 코드를 디버깅(중단점 설정, 변수 값 확인 등)할 때 필요한 설정을 정의합니다. `F5` 키를 누르면 이 설정에 따라 디버거가 실행됩니다.
* 핵심 설정:
  * `program`: 디버깅할 실행 파일의 경로를 지정합니다. (`tasks.json`에서 만든 결과물 경로와 일치해야 합니다.)
  * `miDebuggerPath`: 사용할 디버거의 경로입니다. macOS의 기본 디버거인 `lldb`를 사용합니다.
  * `preLaunchTask`: 가장 중요! 디버깅을 시작하기 전에 실행할 작업을 지정합니다. 여기에 `tasks.json`에서 설정한 `label` 이름("C/C++: clang++ build active file")을 정확히 적어주면, `F5`를 누를 때마다 자동으로 컴파일을 먼저 수행하고 최신 코드로 디버깅을 시작합니다.

### 📝 `.vscode/launch.json` 내용:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "C/C++: clang++ build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "lldb",
            "miDebuggerPath": "/usr/bin/lldb",
            "preLaunchTask": "C/C++: clang++ build active file"
        }
    ]
}
```

---

# 요약

이제 C/C++ 프로젝트를 새로 시작할 때마다, 프로젝트 루트 폴더에 `.vscode` 폴더를 만들고 이 세 가지 파일을 복사해 넣기만 하면 됩니다. 그러면 바로 코드를 작성하고, `Cmd+Shift+B`로 빌드하고, `F5`로 디버깅을 시작할 수 있습니다.

