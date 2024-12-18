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
* 이미지팩 다운로드
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
> <img src="https://github.com/user-attachments/assets/daea19ed-be57-46dc-bcc9-6b49600c08a7" alt="image" width="47%">  
> <img src="https://github.com/user-attachments/assets/dae7e18b-ee01-4941-bdc8-857479c5e38c" alt="image" width="47%">
* 아두이노(더스트 센서)를 젯봇에 연결하여 조립
> <img src="https://github.com/user-attachments/assets/9cce4dca-f054-43bf-a0af-6e85105b622f" alt="390825388-368cd62d-57e3-476b-a5c4-3dcbbcd1913f" width="80%">





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


3-1_arduino_code_실습(PM2.5 dust sensor)
====================
## 0. 준비 단계
### 0.1. Jetson nano에 파이썬 3.8 설치하기

1.update & upgrade
<pre>
<code>
sudo apt update
sudo apt upgrade
</code>
</pre>
2. 필요한 패키지 설치
<pre>
<code>
sudo apt install build-essential libssl-dev zlib1g-dev libncurses5-dev libncursesw5-dev libreadline-dev 
libsqlite3-dev libgdbm-dev libdb5.3-dev libbz2-dev libexpat1-dev liblzma-dev libffi-dev libc6-dev
</code>
</pre>
3. python3.8 소스코드 받기
<pre>
<code>
cd /
sudo wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tar.xz
</code>
</pre>
4. 압축 풀기
<pre>
<code>
sudo tar -xf Python-3.8.12.tar.xz
cd Python-3.8.12
</code>
</pre>
5. Build
<pre>
<code>
./configure --enable-optimizations
make -j4
</code>
</pre>
6. 마무리
<pre>
<code>
sudo make altinstall
python3.8 --version
</code>
</pre>
7. 가상환경 (중요!!)
<pre>
<code>
python3.8 -m venv myenv                                     
source myenv/bin/activate
</code>
</pre>
>
<pre>
<code>
pip install —trusted-host pypi.org —trusted-host
files.pythonhosted.org pip setuptools
</code>
</pre>

<img src="https://github.com/user-attachments/assets/a3ccebf4-b803-4867-ac58-9d69a208dc82" width="30%" />
<img src="https://github.com/user-attachments/assets/26b1c21e-20ae-406d-9a08-69a20982fff6" width="30%" />
<img src="https://github.com/user-attachments/assets/46911449-f62a-4a53-912b-a141c13b0f5b" width="30%" />

***

### 0.2. Jetson nano에 jupyter notebook 설치하기

* 앞으로 python3.8 사용할때는 아래 코드를 사용해서 가상환경으로 들어간다. 가상환경 이름: myenv
<pre>
<code>
source myenv/bin/activate
</code>
</pre>
* jupyter notebook 설치
<pre>
<code>
pip install jupyter
</code>
</pre>

<pre>
<code>
pip install openai
</code>
</pre>

<pre>
<code>
Pip install gradio
</code>
</pre>

* jupyter notebook 실행
<pre>
<code>
jupyter notebook
</code>
</pre>
<img src="https://github.com/user-attachments/assets/3fdc497f-537b-4982-8255-538bbfee75af" width="70%" />

***

### 0.3. Jetson GPIO
1. 가상환경에서 Jetson.GPIO 깔려있는지 확인 -> 숫자가 나와야함 -> 깔려있다면 다음 단계 안해도 됨
<pre>
<code>
source myenv/bin/activate
python3 -c "import Jetson.GPIO as GPIO; print(GPIO.VERSION)"
Deactivate
</code>
</pre>
2. 가상환경 비활성화하고 아래 코드 실행해서 깔려있는지 확인 -> 깔려있다면 다음단계 X
<pre>
<code>
python3 -c "import Jetson.GPIO as GPIO; print(GPIO.VERSION)"
</code>
</pre>
3. 가상환경 비활성화에서도 안깔려있으면 코드 실행 / 깔려있으면 실행 안해도 됨
<pre>
<code>
sudo apt-get update
sudo apt-get install python3-jetson-gpio
</code>
</pre>
4. 가상환경에서만 안되는거면? 아래 코드 실행 -> 다시 1번단계 실행해보기
<pre>
<code>
cp -r /usr/lib/python3/dist-packages/Jetson /home/dli/myenv/lib/python3.8/site-packages/
cp -r /usr/lib/python3/dist-packages/Jetson.GPIO-2.0.17.egg-info /home/dli/myenv/lib/python3.8/site-packages/
</code>
</pre>
<img src="https://github.com/user-attachments/assets/9d17d306-dffd-4aa1-b8c3-772a1507a7c3" width="40%" />
<img src="https://github.com/user-attachments/assets/39e0722c-212d-4479-bc49-b97ddfd1575e" width="40%" />

***

### 0.4. 아두이노
* 기존 아두이노 삭제
>
    sudo apt remove —purge arduino
    sudo apt autoremove
>
* 1.8.19 버전으로 다운로드: <https://www.arduino.cc/en/software>
* arduino-1.8.19라는 폴더에 압축해제
>
    cd Downloads
    tar -xf arduino-1.8.19-linuxaarch64.tar.xz
