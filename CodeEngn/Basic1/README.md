<img width="614" alt="image" src="https://github.com/user-attachments/assets/e4d65336-cc28-4c7b-bcbd-2e293ea2c4cb">
- 오늘은 CodeEngn의 Basic1 문제를 풀어보도록 하겠다.

<img width="599" alt="image" src="https://github.com/user-attachments/assets/6eb5848f-5e25-4b0b-82f1-9705c3e590cd">
- 파일을 압축해제하면 .exe 파일이 하나 존재하는 것을 알 수 있다.
- Detect It Easy를 이용해서 파일이 패킹되어 있는지 확인해보면, 패킹은 되어 있지 않고, 32비트이며, Delpi 언어로 제작되었음을 알 수 있다.

- 01.exe 파일을 실행하면, <img width="173" alt="image" src="https://github.com/user-attachments/assets/c60c2e87-6ec2-47fd-b93a-f1e4526fcb5d">
<img width="153" alt="image" src="https://github.com/user-attachments/assets/a2e5d783-1bc5-4495-a2d8-20ab46af449a">

- 해당 Alert가 뜨게 된다.
- 즉, 문제의 내용처럼 HDD를 CD-Rom으로 인식시키기 위해서는 GetDriveTypeA의 리턴값이 무엇이 되어야 하는지 찾으면 될 것 같다.

- x32dbg로 해당 파일을 열어주면 다음과 같은 화면을 볼 수 있다.
  <img width="1280" alt="image" src="https://github.com/user-attachments/assets/2edce165-6b23-4ddd-8780-a146e856e9f3">

- 우리는 출력되는 문자열을 알고 있기 때문에 해당 포인트를 이용해서 넘어가준다.
![스크린샷(19)](https://github.com/user-attachments/assets/4e1c9162-66dd-413a-82cd-2fcb2f53bb19)
![스크린샷(18)](https://github.com/user-attachments/assets/ba4dc127-cc27-44f5-9100-4bd45db9b954)

<img width="839" alt="image" src="https://github.com/user-attachments/assets/0b245ca0-78bd-484c-885c-ba9785e6bcf6">
- 해당 포인트로 가면 프로그램의 EntryPoint와 문제를 해결할 수 있는 정보들이 보인다.

<img width="798" alt="image" src="https://github.com/user-attachments/assets/4afe9ea3-11e4-4203-be58-e44680bffd8b">
- 해당 부분이 문제를 풀 수 있는 정보들이다. 일단 Make me think your HD is a CD-Rom. 이 뜨고 나서, inc, dec를 거쳐 cmp를 했을 때 eax와 esi의 값이 일치하면 je (jump equal)를 해서 올바른 구문이 나오게 한다.

<img width="1251" alt="image" src="https://github.com/user-attachments/assets/bb488fe3-0c9c-4bae-8643-0201920e8a26">

- eax의 초기값은 3인 것을 확인할 수 있다. 
<img width="1105" alt="image" src="https://github.com/user-attachments/assets/1a26a06f-0fbe-42a7-a940-6f7b331d074a">

- inc, dec를 cmp 전까지 계속 진행시켜 보겠다.
  <img width="1280" alt="image" src="https://github.com/user-attachments/assets/e43e0312-5d0e-42c1-99b9-cd0720c505ad">
- esi가 3이고 eax가 1이 되기 때문에 초기 eax 값을 5로 바꿔주거나 분기문을 지나기 전에 같은 값으로 바꿔주면 된다.

- <img width="985" alt="image" src="https://github.com/user-attachments/assets/465a856e-18fa-4948-a865-744bb4affd63">
<img width="1255" alt="image" src="https://github.com/user-attachments/assets/ac91dbf5-7bf2-47e2-9d93-948690dbbddb">
