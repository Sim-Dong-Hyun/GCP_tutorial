# GCP_Install and Setting

https://cloud.google.com

위 링크에 접속 후 가입 및 300$ 크레딧 수령

프로젝트 생성

![대체 텍스트](/figure/1-1.png)


![대체 텍스트](/figure/2-1.PNG)





좌측 상단에 탐색 메뉴를 클릭하고, **ML엔진**에 들어가서 **모델**을 만들어준다.




위 사진처럼 각 종 서비스들을 고정해두면 두고두고 편하다.




![대체 텍스트](/figure/10.png)




**Storage**에 들어가서 **버킷**을 만든다.

> 이름은 알아서, 기본 저장소 클래스는 Multi-Regional, 위치는 아시아로 해줍시다.







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

**set GOOGLE_APPLICATION_CREDENTIALS=[PATH]**



나의 경우엔 아래와 같다.

**set GOOGLE_APPLICATION_CREDENTIALS=[C:\Users\SDH\Desktop\MINESLAB\GCP_tensorflow_test\test-f0439c5d022a.json]**




여기까지 했으면 아래의 링크를 눌러 구글 클라우드 SDK를 다운받는다.


https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe


설치가 되었다면 Google Cloud SDK Shell을 실행 시키고

**gcloud init**이라는 명령어를 입력해준다.


지역 빼고는 알아서 잘 해주면 된다.

지역의 경우 2018/09/28 기준 되지 않는 지역이 몇군대 있었다.

안되는 지역일 경우 shell이 알아서 알려준다. 안되는 지역을 피하고 선택하면 된다.




> 사실 이 튜토리얼은 필자가 급하게 하다가 뜬금없이 쓰게 되어 버렸는데
>
> 학과 동기가 튜토리얼을 요청해서 쓰는 것이다. 때문에 SDK를 새로 설치하지 않고
>
> 기억에 의존해서 튜토리얼을 쓰는 중이다. 즉, 정확하지 않을 수도 있다.
>
> 잘 안된다면 카톡으로 물어보세요.




***




init 까지 다 되었다면 아래 단계를 진행하면 된다.

구글 클라우드 플랫폼에 접속해서 자신의 프로젝트로 가보자.




![대체 텍스트](/figure/7.png)





여기서 프로젝트 ID를 복사해준다.




![대체 텍스트](/figure/1-1.png)




우측 상단 메뉴에 보면 Cloud Shell 활성화 버튼이 있다.


콘솔이 켜지면 아래 명령어를 입력한다.


**gcloud config set project [selected-project-id]**


브라켓 안에는 아까 복사한 프로젝트 ID를 붙여 넣는다.

브라켓은 지워줍시다. 아래 사진처럼 에러가 뜰 수도 있습니다.




![대체 텍스트](/figure/8.png)




***




위 과정까지 했다면 Google Cloud SDK Shell을 켠다.

아까 설치한 그것 맞다. 실행시켜주자. 아래 명령어도 실행시켜주자.

**gcloud ml-engine models list**




![대체 텍스트](/figure/9.png)




위와 같이 나온다면 정상이다.

**gcloud projects list** 라고 입력하면 계정의 모든 프로젝트를 볼 수 있다.


다른 명령어는 **gcloud --help** 를 입력해서 볼 수 있다.




***




이제 폴더 하나를 만들어주자. 아까 JSON 파일을 저장한 폴더라도 상관없다.


**__init__.py** 라는 파일을 만든다. 언더바(under line) 두개를 앞 뒤로 붙여주어야 한다.
> 깃허브 마크다운 문법상 언더바가 나오질 않는다. 방법이 있을텐데 필자가 어떻게 하는지 모른다.
> 아래 사진 참고.

안에 아무것도 들어있지 않아도 상관없다.





그 다음 간단한 코딩을 해준다.

필자는 간단한 계산을 해보았다.




![대체 텍스트](/figure/11.png)




300$ 크레딧이 주어졌다고 하지만, 로컬에서 한번쯤 돌려보고 클라우드에 업로드 하는 것이 경제적인것 같다.




***




cmd를 열어준다.

그리고 긴 명령어를 입력해준다.


아래는 예시이다.




![대체 텍스트](/figure/12.png)