>
    cd arduino-1.8.19
    sudo ./install.sh
    sudo usermod -aG dialout $USER
    newgrp dialout
>
    arduino
<img src="https://github.com/user-attachments/assets/40500c61-2513-48a5-a653-2d17640da353" width="50%" />

***
## 1. 미세먼지 읽어오는 코드

    import Jetson.GPIO as GPIO
    import time
    import math

    def measure_pm25():
        """
        PM2.5 농도를 측정하여 반환하는 함수.

        Args:
            pin (int): 측정에 사용할 GPIO 핀 번호 (BCM 핀 기준).
            sample_time_ms (int): 샘플링 시간 (밀리초 단위).

        Returns:
            float: PM2.5 농도 (ug/m3).
        """

        pin = 8
        sample_time_ms=30000
        # GPIO 초기화
        GPIO.setmode(GPIO.BCM)
        GPIO.setup(pin, GPIO.IN)

        low_pulse_occupancy = 0
        start_time = time.time()

        try:
            # 샘플링 시간 동안 LOW 신호 지속 시간 측정
            while (time.time() - start_time) * 1000 <= sample_time_ms:
                pulse_start = time.time()
                while GPIO.input(pin) == GPIO.LOW:
                    pass
                pulse_end = time.time()

                # LOW 상태 지속 시간 계산
                pulse_duration = (pulse_end - pulse_start) * 1e6  # 마이크로초 단위로 변환
                low_pulse_occupancy += pulse_duration

            # PM2.5 농도 계산
            ratio = low_pulse_occupancy / (sample_time_ms * 10.0)
            concentration = (
                1.1 * math.pow(ratio, 3) - 3.8 * math.pow(ratio, 2) + 520 * ratio + 0.62
            )
            return str(round(concentration,2))

        except Exception as e:
            print(f"Error during measurement: {e}")
            return None

        finally:
            GPIO.cleanup()

    # 예시: 함수 호출
    if __name__ == "__main__":
        pm25_concentration = measure_pm25()
        if pm25_concentration is not None:
            print(f"Measured PM2.5 Concentration: {pm25_concentration:} ug/m3")
        else:
            print("Measurement failed.")
***
> <결과값>
Measured PM2.5 Concentration: 927746.07 ug/m3

## 2. 함수정의
<pre>
<code>
use_functions = [
    {
        "type": "function",
        "function": {
            "name": "measure_pm25",
            "description": "Reads and calculatses the fine dust (PM2.5 and PM10) concentration from the given sensor data"

        }
    }
]
</code>
</pre>
***
## 3. Chat completions
<pre>
<code>
import os
from openai import OpenAI
import json

os.environ['OPENAI_API_KEY'] = 
</code>
</pre>

## 4. Gradio로 GUI 구성하기
<pre>
<code>
def ask_openai(llm_model, messages, user_message, functions = ''):
    client = OpenAI()
    proc_messages = messages

    if user_message != '':
        proc_messages.append({"role": "user", "content": user_message})

    if functions == '':
        response = client.chat.completions.create(model=llm_model, messages=proc_messages, temperature = 1.0)
    else:
        response = client.chat.completions.create(model=llm_model, messages=proc_messages, tools=functions, tool_choice="auto") # 이전 코드와 바뀐 부분

    response_message = response.choices[0].message
    tool_calls = response_message.tool_calls

    if tool_calls:
        # Step 3: call the function
        # Note: the JSON response may not always be valid; be sure to handle errors

        available_functions = {
            "measure_pm25": measure_pm25
        }

        messages.append(response_message)  # extend conversation with assistant's reply

        # Step 4: send the info for each function call and function response to GPT
        for tool_call in tool_calls:
            function_name = tool_call.function.name
            function_to_call = available_functions[function_name]
            function_args = json.loads(tool_call.function.arguments)


            print(function_args)

            if 'user_prompt' in function_args:
                function_response = function_to_call(function_args.get('user_prompt'))
            else:
                function_response = function_to_call(**function_args)

            proc_messages.append(
                {
                    "tool_call_id": tool_call.id,
                    "role": "tool",
                    "name": function_name,
                    "content": function_response,
                }
            )  # extend conversation with function response
        second_response = client.chat.completions.create(
            model=llm_model,
            messages=messages,
        )  # get a new response from GPT where it can see the function response

        assistant_message = second_response.choices[0].message.content
    else:
        assistant_message = response_message.content

    text = assistant_message.replace('\n', ' ').replace(' .', '.').strip()


    proc_messages.append({"role": "assistant", "content": assistant_message})

    return proc_messages, text
</code>
</pre>

<pre>
<code>
import gradio as gr
import random


messages = []

def process(user_message, chat_history):

    # def ask_openai(llm_model, messages, user_message, functions = ''):
    proc_messages, ai_message = ask_openai("gpt-4o-mini", messages, user_message, functions= use_functions)

    chat_history.append((user_message, ai_message))
    return "", chat_history

with gr.Blocks() as demo:
    chatbot = gr.Chatbot(label="채팅창")
    user_textbox = gr.Textbox(label="입력")
    user_textbox.submit(process, [user_textbox, chatbot], [user_textbox, chatbot])



