NVIDIA_jetson_DLI
=================

## 1. jetson-nano-jpg 이미지 다운로드
> <img src="https://github.com/user-attachments/assets/56405bb4-c359-42ad-8da5-c0237e6be9f7" alt="이미지" width="60%"/>
> <img src="https://github.com/user-attachments/assets/68da29f6-f73b-4301-ae2b-5adb6dd27b81" alt="image" width="70%">

> 이미지 다운로드하여 준비하기
***
## 2. SD card format
> <img src="https://github.com/user-attachments/assets/3a1c3246-0f2d-4f49-8b32-a44827477ee4" alt="image" width="35%">      
>
> <img width="35%" alt="1_SD카드 format" src="https://github.com/user-attachments/assets/e296ff5f-4bde-4fb5-ae36-1d81e5aab3b0">
>
> <img src="https://github.com/user-attachments/assets/6836aa3c-17a8-4a18-8cfb-7f37bf5ff971" alt="image" width="25%">
* 오른쪽 컴퓨터 데스크탑에 sd카드 넣기
* SD Card Formatter로 포맷하기
***
## 3. balenaEtcher로 이미지 굽기

> <img width="62" alt="4" src="https://github.com/user-attachments/assets/455a255d-3192-4d2d-a368-cb514a6b31c4">   
* 프로그램 다운로드   
> <img width="40%" alt="2_" src="https://github.com/user-attachments/assets/bf5eadf3-d53c-4796-9317-5d2358483db3">   
> <img width="40%" alt="3" src="https://github.com/user-attachments/assets/5346d442-da67-4a86-9918-29a99c6f62ef">   


>*파일 업로드시 압축해제 후 사용   
* uSD 에 Jetpack 4.6 이미지 굽기
* flash 한 후 verifying 까지 마친 마이크로 SD카드 준비 완료

***
## 4. NVDIA_jetson_DLI 환경설정

* 젯봇에 마이크로 SD카드 넣기
* HDML 선으로 컴퓨터와 연결하여 환경설정   
> <img src="https://github.com/user-attachments/assets/f7850586-6f2c-4735-9889-021b51ed8f26" alt="image" width="60%">
* 초기 언어: Englsih로 설정
* 와아파이 연결: aifrenz
* Seoul 설정
* dli로 유저 만들기 (name과 password 모두 dli로 설정)
* 계속 진행하여 마무리
> <img src="https://github.com/user-attachments/assets/166d3870-7fd8-47c3-8d9f-648b2a5f23f7" alt="image" width="60%">
* 싱글보드 컴퓨터 설정 완료

    * <한글 패치 설치하기>
>     
    sudo apt-get update
    dli@dli-desktop:~$ sudo apt-get install fcitx-hangul
    dli@dli-desktop:~$ im-config -n fcitx —> reboot
>
> 자세한 것은 <https://driz2le.tistory.com/253> 참조하여 진행

***
## 5. 젯봇 완성하기
* jetson nano에 연결 => 구운 SD카드, HDMI선(모니터와 연결), 쿨링팬, 와이파이 연결잭, 키보드, 마우스
* POWER -> 5volt 규격 이용 반드시!!!
***
## 6. 파이썬 설치
    dli@dli-desktop:~$ sudo apt install python3-pip
    do you want to continue ? Y
    dli@dli-desktop:~$  sudo -H pip3 install -U jetson-stats
> 
> 4.2.12 버젼으로 설치
>
***
## 7. jtop Nano 통해 정보 확인
> <img src="https://github.com/user-attachments/assets/95a18ec8-d50d-4318-9874-8b5983f87eec" alt="image" width="50%">
>    
    dli@dli-desktop:~$ reboot   
    dli@dli-desktop:~$ jtop
***
## 8. CSI(USB) 카메라 설치

    dli@dli-desktop:~$  ls /dev/vi*
