# ubuntu 20.04 setting

### Environments
- ubuntu 20.04
- RTX 3070ti
- Nvidia-driver-470
- [CUDA 11.2](https://developer.nvidia.com/cuda-11.2.0-download-archive)
- [cuDNN 8.1.1](https://developer.nvidia.com/cudnn)

## 그래픽 드라이버 설치
- 그래픽카드에 맞는 드라이버 확인
```
ubuntu-drivers devices
```
- nvidia driver 설치
```
sudo apt install nvidia-driver-470
```

## CUDA 설치
- CUDA 11.2 설치
```
wget https://developer.download.nvidia.com/compute/cuda/11.2.2/local_installers/cuda_11.2.2_460.32.03_linux.run
sudo sh cuda_11.2.2_460.32.03_linux.run
```
- Driver 체크 해제 후 설치
- .bashrc 수정
```
sudo gedit ~/.bashrc
```
```
export PATH=/usr/local/cuda-11.2/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
```
source ~/.bashrc
```
- cuda 설치 확인
```
nvcc --version
```

## cuDNN 설치
- [cuDNN 8.1.1](https://developer.nvidia.com/cudnn) 다운
- 압축해제
```
tar –xzvf cudnn-11.2-linux-x64-v8.1.1.33.tgz
```
- 설치
```
sudo cp cuda/include/cudnn*.h /usr/local/cuda/include
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
```
- 설치 확인
```
cat /usr/local/cuda/include/cudnn_version.h | grep CUDNN_MAJOR -A 2
ldconfig -N -v $(sed 's/:/ /' <<< $LD_LIBRARY_PATH) 2>/dev/null | grep libcudnn
```

## matplotlib 한글 폰트 설정
- 나눔 폰트 설치
```
sudo apt-get install fonts-nanum*
```
- 폰트 업데이트
```
fc-cache -fv
```
- matplotlib 패키지 안에 폰트 복사 (아나콘다 환경을 이용하여 아나콘다 경로 설정)
```
cp /usr/share/fonts/truetype/nanum/Nanum* /anaconda3/envs/환경명/lib/python3.7/site-packages/matplotlib/mpl-data/fonts/ttf/
```
- matplotlib 사용 예시
```
font_name = fm.FontProperties(fname="/usr/share/fonts/truetype/nanum/NanumGothic.ttf").get_name()
```