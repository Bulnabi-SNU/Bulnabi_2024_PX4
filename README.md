# Bulnabi_2024_PX4
본 repository는 불나비의 2024 한국로봇항공기대회 PX4 개발을 위해 제작되었으며, PX4-AutoPilot의 v1.14.3 버전을 그대로 가져온 것이다. 대회의 소프트웨어 개발에 참여하는 모든 인원은 PX4_Autopilot을 해당 repository로 다시 변경해야 한다.
**Reference**: [PX4_Autopilot github v1.14.3](https://github.com/PX4/PX4-Autopilot/tree/v1.14.3)
#### 개발 환경
> 1. Ubuntu 20.04
> 2. ROS2 foxy

## Installation
1. 현재 repository를 fork 버튼을 통해 본인 계정으로 fork
2. fork한 본인의 repository에서 본인의 local computer로 clone
    ``` shell
    git clone [your_repository_url]
    # git clone https://github.com/okj001010/Bulnabi_2024_PX4.git
    ```
3. Bulnabi_2024_PX4 폴더로 이동해서 Bulnabi-SNU/Bulnabi_2024_PX4를 upstream으로 추가
    ``` shell
    git remote add upstream https://github.com/Bulnabi-SNU/Bulnabi_2024_PX4.git
    ```
4. Bulnabi_2024_PX4가 upstream으로 잘 등록되었다면, ```git remote -v```를 실행하면 다음과 같이 출력됨
    ```
    origin	https://github.com/okj001010/Bulnabi_2024_PX4.git (fetch)
    origin	https://github.com/okj001010/Bulnabi_2024_PX4.git (push)
    upstream	https://github.com/Bulnabi-SNU/Bulnabi_2024_PX4.git (fetch)
    upstream	https://github.com/Bulnabi-SNU/Bulnabi_2024_PX4.git (push)
    ```
5. upstream에서 tag를 받음
    ``` shell
    git fetch --tags upstream
    ```
6. submodule을 update (오래 걸림)
    ``` shell
    make submodulesclean
    ```
7. 다음 명령어 실행
    ``` shell
    bash ./Tools/setup/ubuntu.sh
    ```
    완료가 되면 ubuntu를 로그아웃했다가 다시 접속

8. 다시 Bulnabi_2024_PX4 폴더로 들어와서 다음 명령어 실행 (매우 오래 걸림)
    ``` shell
    make px4_sitl gazebo-classic
    ```

## Development (Optional)

(**주의** : PX4 version이 맞지 않을 시 나중에 어떤 문제가 발생할지 모르기 때문에 가능하면 해당 repo를 수정하지 않는 것이 좋으며, 최소한의 소프트웨어팀 인원만 수정하는 편이 좋다.)

1. 아래의 명령어를 실행해, 모든 test를 통과하는지 확인 (오래 걸림)
    ``` shell
    make tests
    ```
    ```
    100% tests passed, 0 tests failed out of 139
    ```
2. 수정 사항을 본인 계정의 repository에 push
    ```
    git add . # or git add [file name]
    git commit -m "[YOUR_COMMIT_MESSAGE]" # Clear, concise and informative commit message
    git push origin v1.14.3_bulnabi
    ```
3. Pull request 버튼을 클릭하고 reviewer를 지정해서 올림
4. 추후에 reviewer가 확인하고 merge 버튼을 누르면 본인의 수정사항이 Bulnabi-SNU/Bulnabi_2024_PX4에 merge됨

## How to upload PX4 onto Pixhawk
위의 과정을 따라 Bulnabi_2024_PX4를 설치했다면, 그것을 Pixhawk 위에 올린 뒤에 본인들의 작업물(Companion computer 활용한 부분 포함)과 충돌이 일어나지는 않는지 확인해야 한다.

기존에는 QGround Control을 연결한 뒤, Vehicle Setting -> Firmware에 들어간 뒤, USB를 뺐다가 다시 끼면 Stable한 px4 버전이 자동으로 픽스호크 보드에 업로드가 되었다. 그러나 이제는, Bulnabi_2024_PX4를 사용할 것이기 때문에 위 방법 대신 아래와 같은 방법을 사용한다.


Bulnabi_2024_PX4 폴더에서 픽스호크 보드 제품 버전에 맞는 명령어를 실행한다. https://docs.px4.io/main/en/dev_setup/building_px4.html
``` shell
make px4_fmu-v6x_default
```
build가 완료되면, 다음 명령어를 통해 upload를 진행한다.
``` shell
make px4_fmu-v6x_default upload
```
그럼 bootloader 어쩌고라는 말이 뜰 텐데, 그 다음 usb를 뺐다가 끼면 기체에 우리의 Bulnabi_2024_PX4 펌웨어가 업로드되게 된다.
그 이후는 기존에 QGroundControl 사용 방법과 동일하다. (펌웨어는 이미 업로드했으므로, 그 부분을 제외하고)
