# xcrun error 해결법

### Error
```
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
```

vscode에서 컴파일을 하는데 `xcrun error`가 떴다.
읽어보니 Xcode Command Line Tools에 이슈가 발생해서 되지 않았던 것이다.

### 해결법
```
xcode-select --install
```
터미널에서 위의 명령어를 입력하면 설치하는 창이 뜬다. 확인을 누르고 기다리고 나서 다시 컴파일을 해보니 정상적으로 돌아간다! 왜 갑자기 안된 건지 자세히는 모르겠다. 찾아보니 Mac Os 업데이트를 하면 이런 이슈가 생길 수도 있다고 한다.