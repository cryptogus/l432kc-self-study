![image](https://github.com/user-attachments/assets/0515898d-8d2f-45af-90bb-800e99cb1f10)# 보드 위의 LED 깜빡거리기

Windows 11 환경  
STM32 IDE 이용
![image](https://github.com/user-attachments/assets/45181d18-eeb4-49c8-93a5-10850fd99712)

`Create a New STM32 project`선택

![image](https://github.com/user-attachments/assets/4c130f24-a047-4042-adf7-1304a26409f3)
보드의 MCU선택. 나는 MCU(칩)만 구매한게 아니라 board에 MCU가 붙어있는 걸 구매했기에 제일 위에거 선택. 확인을 위해 물결 밑출 친 보드 링크 확인
![image](https://github.com/user-attachments/assets/e6ad4841-12db-4098-a92e-ee6baf77d61d)
확인 결과: 맞음, NEXT 버튼 누르기
![image](https://github.com/user-attachments/assets/cd586557-0cc0-4c96-8cf4-d136920373f9)
프로젝트 이름 정하고 생성하기. `LED`로 했음, empty라는 옵션을 설정하면 기본적인 보드에 대한 세팅 관련 파일들만 생성됨.

![image](https://github.com/user-attachments/assets/057993ca-58f8-469c-888e-775f92ce8d3b)
`.ld` 파일: 링커라고 memory map 등에 관한 정보가 세팅되어있음. 본인이 보드에 대해 잘 안다면 RAM과 FLASH의 메모리 크기나 주소같은 설정을 바꿀수도 있을 것이다. 일반적으로 linux pc상에서 ld라는 링커가 있는거랑 보드의 링커랑은 살짝 다를 수 있음.  

![image](https://github.com/user-attachments/assets/f47c6fba-6619-4c9a-a8a3-9ba8f5eb20c7)
`.s` 파일: 일반적으로는 어셈블리 파일이지만, 보통 이런 보드에서는 부팅시 처음 시작되는 파일로, c언어의 main함수보다 먼저 시작해서 클락 등의 기초적인 부팅 작업을 해주는 역할을 함.