>
    git clone  https://github.com/JetsonHacksNano/CSI-Camera.git
    dli@dli-desktop:~/CSI-Camera$ ls
    dli@dli-desktop:~/CSI-Camera$ python3 simple_camera.py   
* 우리에게 맞는 코드 




> <img src="https://github.com/user-attachments/assets/67d7c064-61fc-4f2b-8c32-6d23a553b23a" alt="카메라 오픈" width="80%">
* 카메라 오픈
> <img src="https://github.com/user-attachments/assets/3e56c144-e4bc-48ad-9642-7a16b3847787" alt="Screenshot from 2024-11-14 21-03-09" width="80%">
* 얼굴 정상 인식
> <img src="https://github.com/user-attachments/assets/19d97c5a-f5a9-4220-a73b-1e375fba33b4" alt="Screenshot from 2024-11-14 21-27-46" width="80%">
* 이ㅣ
***
## 9. Docker 설치
* 교육과정에 필요한 dir 추가   
* docker 다운로드
>  
    sudo docker run --runtime nvidia -it --rm --network host \
        --memory=500M --memory-swap=4G \
        --volume ~/nvdli-data:/nvdli-nano/data \
        --volume /tmp/argus_socket:/tmp/argus_socket \
        --device /dev/video0 \
        nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1kr
>
* 메모리 부족을 해결하기 위한 SWAP 18GB 설치

> <img src="https://github.com/user-attachments/assets/82804b63-9f26-422f-baee-c569153e3954" alt="Screenshot from 2024-11-21 20-32-30" width="80%">

***
## 10. Docker를 통한 classification Juypter 이용
* CSI Camera 오류로 USB Camera로 변경
* 엄지 위 / 아래 각각 30개씩 train 데이터 카메라로 찍기
> 결과는 밑의 사진

> <img src="https://github.com/user-attachments/assets/d24dac0c-16c7-4ef7-a803-692feb295316" alt="Screenshot from 2024-11-21 20-32-30" width="80%">

> <img src="https://github.com/user-attachments/assets/7067c297-37dc-4737-935c-09c040500716" alt="Screenshot from 2024-11-21 20-59-13" width="80%">

***

## 11. Arduino 설치
* Arduino 홈페이지에서 다운로드 패키지 받기
>
    sudo apt-get update
    sudo apt-get install arduino
    arduino
>
> <img src="https://github.com/user-attachments/assets/9e2a6a8a-df2c-4629-b5fa-2d9b8f6b4544" alt="Screenshot from 2024-11-21 21-50-47" width="80%">
***
## 12. Arduino basic, blink 활용
> <img src="https://github.com/user-attachments/assets/5ca8fa9a-dff6-42ee-81b0-d7a4a152f586" alt="Screenshot from 2024-11-28 20-39-39" width="80%">
***
## 13. Arduino grove dust sensor 활용
> <img src="https://github.com/user-attachments/assets/daea19ed-be57-46dc-bcc9-6b49600c08a7" alt="image" width="50%">  
> <img src="https://github.com/user-attachments/assets/dae7e18b-ee01-4941-bdc8-857479c5e38c" alt="image" width="50%">
> <img src="https://github.com/user-attachments/assets/9cce4dca-f054-43bf-a0af-6e85105b622f" alt="390825388-368cd62d-57e3-476b-a5c4-3dcbbcd1913f" width="50%">





    int pin = 8;
    unsigned long duration;
    unsigned long starttime;
    unsigned long sampletime_ms = 30000;//sampe 30s ;
    unsigned long lowpulseoccupancy = 0;
    float ratio = 0;
    float concentration = 0;
     
    void setup() 
    {
        Serial.begin(9600);
        pinMode(pin,INPUT);
        starttime = millis();//get the current time;
    }
    
    void loop() 
    {
        duration = pulseIn(pin, LOW);
        lowpulseoccupancy = lowpulseoccupancy+duration;
    
        if ((millis()-starttime) > sampletime_ms)//if the sampel time == 30s
        {
            ratio = lowpulseoccupancy/(sampletime_ms*10.0);  // Integer percentage 0=>100
            concentration = 1.1*pow(ratio,3)-3.8*pow(ratio,2)+520*ratio+0.62; // using spec sheet curve
            Serial.print(lowpulseoccupancy);
            Serial.print(",");
            Serial.print(ratio);
            Serial.print(",");
            Serial.println(concentration);
            lowpulseoccupancy = 0;
            starttime = millis();
        }
    }

