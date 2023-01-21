---
lab:
  title: 번역 살펴보기
---

# <a name="explore-translation"></a>번역 살펴보기

> **참고** 이 랩을 완료하려면 관리 액세스 권한이 있는 [Azure 구독](https://azure.microsoft.com/free?azure-portal=true)이 필요합니다.

인류 문명이 발전할 수 있었던 원동력 중 하나는 서로 소통하는 능력이었습니다. 대부분의 인간 노력에는 소통이 핵심입니다.

AI(인공 지능)는 언어 간 텍스트 또는 음성을 번역하여 소통을 간소화하여 국가 및 문화권 간 소통 장벽을 제거하는 데 도움이 될 수 있습니다.

Translator 서비스의 기능을 테스트하기 위해 Cloud Shell에서 실행되는 간단한 명령줄 애플리케이션을 사용합니다. 웹 사이트 또는 휴대폰 앱과 같은 실제 솔루션에는 동일한 원칙과 기능이 적용됩니다.

## <a name="create-a-cognitive-services-resource"></a>*Cognitive Services* 리소스 만들기

**Translator** 리소스 또는 **Cognitive Services** 리소스를 생성하여 Translator 서비스를 사용할 수 있습니다.

아직 만들지 않았다면 Azure 구독에서 **Cognitive Services** 리소스를 만듭니다.

1. 다른 브라우저 탭의 [https://portal.azure.com](https://portal.azure.com?azure-portal=true)에서 Azure Portal을 열고 Microsoft 계정을 사용하여 로그인합니다.

1. **&#65291;리소스 만들기** 단추를 선택하고 *Cognitive Services*를 검색한 후에 다음 설정을 사용하여 **Cognitive Services** 리소스를 만듭니다.
    - **구독**: *자신의 Azure 구독*.
    - **리소스 그룹**: *고유한 이름이 있는 리소스 그룹을 선택하거나 생성*합니다.
    - **지역**: 사용 가능한 지역을 선택합니다.
    - **이름**: *고유한 이름을 입력*합니다.
    - **가격 책정 계층**: 표준 S0
    - **이 확인란 선택하여 아래의 모든 약관을 읽고 이해했음을 확인**: 선택하였습니다.

1. 리소스를 검토 및 만들고 배포가 완료될 때까지 기다립니다. 그런 다음, 배포된 리소스로 이동합니다.

1. Cognitive Services 리소스에 대한 **키 및 엔드포인트** 페이지를 봅니다. 클라이언트 애플리케이션에서 연결하려면 키와 위치가 필요합니다.

### <a name="get-the-key-and-location-for-your-cognitive-services-resource"></a>Cognitive Services 리소스의 키 및 위치 가져오기

1. 배포가 완료될 때까지 기다립니다. 그런 다음, Cognitive Services 리소스로 이동하고 **개요** 페이지에서 링크를 선택하여 서비스의 키를 관리합니다. 클라이언트 애플리케이션에서 Cognitive Services 리소스에 연결하려면 키와 위치가 필요합니다.

1. 리소스에 대한 **키 및 엔드포인트** 페이지를 봅니다. 클라이언트 애플리케이션에서 연결하려면 **위치/지역** 및 **키**가 필요합니다.

> **참고** Translator 서비스를 사용하기 위해 Cognitive Service 엔드포인트를 사용할 필요가 없습니다. Translator 서비스만을 위한 글로벌 엔드포인트가 제공됩니다. 

## <a name="run-cloud-shell"></a>Cloud Shell 실행

Translation 서비스의 기능을 테스트하기 위해 Azure의 Cloud Shell에서 실행되는 간단한 명령줄 애플리케이션을 사용합니다. 

1. Azure Portal에서 검색 상자 오른쪽 페이지 맨 위에 있는 **[>_]**(*Cloud Shell*) 단추를 선택합니다. 그러면 포털 아래쪽에 Cloud Shell 창이 열립니다.

    ![맨 위 검색 상자 오른쪽에 있는 아이콘을 클릭하여 Cloud Shell을 시작합니다.](media/translate-text-and-speech/powershell-portal-guide-1.png)

1. Cloud Shell을 처음 열면 사용할 셸 유형(*Bash* 또는 *PowerShell*)을 선택하라는 메시지가 표시될 수 있습니다. **PowerShell**을 선택합니다. 이 옵션이 표시되지 않으면 단계를 건너뜁니다.  

1. Cloud Shell에 대한 스토리지를 만들라는 메시지가 표시되면 구독이 지정되었는지 확인하고 **스토리지 만들기**를 선택합니다. 그런 다음, 스토리지가 만들어질 때까지 1분 정도 기다립니다.

    ![확인을 클릭하여 스토리지를 만듭니다.](media/translate-text-and-speech/powershell-portal-guide-2.png)

1. Cloud Shell 창의 왼쪽 위에 표시된 셸 형식이 *PowerShell*로 전환되었는지 확인합니다. *Bash*인 경우 드롭다운 메뉴를 사용하여 *PowerShell*로 전환합니다. 

    ![PowerShell로 전환하기 위해 왼쪽 드롭다운 메뉴를 찾는 방법](media/translate-text-and-speech/powershell-portal-guide-3.png) 

1. PowerShell이 시작될 때까지 기다립니다. Azure Portal에 다음 화면이 표시되어야 합니다.  

    ![PowerShell이 시작될 때까지 기다립니다.](media/translate-text-and-speech/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>클라이언트 애플리케이션 구성 및 실행

이제 사용자 지정 모델이 있으므로 Translation 서비스를 사용하는 간단한 클라이언트 애플리케이션을 실행할 수 있습니다.

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

    ![코드 편집기.](media/translate-text-and-speech/powershell-portal-guide-4.png)

1. 왼쪽의 **Files** 창에서 **ai-900**을 확장하고 **translator.ps1**을 선택합니다. 이 파일에는 Translator 서비스를 사용하는 일부 코드가 포함되어 있습니다.

    ![Translator 서비스를 사용하기 위한 코드가 포함된 편집기](media/translate-text-and-speech/translate-code.png)

1. 코드의 세부 사항에 대해 너무 걱정하지 마세요. 중요한 점은 지역/위치 및 Cognitive Services 리소스의 키 중 하나가 필요하다는 것입니다. Azure Portal의 리소스에 대한 **키 및 엔드포인트** 페이지에서 이러한 값을 복사하여 코드 편집기에 붙여넣고 각각 **YOUR_KEY** 및 **YOUR_LOCATION** 자리 표시자 값을 대체합니다.

    키 및 위치 값을 붙여넣은 후 코드의 첫 번째 줄은 다음과 유사해야 합니다.

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."
    $location="somelocation"
    ```

1. 편집기 창의 오른쪽 위에서 **...** 단추를 사용하여 메뉴를 열고 **저장**을 선택하여 변경 내용을 저장합니다. 그런 다음, 메뉴를 다시 열고 **편집기 닫기**를 선택합니다.

    샘플 클라이언트 애플리케이션은 Translator 서비스를 사용하여 여러 작업을 수행합니다.
    - 텍스트를 영어에서 프랑스어, 이탈리아어 및 중국어로 번역합니다.
    - 오디오를 영어에서 프랑스어로 된 텍스트로 번역

    아래 비디오 플레이어를 사용하여 애플리케이션에서 처리할 입력 오디오를 들어봅니다.

    <div class="embeddedvideo"><iframe src="https://www.microsoft.com/videoplayer/embed/RWORN0" frameborder="0" allowfullscreen="true" data-linktype="external"></iframe></div>


    > **참고** 실제 애플리케이션은 마이크의 입력을 받아 화자로 응답을 보낼 수 있지만, 이 간단한 예제에서는 오디오 파일에 미리 녹음된 입력을 사용합니다.

1. Cloud Shell 창에서 다음 명령을 입력하여 코드를 실행합니다.

    ```PowerShell
    cd ai-900
    ./translator.ps1
    ```

1. 출력을 검토합니다. 영어로 된 텍스트를 프랑스어, 이탈리아어 및 중국어로 번역한 것을 보셨나요?  영어 오디오 “hello”를 프랑스어로 번역한 텍스트를 보셨나요?

## <a name="learn-more"></a>자세한 정보

이 간단한 앱은 Translator 서비스의 기능 중 일부만 보여줍니다. 이 서비스를 사용하여 수행할 수 있는 작업을 자세히 알아보려면 [Translator 페이지](https://docs.microsoft.com/azure/cognitive-services/translator/translator-overview)를 참조하세요.