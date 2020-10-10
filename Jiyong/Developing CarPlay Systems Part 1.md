# Developing CarPlay Systems, Part 1

### CarPlay

- Familiar 
  - CarPlay는 iPhone의 친숙한 요소와 상호 작용 패턴을 자동차에 적용합니다
- Integrated
  - CarPlay는 차량의 내장 시스템과 신중하게 통합되어 최상의 사용자 경험을 제공합니다.
- Future ready
  - CarPlay를 사용하면 미래를위한 디자인을 할 수 있습니다.



### How CarPlay Works

iPhone이 연결되면 CarPlay 세션이 시작됩니다.
CarPlay 세션이 시작되면 정보가 통신 프로토콜을 통해 양방향으로 전송됩니다.
iPhone에서 자동차로 비디오와 오디오를 전송, 자동차의 마이크에서 iPhone으로 오디오를 전송할 수 있습니다.

CarPlay 홈 화면이 처음 표시되고 오디오가 재생되지 않으면 통신 프로토콜이 설정 및 위치 정보에 사용됩니다.
CarPlay UI(홈 화면)를 보여주기 위하여 H264 비디오 스트림이 iPhone에서 자동차로 전송됩니다.

![image-20201010203135617](/Users/user/Library/Application Support/typora-user-images/image-20201010203135617.png)

그런 다음 CarPlay에서 오디오를 재생하면 통신 프로토콜이 추가로 재생 트랙에 대한 정보를 전송하는 데 사용됩니다. 여기의 비디오 스트림은 현재 재생중인 화면을 인코딩하고 있으며 노래의 오디오는 자동차로 전송됩니다.

![image-20201010203159820](/Users/user/Library/Application Support/typora-user-images/image-20201010203159820.png)

CarPlay UI가 종료되고 자동차 화면이 표시되면 CarPlay 세션은 유지됩니다.
통신 프로토콜은 현재 재생 및 위치 정보에 계속 사용됩니다.
비디오 스트림은 더 이상 필요하지 않지만 CarPlay 오디오는 계속 재생됩니다.
화면과 오디오는 독립적으로 제어됩니다. 기본 시스템의 비디오는 CarPlay 오디오가 재생되는 동안 표시 될 수 있습니다. CarPlay 인터페이스가 표시되면 FM 라디오와 같은 기본 시스템의 오디오가 재생 될 수 있습니다.

![image-20201010203100760](/Users/user/Library/Application Support/typora-user-images/image-20201010203100760.png)

PTT 스티어링 휠 버튼을 사용하여 Siri를 실행하면 어떻게되는지 살펴 보겠습니다.
통신 프로토콜은 iOS 음성 인식이 진행 중임을 헤드 유닛에 알리는 데 사용됩니다.
CarPlay UI가 화면으로 전송되고 Siri 오디오 차임이 차량 스피커에서 재생됩니다. 이 경우 오디오도 차량의 마이크에서 iPhone으로 전송됩니다.

### 유선연결

![image-20201010203709157](/Users/user/Library/Application Support/typora-user-images/image-20201010203709157.png)

유선 CarPlay의 경우 데이터는 USB를 통해 전송됩니다.
모든 데이터는 IP로 래핑됩니다.

오디오, 전화, 차량센서들은 iAP2 통신 프로토콜을 통해 전송되고,  그 외 데이터는 IP를 통해 통신하며 통신 플러그인은 Apple에서 제공하는 소스코드이며 터치스크린, 버튼, 터치패드 액션이 Plug-in으로 전송되어 통신이 이루어지게 됩니다.

![image-20201010204045166](/Users/user/Library/Application Support/typora-user-images/image-20201010204045166.png)

무선 연결에 있어서는 Wi-Fi와 블루투스가 모두 필요합니다.
무선의 경우 모든 데이터가 IP로 래핑됩니다. 그 외의 작동 방식은 유선방식과 동일하다.

### Key Vehicle Requirements

- **Key Vehicle Requirements**

  > 여러 표준 디스플레이 해상도가 지원되며 해당 해상도가 여기에 표시됩니다. 대부분은 약 **16x9** 입니다.
  >
  > 지원되는 모든 해상도는 가로 방향입니다.
  >
  >  24 bit 색 농도가 필요하며, 반응 형 사용자 인터페이스에는 60Hz의 재생률을 적극 권장합니다.
  >  H264 디코더가 올바른 프로필을 지원하는지 확인하십시오. 

- **Speaker and Microphone Requirements**

  > ![image-20201010204851734](/Users/user/Library/Application Support/typora-user-images/image-20201010204851734.png)
  > CarPlay 오디오는 Main audio와 Alternate audio로 분리됩니다.
  > Main audio는 양방향이며 음악 및 기타 미디어와 전화 통화 및 Siri에 사용됩니다.
  >
  > Notification에는 대체 오디오가 사용되며 항상 헤드 유닛에서 메인 오디오와 믹싱해야합니다. .
  >
  > LPCM은 유선 CarPlay에 사용됩니다.(LPCM은 무압축이고,음질도 당연히 가장 좋지만, 용량이 엄청나게 큼)
  >
  > Wireless CarPlay에는 압축 된 오디오가 필요합니다.
  >  AAC-LC는 미디어에 사용되며 다른 오디오의 경우 OPUS와 AAC-ELD 중에서 선택할 수 있습니다.

- 

### Design Guidelines

### Supported Apps

