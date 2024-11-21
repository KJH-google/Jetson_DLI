## NVIDIA_jetson_DLI
=========================
# 1. jetson-nano-jpg 이미지 다운로드
# 2. SD card format
<img width="413" alt="1_SD카드 format" src="https://github.com/user-attachments/assets/e296ff5f-4bde-4fb5-ae36-1d81e5aab3b0">

# 3. balenaEtcher로 이미지 굽기

<img width="62" alt="4" src="https://github.com/user-attachments/assets/455a255d-3192-4d2d-a368-cb514a6b31c4">
<img width="596" alt="2_" src="https://github.com/user-attachments/assets/bf5eadf3-d53c-4796-9317-5d2358483db3">

<img width="593" alt="3" src="https://github.com/user-attachments/assets/5346d442-da67-4a86-9918-29a99c6f62ef">

> 파일 업로드시 압축해제 후 사용

# 4. NVDIA_jetson_DLI 환경설정
> 초기 언어: Englsih로 설정
> 와아파이 연결: aifrenz
> Seoul 설정
> dli로 유저 만들기
> 계속 진행하여 마무리

> 한글 패치 설치
> sudo apt-get update
> dli@dli-desktop:~$ sudo apt-get install fcitx-hangul
> dli@dli-desktop:~$ im-config -n fcitx —> reboot
> 자세한 것은 https://driz2le.tistory.com/253 참조


# 5. 젯봇 완성하기
> jetson nano에 연결 => 구운 SD카드, HDMI선(모니터와 연결), 쿨링팬, 와이파이 연결잭, 키보드, 마우스
> POWER -> 5volt 규격 이용 반드시!!!

# 6. 파이썬 설치
> 4.2.12 버젼

# 7. CSI(USB) 카메라 설치



우리에게 맞는 코드
git clone  https://github.com/JetsonHacksNano/CSI-Camera.git
dli@dli-desktop:~/CSI-Camera$ ls
dli@dli-desktop:~/CSI-Camera$ python3 simple_camera.py 



![카메라 오픈](https://github.com/user-attachments/assets/67d7c064-61fc-4f2b-8c32-6d23a553b23a)

![Screenshot from 2024-11-14 21-03-09](https://github.com/user-attachments/assets/3e56c144-e4bc-48ad-9642-7a16b3847787)

![Screenshot from 2024-11-14 21-27-46](https://github.com/user-attachments/assets/19d97c5a-f5a9-4220-a73b-1e375fba33b4)


# 8. Docker 설치
> 교육과정에 필요한 dir 추가
> docker 다운로드
sudo docker run --runtime nvidia -it --rm --network host \
    --memory=500M --memory-swap=4G \
    --volume ~/nvdli-data:/nvdli-nano/data \
    --volume /tmp/argus_socket:/tmp/argus_socket \
    --device /dev/video0 \
    nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1kr
> 메모리 부족을 해결하기 위한 SWAP 18GB 설치

![Screenshot from 2024-11-21 20-32-30](https://github.com/user-attachments/assets/82804b63-9f26-422f-baee-c569153e3954)

# 9. Docker를 통한 classification Juypter 이용
> CSI Camera 오류로 USB Camera로 변경
> 엄지 위 / 아래 각각 30개씩 train 데이터 카메라로 찍기
> 결과는 밑의 사진

![Screenshot from 2024-11-21 20-32-30](https://github.com/user-attachments/assets/d24dac0c-16c7-4ef7-a803-692feb295316)

![Screenshot from 2024-11-21 20-59-13](https://github.com/user-attachments/assets/7067c297-37dc-4737-935c-09c040500716)



