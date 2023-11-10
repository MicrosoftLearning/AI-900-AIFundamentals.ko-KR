---
lab:
  title: 음성 살펴보기
---

# 음성 살펴보기

> **참고** 이 랩을 완료하려면 관리 액세스 권한이 있는 [Azure 구독](https://azure.microsoft.com/free?azure-portal=true)이 필요합니다.

가청 음성을 해석하고 적절하게 응답할 수 있는 소프트웨어를 빌드하려면 음성 언어를 텍스트로 전사하는 간단한 방법을 제공하는 Azure AI Speech** 서비스를 사용할 **수 있습니다.

예를 들어 “What time is it?”과 같은 음성 질문에 구두로 답할 수 있는 스마트 디바이스를 만들고자 한다고 가정하겠습니다. 응답은 현지 시간이어야 합니다.

Speech 서비스의 기능을 테스트하기 위해 Cloud Shell에서 실행되는 간단한 명령줄 애플리케이션을 사용합니다. 웹 사이트 또는 휴대폰 앱과 같은 실제 솔루션에는 동일한 원칙과 기능이 적용됩니다.

## *Azure AI 서비스* 리소스 만들기

Speech 리소스 또는 Azure AI 서비스 리소스를 ****만들어 Speech** Service를 사용할 수 있습니다**.

아직 수행하지 않은 경우 Azure 구독에서 **Azure AI 서비스 리소스를** 만듭니다.

1. 다른 브라우저 탭의 [https://portal.azure.com](https://portal.azure.com?azure-portal=true)에서 Azure Portal을 열고 Microsoft 계정을 사용하여 로그인합니다.

1. **65291을 클릭합니다. 리소스** 단추를 만들고 Azure AI 서비스를 검색*합니다*. Azure AI 서비스 계획 만들기****를** 선택합니다**. 페이지로 이동하여 Azure AI 서비스 리소스를 만듭니다. 다음 설정을 사용하여 구성합니다.
    - **구독**: *자신의 Azure 구독*.
    - **리소스 그룹**: *고유한 이름이 있는 리소스 그룹을 선택하거나 생성*합니다.
    - **지역**: 사용 가능한 지역을 선택합니다**.
    - **이름**: 고유한 이름을 입력합니다.
    - **가격 책정 계층**: 표준 S0
    - **이 확인란 선택하여 아래의 모든 약관을 읽고 이해했음을 확인**: 선택하였습니다.

1. 리소스를 검토하고 만듭니다.

### Azure AI 서비스 리소스의 키 및 위치 가져오기

1. 배포가 완료될 때까지 기다립니다. 그런 다음, Azure AI 서비스 리소스 **로 이동하고 개요** 페이지에서 링크를 클릭하여 서비스에 대한 키를 관리합니다. 클라이언트 애플리케이션에서 Azure AI 서비스 리소스에 연결하려면 엔드포인트와 키가 필요합니다.

1. 리소스에 대한 **키 및 엔드포인트** 페이지를 봅니다. 클라이언트 애플리케이션에서 연결하려면 **위치/지역** 및 **키**가 필요합니다.

## Cloud Shell 실행

Speech 서비스의 기능을 테스트하기 위해 Azure의 Cloud Shell에서 실행되는 간단한 명령줄 애플리케이션을 사용합니다.

1. Azure Portal에서 검색 상자 오른쪽 페이지 맨 위에 있는 **[>_]**(*Cloud Shell*) 단추를 선택합니다. 그러면 포털 아래쪽에 Cloud Shell 창이 열립니다.

    ![맨 위 검색 상자 오른쪽에 있는 아이콘을 클릭하여 Cloud Shell 시작](media/recognize-synthesize-speech/powershell-portal-guide-1.png)

1. Cloud Shell을 처음 열면 사용할 셸 유형(*Bash* 또는 *PowerShell*)을 선택하라는 메시지가 표시될 수 있습니다. **PowerShell**을 선택합니다. 이 옵션이 표시되지 않으면 단계를 건너뜁니다.  

1. Cloud Shell에 대한 스토리지를 만들라는 메시지가 표시되면 구독이 지정되었는지 확인하고 **스토리지 만들기**를 선택합니다. 그런 다음, 스토리지가 만들어질 때까지 1분 정도 기다립니다.

    ![확인을 클릭하여 스토리지를 만듭니다.](media/recognize-synthesize-speech/powershell-portal-guide-2.png)

1. Cloud Shell 창의 왼쪽 위에 표시된 셸 형식이 *PowerShell*로 전환되었는지 확인합니다. *Bash*인 경우 드롭다운 메뉴를 사용하여 *PowerShell*로 전환합니다.

    ![PowerShell로 전환하기 위해 왼쪽 드롭다운 메뉴를 찾는 방법](media/recognize-synthesize-speech/powershell-portal-guide-3.png)

1. PowerShell이 시작될 때까지 기다립니다. Azure Portal에 다음 화면이 표시되어야 합니다.  

    ![PowerShell이 시작될 때까지 기다립니다.](media/recognize-synthesize-speech/powershell-prompt.png)

## 클라이언트 애플리케이션 구성 및 실행

이제 사용자 지정 모델이 있으므로 Speech 서비스를 사용하는 간단한 클라이언트 애플리케이션을 실행할 수 있습니다.

1. 명령 셸에서 다음 명령을 입력하여 샘플 애플리케이션을 다운로드하고 ai-900이라는 폴더에 저장합니다.

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    >**팁** 다른 랩에서 이미 이 명령을 사용하여 *ai-900* 리포지토리를 복제했다면 이 단계를 건너뛰어도 됩니다.

1. 파일은 **ai-900**이라는 폴더에 다운로드됩니다. 이제 Cloud Shell 스토리지에 있는 모든 파일을 보고 작업하려고 합니다. 셸에 다음 명령을 입력합니다.

     ```PowerShell
    code .
    ```

    그러면 아래 이미지와 같은 편집기가 열립니다.

    ![코드 편집기.](media/recognize-synthesize-speech/powershell-portal-guide-4.png)

1. 왼쪽의 **Files** 창에서 **ai-900**을 확장하고 **speaking-clock.ps1**을 선택합니다. 이 파일에는 Speech 서비스를 사용하여 음성을 인식하고 합성하는 일부 코드가 포함되어 있습니다.

    ![Speech 서비스를 사용하기 위한 코드가 포함된 편집기](media/recognize-synthesize-speech/speaking-clock-code.png)

1. 코드의 세부 정보에 대해 크게 걱정하지 마세요. 중요한 점은 Azure AI 서비스 리소스에 대한 지역/위치 및 키 중 하나가 필요하다는 것입니다. Azure Portal의 리소스에 대한 **키 및 엔드포인트** 페이지에서 이러한 값을 복사하여 코드 편집기에 붙여넣고 각각 **YOUR_KEY** 및 **YOUR_LOCATION** 자리 표시자 값을 대체합니다.

    > **팁** **키 및 엔드포인트**와 **편집기** 창에서 작업할 때 구분줄을 사용하여 화면 영역을 조정해야 할 수도 있습니다.

    키 및 지역/위치 값을 붙여넣은 후 코드의 첫 번째 줄은 다음과 유사해야 합니다.

    ```PowerShell
    $key = "1a2b3c4d5e6f7g8h9i0j...."
    $region="somelocation"
    ```

1. 편집기 창의 오른쪽 위에서 **...** 단추를 사용하여 메뉴를 열고 **저장**을 선택하여 변경 내용을 저장합니다. 그런 다음, 메뉴를 다시 열고 **편집기 닫기**를 선택합니다.

    샘플 클라이언트 애플리케이션은 Speech 서비스를 사용하여 음성 입력을 전사하고 적절한 음성 응답을 합성합니다. 실제 애플리케이션은 마이크의 입력을 받아 화자로 응답을 보낼 수 있지만, 이 간단한 예제에서는 파일에 미리 녹음된 입력을 사용하고 응답을 다른 파일로 저장합니다.

    아래 비디오 플레이어를 사용하여 애플리케이션에서 처리할 입력 오디오를 들어봅니다.

    <div class="embeddedvideo"><iframe src="https://www.microsoft.com/videoplayer/embed/RWMAvi" frameborder="0" allowfullscreen="true" data-linktype="external"></iframe></div>

1. PowerShell 창에서 다음 명령을 입력하여 코드를 실행합니다.

    ```PowerShell
    cd ai-900
    ./speaking-clock.ps1
    ```

1. 출력을 검토합니다. “What time is it?” 텍스트를 성공적으로 인식하고 및 output.wav*라는 *파일에 적절한 응답을 저장했습니다.

    다음 비디오 플레이어를 사용하여 애플리케이션에서 생성된 음성 출력을 들어봅니다.

    <div class="embeddedvideo"><iframe src="https://www.microsoft.com/videoplayer/embed/RWMSIU" frameborder="0" allowfullscreen="true" data-linktype="external"></iframe></div>

## 자세한 정보

이 간단한 앱은 Speech 서비스의 기능 중 일부만 표시합니다. 이 서비스를 사용하여 수행할 수 있는 작업을 자세히 알아보려면 [Speech 페이지](https://azure.microsoft.com/services/cognitive-services/speech-services/)를 참조하세요.
