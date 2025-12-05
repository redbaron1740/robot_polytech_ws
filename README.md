1. 새로운 pip pkg를 requirements.txt 파일을 생성

아래 명령어로 한 번에 필요한 pip 패키지를 설치 가능

    pip install -r requirements.txt 
   

2. ROS PKG 컴파일
아래 경로로 이동하여, ros 컴파일
    cd robot_polytech_ws 
   

    colcon build 
   

    ls -al 
   
3. 
4. 
   


* build log install = 3가지가 생성이 되었는지 확인, 있다면


    rm -rf build/ install/ log/ 
   
   

3. PEAK-CAN USB 장비의 드라이버 설치...
  3.1 준비 사항
>
sudo apt update && sudo apt upgrade -y
>
sudo apt-get install libpopt-dev libelf-dev

  3.2 Download pcan for linux driver 및 압출 해체

  Download link : https://www.peak-system.com/fileadmin/media/linux/index.php
  
  예) peak-linux-driver-X.Y.Z.tar.gz

    tar -xvf peak-linux-driver-X.Y.Z.tar.gz 
   
    cd peak-linux-driver-X.Y.Z 


  3.3 드라이버 컴파일 및 설치
 >
sudo make clean
 
 >
sudo make NET=NETDEV_SUPPORT 
  
 >
sudo make install

  3.4 커널 모듈 로드
 >
sudo modprobe pcan

  3.5 드라이버 설치 확인
 > 
 
    pcaninfo 
    
 >

    cat /proc/pcan


4. 등록된 PCAN bring up
  4.1 ip link 로 등록 상황 파악
>
ip link
>
> or
>
dmesg | grep can
>

can0, can1 확인

  4.2 can0, can1이 이미 할당되어 있다면,
>
sudo ip link set can2 down
>
sudo ip link set can2 up type can bitrate 500000
>
candump can2

  4.3 할당되어 있지 않다면,
>
sudo ip link set can0 down
>
sudo ip link set can0 up type can bitrate 500000
>
candump can0
 

  
