# 맥북 메뉴바 색상 변경하는 방법
다크 모드를 사용하더라도, 배경화면이 밝으면 메뉴바도 밝아지는 현상이 있다.   
이를 해결하기 위하여 알아본 것이 [ChangeMenuBarColor](https://github.com/igorkulman/ChangeMenuBarColor)이다.   

1. App-store에서 `Xcode` 설치 및 실행 (꼭 프로그램을 한 번이라도 실행시켜야 한다)
2. 터미널에서 아래 명령어 실행
    ```
    xcode-select --install
    ```
3. 터미널로 프로젝트를 다운받을 폴더로 이동한 뒤 clone
    ```
    git clone https://github.com/igorkulman/ChangeMenuBarColor.git
    ```
4. `ChangeMenuBarColor` 폴더로 이동
    ```
    cd ChangeMenuBarColor
    ```
5. 실행
    ```
    swift build -c release
    ```
    만약 아래와 같은 에러가 뜬다면, Xcode가 제대로 설치되었는지 확인한다.
    ```
    error: terminated(72): /usr/bin/xcrun --sdk macosx --find xctest output:
    xcrun: error: unable to find utility "xctest", not a developer tool or in PATH
    ```
6. `./build/release` 폴더 안에 실행할 수 있는 `ChangeMenuBarColor` 파일 생성
    ```
    cp .build/release/ChangeMenuBarColor .
    ```
   
### 고정된 색상으로 변경
배경사진 경로는 입력하지 않아도 적용 된다.
```
./ChangeMenuBarColor SolidColor "desired_hex_color"  "optional_path_to_your_wallpaper"
```
만약, 1개 이상의 모니터를 사용하고 있을 시, 모두 변경을 원한다면 `--all-displays`
```
./ChangeMenuBarColor SolidColor "desired_hex_color" --all-displays
```

### 그라데이션 색상으로 변경
배경사진 경로는 입력하지 않아도 적용 된다.
```
./ChangeMenuBarColor Gradient "start_hex_color" "end_hex_color" "optional_path_to_your_wallpaper"
```