>


    int pin = 8;
    unsigned long duration;
    unsigned long starttime;
    unsigned long sampletime_ms = 30000;  // 30초 동안 샘플링
    unsigned long lowpulseoccupancy = 0;
    float ratio = 0;
    float concentration = 0;
    
    void setup()
    {
        Serial.begin(9600);
        pinMode(pin, INPUT);
        starttime = millis();
        Serial.println("미세먼지 측정을 시작합니다...");
        Serial.println("==============================");
    }
    
    void loop()
    {
        duration = pulseIn(pin, LOW);
        lowpulseoccupancy = lowpulseoccupancy + duration;
    
        if ((millis()-starttime) > sampletime_ms)  // 30초마다 측정
        {
            ratio = lowpulseoccupancy/(sampletime_ms*10.0);
            concentration = 1.1*pow(ratio,3)-3.8*pow(ratio,2)+520*ratio+0.62; // ug/m3 단위
    
            Serial.println("==============================");
            Serial.print("미세먼지 농도: ");
            Serial.print(concentration);
            Serial.println(" ug/m3");
    
            // 대기질 상태 표시
            Serial.print("대기질 상태: ");
            if(concentration <= 30) {
                Serial.println("좋음");
            }
            else if(concentration <= 80) {
                Serial.println("보통");
            }
            else if(concentration <= 150) {
                Serial.println("나쁨");
            }
            else {
                Serial.println("매우 나쁨");
            }
    
            Serial.println("------------------------------");
            Serial.print("측정 시간: ");
            Serial.print(millis()/1000);
            Serial.println("초");
            Serial.println("==============================\n");
    
            // 다음 측정을 위한 초기화
            lowpulseoccupancy = 0;
            starttime = millis();
        }
    }


>


    int pin = 8;
    unsigned long duration;
    unsigned long starttime;
    unsigned long sampletime_ms = 30000;  // 30초 동안 샘플링
    unsigned long lowpulseoccupancy = 0;
    float ratio = 0;
    float concentration = 0;
    
    void setup()
    {
        Serial.begin(9600);
        pinMode(pin, INPUT);
        starttime = millis();
        Serial.println("Start checking dust...");
        Serial.println("==============================");
    }
    
    void loop()
    {
        duration = pulseIn(pin, LOW);
        lowpulseoccupancy = lowpulseoccupancy + duration;
    
        if ((millis()-starttime) > sampletime_ms)  // 30초마다 측정
        {
            ratio = lowpulseoccupancy/(sampletime_ms*10.0);
            concentration = 1.1*pow(ratio,3)-3.8*pow(ratio,2)+520*ratio+0.62; // ug/m3 단위
            
            concentration = concentration * 0.2;
    
            Serial.println("==============================");
            Serial.print("Dust conc: ");
            Serial.print(concentration);
            Serial.println(" ug/m3");
    
            // 대기질 상태 표시
            Serial.print("Air condition: ");
            if(concentration <= 30) {
                Serial.println("Good");
            }
            else if(concentration <= 80) {
                Serial.println("Normal");
            }
            else if(concentration <= 150) {
                Serial.println("Bad");
            }
            else {
                Serial.println("Worst");
            }
    
            Serial.println("------------------------------");
            Serial.print("check time: ");
            Serial.print(millis()/1000);
            Serial.println("second");
            Serial.println("==============================\n");
    
            // 다음 측정을 위한 초기화
            lowpulseoccupancy = 0;
            starttime = millis();
        }
    }

