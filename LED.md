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

일단 보드를 연결하고 `main.c`에 간단하게 아래와 같이 코드를 작성해보았다.
```c
/* Loop forever */
for(;;) {
	int x = 1;
	int y = 2;
	int z = x + y;
}
```
![image](https://github.com/user-attachments/assets/169c5ee3-9d6a-4751-a114-d0950d1e784f)

디버그 먼저 해보겠다. 벌래 모양 버튼 누른다.  

![image](https://github.com/user-attachments/assets/578ec07d-56bb-40b4-951b-4e44ea9da092)
`.elf` 파일이 보이는데, 애는 보통 linux 환경에서의 목적파일 같은 녀석이다. 근데 여기서는 디버깅 정보를 가진 보드에 올라갈 실행파일이라고 생각하면 된다. 컴파일 할때 Debug, Release 둘 중 하나를 선택하게 되는데 `.elf` 는 Debug모드로 컴파일 했을때의 결과물인 것이다. 그래서 잘 보면 `Debug`라는 디렉터리 밑에 `.elf` 파일이 생긴다.

![image](https://github.com/user-attachments/assets/02ae9d99-0a97-4ccc-85d6-7d3f96f78cc2)

디버그 설정 창이 뜬다. JATG, SWD, ST-LINK, J-LINK.. 참 많이도 뜬다. 경험해보지 않으면 모를 것들이다.

![image](https://github.com/user-attachments/assets/982fa338-c8d3-404b-a9a5-72a6a49bdf02)

위의 설정들은 아래부분에서 다시 수정이 가능하다.

![image](https://github.com/user-attachments/assets/5b6a8061-c46a-490d-b351-678b35faea0b)

그리고 이런 경고창? 이 뜨는데

![image](https://github.com/user-attachments/assets/d08a6f3a-b4b2-4226-af7c-b51fc17b690b)

이건 그냥 디버그 관점으로 전환하면 디버깅에 필요한 도구들이 더 잘 보이도록 IDE의 레이아웃이 바뀌는데 바꿀거냐는 거다. 나는 그냥 yes 눌렀다.

![image](https://github.com/user-attachments/assets/fe9b7edf-cfe8-4fef-afc6-f7e8bf757fb1)

위 사진은 디버깅이 잘 되는 모습이다. 값이 잘 들어가고 있다. 이게 지금 무슨 상황이냐면, 위에 main.c에 작성한 코드를 컴파일 했고, 이를 (MCU 대신 그냥 편하게 보드라고 부르겠다) 보드에서 실행가능한 파일로 컴파일 되고, 그 실행파일 `.elf` 나 `.hex` 파일이 IDE에 연결된 ST-LINK에 의해 (정확히는 programmer)해당 보드에 올라간다(보드에 다운로드 된다).
