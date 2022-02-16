## 로컬 개발 

로컬 컴퓨터에서 작업 중이라면 다음 단계를 따라 랩이 작동하도록 환경을 구성할 수 있습니다.  

### C++ 재배포 가능 패키지 
1. [Visual C++ 재배포 가능 패키지(x64)](https://aka.ms/vs/16/release/vc_redist.x64.exe) 다운로드 및 설치 

### Python 및 필수 패키지 
1. [Python 3.6.1](https://www.python.org/downloads/release/python-361/) 설치  
   - **중요**: Python을 PATH 변수에 추가하고 기본 Python 환경으로 등록하는 옵션을 선택합니다. 
2. 설치 후에 *명령 프롬프트*를 열고 다음 명령을 입력하여 필요한 패키지를 설치합니다. 

> pip install ipython jupyter matplotlib pillow requests azure-cognitiveservices-vision-computervision azure-cognitiveservices-vision-customvision azure-cognitiveservices-vision-face azure-cognitiveservices-language-textanalytics azure.cognitiveservices.speech azure_ai_formrecognizer 

### Visual Studio Code 
1. Visual Studio Code가 아직 설치되어 있지 않으면 [여기에서 다운로드](https://code.visualstudio.com/Download)하세요. 설치 후에 Visual Studio Code를 실행하고 확장 프로그램 탭(CTRL+SHIFT+X)에서 Microsoft의 **Python** 확장 프로그램을 검색하여 설치합니다.

2. Visual Studio Code에서 새 터미널을 열고, **git clone https://github.com/MicrosoftLearning/AI-900KO-Microsoft-Azure-AI-Fundamentals** 을 입력하고, *들어가기*를 선택합니다. 

