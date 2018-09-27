# GCP_tutorial

https://cloud.google.com

위 링크에 접속 후 가입 및 300$ 크레딧 수령

프로젝트 생성

![대체 텍스트](/figure/1.png)

***

좌측 상단에 탐색 메뉴 클릭 후 **Compute Engine**을 클릭
**VM인스턴스 생성**

![대체 텍스트](/figure/2.png)
![대체 텍스트](/figure/3.png)

ID 및 API 엑세스는 사진에 표시된대로 해준다.

나머지 옵션은 취향따라 알아서 선택한다.

좌측 상단에 탐색 메뉴를 클릭하고, **ML엔진**에 들어가서 **모델**을 만들어준다.

**Storage**에 들어가서 **버킷**을 만든다.

> 이름은 알아서, 기본 저장소 클래스는 Multi-Regional, 위치는 아시아로 해줍시다.

위 사진처럼 각 종 서비스들을 고정해두면 두고두고 편하다.

고정하는 김에 **API및 서비스**도 고정해두자.

좀있다가 써야한다.

***

https://console.cloud.google.com/flows/enableapi?apiid=ml.googleapis.com,compute_component&_ga=2.109735046.-2023158229.1525695083

위 링크에 들어가서 프로젝트를 등록한다.

아래 사진과 같다

![대체 텍스트](/figure/4.png)


> 안될시 https://cloud.google.com/ml-engine/docs/tensorflow/getting-started-training-prediction 에 접속 후
>
> 컨트룰 + F로 Enable the Cloud Machine Learning Engine and Compute Engine APIs. 를 찾고
>
> ENABLE THE APIS 버튼을 눌러준다. 
>
> 그렇다 이 튜토리얼은 구글 클라우드 플랫폼에서 제공하는 문서를 옮긴 것이다. 정말 쓸모없는 짓이다.


***

https://console.cloud.google.com/apis/credentials/serviceaccountkey?_ga=2.104613379.-2023158229.1525695083

위 링크에 들어가서 서비스 계정 키를 만들어준다.

서비스 계정은 **Compute Engine default service account**를 선택한다.

> 마찬가지로 안될 시 Go to the Create service account key page in the GCP Console. 를 찾고
>
> Go to the Create service account key page 버튼을 눌러준다.

![대체 텍스트](/figure/5.png)

위와 같은 모습이 보이면 잘된것이다.

**키 유형**은 **JSON**을 선택한다.

생성 버튼을 누르면 JSON 파일이 다운로드 될 것이다. 


![대체 텍스트](/figure/6.png)


따로 폴더를 만들어서 빼놓도록 하자!


***

cmd를 열고 아래 명령어를 적어준다.

PATH에는 방금 다운받은 JSON파일의 위치를 입력한다.

set GOOGLE_APPLICATION_CREDENTIALS=[PATH]



나의 경우엔 아래와 같다.

set GOOGLE_APPLICATION_CREDENTIALS=[C:\Users\SDH\Desktop\MINESLAB\GCP_tensorflow_test\test-f0439c5d022a.json]


여기까지 했으면 아래의 링크를 눌러 구글 클라우드 SDK를 다운받는다.


https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe


설치가 되었다면 Google Cloud SDK Shell을 실행 시키고

**gcloud init**이라는 명령어를 입력해준다.


지역 빼고는 알아서 잘 해주면 된다.

지역의 경우 2018/09/28 기준 되지 않는 지역이 몇군대 있었다.

안되는 지역일 경우 shell이 알아서 알려준다. 안되는 지역을 피하고 선택하면 된다.




사실 이 튜토리얼은 필자가 급하게 하다가 뜬금없이 되어 버렸는데

학과 동기가 튜토리얼을 요청해서 쓰는 것이다. 때문에 SDK를 새로 설치하지 않고

기억에 의존해서 튜토리얼을 쓰는 중이다. 즉, 정확하지 않을 수도 있다.

잘 안된다면 카톡으로 물어보세요.


***

init 까지 다 되었다면 아래 단계를 진행하면 된다.

구글 클라우드 플랫폼에 접속해서 자신의 프로젝트로 가보자.

![대체 텍스트](/figure/7.png)

여기서 프로젝트 ID를 복사해준다.

![대체 텍스트](/figure/1.png)


우측 상단 메뉴에 보면 Cloud Shell 활성화 버튼이 있다.


콘솔이 켜지면 아래 명령어를 입력한다.


gcloud config set project [selected-project-id]


브라켓 안에는 아까 복사한 프로젝트 ID를 붙여 넣는다.

브라켓은 지워줍시다. 아래 사진처럼 에러가 뜰 수도 있습니다.


![대체 텍스트](/figure/8.png)


***


위 과정까지 했다면 Google Cloud SDK Shell을 켠다.

아까 설치한 그것 맞다. 실행시켜주자. 아래 명령어도 실행시켜주자.

**gcloud ml-engine models list**