**gcloud ml-engine jobs submit training** [job의 이름] **--package-path=** [돌릴 소스의 상위 dir까지 입력] **--module-name=** [돌릴 소스의 상위 dir와 소스 이름 입력] **--staging-bucket=**[gs://아까 만든 버켓 이름]



이게 한 명령어다. 엄청길다.


사진과 설명을 번갈아가면서 보면 이해될 것이다.

위 명령어 덩어리를 입력한다면 사진과 같이 **state:QUEUED**라는 것을 보게 될 것이다.



제대로 되었다면 구글 클라우드 플렛폼에 접속해서 ML엔진 메뉴에 접속하면 아래와 같은 모습이 보일 것이다.




![대체 텍스트](/figure/13.png)



작업의 진행 상황을 cmd창에서 보고 싶다면 아래의 명령어를 입력하면 된다.


위 gcloud 명령어가 있는 사진에 보면 state:QUEUED의 윗 윗줄에도 적혀있다.




![대체 텍스트](/figure/14.png)




**gcloud ml-engine jobs stream-logs** [job의 이름]




***


![대체 텍스트](/figure/15.png)




작업이 다 돌아갔다면 위와 같이 결과가 나올 것이다.


탐색메뉴에서 **결제**에 들어가면 자신의 결제 정보를 확인할 수 있다.


처음에 가입하고 받은 300$ 크레딧에 대한 만료일과 잔액도 확인이 가능하다.



***USE GPU & Choose Runtime Version, Python Version


이제 ml engine을 사용하는 대부분의 이유인 GPU 사용법에 대해 알아보자.


ml engine은 GPU뿐만 아니라 CPU와 TPU 등 다양한 고성능 컴퓨팅 머신을 제공한다.


TPU 사용법에 대해서는 후에 추가하도록 하고, 이번엔 GPU 사용법에 대해 알아보자.


우선 아래는 ml engine에서 제공하는 사전 정의된 GPU 머신의 종류와 가격이다.


가격 측정의 기준은 아시아 태평양이다.


![대체 텍스트](/figure/gpu.png)


**BASIC**과 **STANDARD_1, PREMIUM_1**의 경우 CPU 머신이다.


그 아래 **BASIC_GPU**은 **NVIDIA Tesla K80**을 사용할 수 있는 머신이다.


즉, 우리는 K80 GPU를 시간 당 약 1.36$에 이용할 수 있는 것이다.


여러개의 K80 GPU 혹은 **NVIDIA Tesla P100**, **NVIDIA Tesla V100**을 사용할 수도 있지만,


우선 하나의 K80부터 다루어보도록 하자.


***


이전에 사용했던 명령어를 기억해보자.


**gcloud ml-engine ...**


![대체 텍스트](/figure/12.png)


이미 눈치 챈 사람도 있겠지만 **--** 뒤에 붙는 명령어는 옵션과 비슷한 것이다.


여기서 우리는 컴퓨팅 머신을 옵션으로 넣어줄 수 있다.

뒤에 **--scale-tier=basic_gpu**을 적으면 GPU 사용 세팅은 끝난 것이다.


실행을 시키면 아래와 같은 명령어를 볼 수 있을 것이다.


![대체 텍스트](/figure/gpu2.png)



***

이제 ml engine의 **runtime version**과 **Python version**을 선택해보자.


https://cloud.google.com/ml-engine/docs/tensorflow/runtime-version-list


위의 링크는 ml engine의 runtime version과 version에 따른 지원하는 패키지

그리고 파이썬 버전을 알 수 있다.


18년 11월 10일 기준 가장 최신 버전은 1.10버전이며,


옵션을 설정하지 않으면 디폴트 값으로 1.0 버전으로 실행된다.


파이썬 3.5의 경우 1.4버전 이상의 경우만 동작이 가능하다.


또한 런타임 버전에 따라 실행 가능한 텐서플로우의 버전이 다르니


자신이 필요한 버전을 선택하도록 하자.


위의 컴퓨팅 머신 선택과 마찬가지로 **--** 를 붙혀서 런타임 버전을 설정해주고,


파이썬 3 유저일 경우 필자와 같이 따로 설정을 적어주자.


**gcloud ml-engine jobs submit test_bundle --package-path=./ --module-name=test.test --staging-bucket=gs://sdh-satellite --scale-tier=basic_gpu --python-version=3.5 --runtime-version=1.10**


위와 같이 적어주면 우리는 이제 GPU를 사용하면서 파이썬 3.5버전과


ml engine 1.10에서 지원하는 패키지를 사용할 수 있다.


이미 위의 기본적인 튜토리얼을 실행시켜본 사람은 알 수 있겠지만


**gcloud ml-engine jobs stream-logs job-name** 이외에 

**gcloud ml-engine jobs describe job-name** 이라는 명령어를 볼 수 있다.


**jobs describe** 명령어를 실행시키면 자신의 job에 대한 정보를 볼 수 있다.


아래 사진을 참고하자.


![대체 텍스트](/figure/jobs_descr.png)
