---
lab:
  title: Cognitive Services 살펴보기
  module: Module 1 - Introduction to AI
---

# <a name="explore-cognitive-services"></a>Cognitive Services 살펴보기

> **참고** 이 랩을 완료하려면 관리 액세스 권한이 있는 [Azure 구독](https://azure.microsoft.com/free?azure-portal=true)이 필요합니다.

Azure Cognitive Services는 비전, 음성, 언어, 의사 결정 서비스의 네 가지 주요 요소로 분류할 수 있는 일반적인 AI 기능을 캡슐화합니다. 이 연습에서는 소프트웨어 애플리케이션에서 Cognitive Services 리소스를 프로비저닝하고 사용하는 방법에 대한 일반적인 이해를 얻기 위해 의사 결정 서비스 중 하나를 살펴봅니다.

이 연습에서 살펴볼 특정 Cognitive Services는 *Anomaly Detector*입니다. Anomaly Detector는 시간이 지남에 따라 데이터 값을 분석하고 추가 조사를 위해 문제 또는 문제를 나타낼 수 있는 비정상적인 값을 검색하는 데 사용됩니다. 예를 들어 온도 제어 스토리지 시설의 센서는 매 분마다 온도를 모니터링하고 측정된 값을 기록할 수 있습니다. Anomaly Detector 서비스를 사용하여 기록된 온도 값을 분석하고 예상 온도의 정상 범위를 크게 벗어나는 모든 값에 플래그를 지정할 수 있습니다.

Anomaly Detection 서비스의 기능을 테스트하기 위해 Cloud Shell에서 실행되는 간단한 명령줄 애플리케이션을 사용합니다. 웹 사이트 또는 휴대폰 앱과 같은 실제 솔루션에는 동일한 원칙과 기능이 적용됩니다.

> **참고** 이 연습의 목표는 Cognitive Services가 프로비저닝되고 사용되는 방식에 대한 일반적인 감각을 얻는 것입니다. Anomaly Detector가 예로 사용되지만 이 연습에서 변칙 검색에 대한 포괄적인 지식을 얻을 수는 없습니다.

## <a name="create-an-anomaly-detector-resource"></a>*Anomaly Detector* 리소스 만들기

먼저 Azure 구독에서 **Anomaly Detector** 리소스를 만들어 보겠습니다.

1. 다른 브라우저 탭의 [https://portal.azure.com](https://portal.azure.com?azure-portal=true)에서 Azure Portal을 열고 Microsoft 계정을 사용하여 로그인합니다.

1. **&#65291;리소스 만들기** 단추를 클릭하고, *Anomaly Detector*를 검색하고, 다음 설정을 사용하여 **Anomaly Detector** 리소스를 만듭니다.
    - **구독**: *자신의 Azure 구독*.
    - **리소스 그룹**: 기존 리소스 그룹을 선택하거나 새로 만듭니다.
    - **지역**: 사용 가능한 지역을 선택합니다.
    - **이름**: *고유한 이름을 입력*합니다.
    - **가격 책정 계층**: 무료 F0

1. 리소스를 검토하고 만듭니다. 배포가 완료될 때까지 기다린 다음, 배포된 리소스로 이동합니다.

1. Anomaly Detector 리소스에 대한 **키 및 엔드포인트** 페이지를 봅니다. 클라이언트 애플리케이션에서 연결하려면 엔드포인트와 키가 필요합니다.

## <a name="run-cloud-shell"></a>Cloud Shell 실행

Anomaly Detector 서비스의 기능을 테스트하기 위해 Azure의 Cloud Shell에서 실행되는 간단한 명령줄 애플리케이션을 사용합니다.

1. Azure Portal에서 검색 상자 오른쪽 페이지 맨 위에 있는 **[>_]**(*Cloud Shell*) 단추를 선택합니다. 그러면 포털 아래쪽에 Cloud Shell 창이 열립니다.

    ![맨 위 검색 상자 오른쪽에 있는 아이콘을 클릭하여 Cloud Shell을 시작합니다.](media/anomaly-detector/powershell-portal-guide-1.png)

1. Cloud Shell을 처음 열면 사용할 셸 유형(*Bash* 또는 *PowerShell*)을 선택하라는 메시지가 표시될 수 있습니다. **PowerShell**을 선택합니다. 이 옵션이 표시되지 않으면 단계를 건너뜁니다.  

1. Cloud Shell에 대한 스토리지를 만들라는 메시지가 표시되면 구독이 지정되었는지 확인하고 **스토리지 만들기**를 선택합니다. 그런 다음, 스토리지가 만들어질 때까지 1분 정도 기다립니다.

    ![확인을 클릭하여 스토리지를 만듭니다.](media/anomaly-detector/powershell-portal-guide-2.png)

1. Cloud Shell 창의 왼쪽 위에 표시된 셸 형식이 *PowerShell*로 전환되었는지 확인합니다. *Bash*인 경우 드롭다운 메뉴를 사용하여 *PowerShell*로 전환합니다.

    ![PowerShell로 전환하기 위해 왼쪽 드롭다운 메뉴를 찾는 방법](media/anomaly-detector/powershell-portal-guide-3.png)

1. PowerShell이 시작될 때까지 기다립니다. Azure Portal에 다음 화면이 표시되어야 합니다.  

    ![PowerShell이 시작될 때까지 기다립니다.](media/anomaly-detector/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>클라이언트 애플리케이션 구성 및 실행

이제 Cloud Shell 환경이 생겼으므로 Anomaly Detector 서비스를 사용하여 데이터를 분석하는 간단한 애플리케이션을 실행할 수 있습니다.

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

    ![코드 편집기.](media/anomaly-detector/powershell-portal-guide-4.png)

1. 왼쪽의 **파일** 창에서 **ai-900**을 확장하고 **detect-anomalies.ps1**을 선택합니다. 이 파일에는 다음과 같이 Anomaly Detection 서비스를 사용하는 일부 코드가 포함되어 있습니다.

    ![변칙을 검색하는 코드가 포함된 편집기](media/anomaly-detector/detect-anomalies-code.png)

1. 코드의 세부 사항에 대해 너무 걱정하지 마세요. 중요한 점은 엔드포인트 URL과 Anomaly Detector 리소스의 키 중 하나가 필요하다는 것입니다. 리소스에 대한 **키 및 엔드포인트** 페이지에서 이러한 값(브라우저 위쪽 영역에 있음)을 복사하여 코드 편집기에 붙여넣고 **YOUR_KEY** 및 **YOUR_ENDPOINT** 자리 표시자 값을 각각 대체합니다.

    > **팁** **키 및 엔드포인트**와 **편집기** 창에서 작업할 때 구분줄을 사용하여 화면 영역을 조정해야 할 수도 있습니다.

    키 및 엔드포인트 값을 붙여넣은 후 코드의 처음 두 줄은 다음과 유사하게 표시됩니다.

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. 편집기 창의 오른쪽 위에서 **...** 단추를 사용하여 메뉴를 열고 **저장**을 선택하여 변경 내용을 저장합니다. 그런 다음, 메뉴를 다시 열고 **편집기 닫기**를 선택합니다.

    변칙 검색은 계열의 값이 예상 매개 변수 내에 있는지 여부를 결정하는 데 사용되는 AI 기술입니다. 샘플 클라이언트 애플리케이션은 Anomaly Detector 서비스를 사용하여 일련의 날짜/시간 및 숫자 값이 포함된 파일을 분석합니다. 애플리케이션은 각 시점에 숫자 값이 예상 매개 변수 내에 있는지 여부를 나타내는 결과를 반환해야 합니다.

1. PowerShell 창에서 다음 명령을 입력하여 코드를 실행합니다.

    ```PowerShell
    cd ai-900
    .\detect-anomalies.ps1
    ```

1. 결과를 검토하고 결과의 마지막 열이 **True** 또는 **False**인지를 파악하여 각 날짜/시간에 기록된 값이 변칙으로 간주되는지 여부를 알아봅니다. 실제 상황에서 이 정보를 사용할 수 있는 방법을 고려합니다. 값이 냉장고 온도 또는 혈압이고 변칙이 감지된 경우 애플리케이션이 트리거할 수 있는 작업은 무엇인가요?  

## <a name="learn-more"></a>자세한 정보

이 간단한 앱은 Anomaly Detector 서비스의 기능 중 일부만 표시합니다. 이 서비스를 사용하여 수행할 수 있는 작업을 자세히 알아보려면 [Anomaly Detector 페이지](https://azure.microsoft.com/services/cognitive-services/anomaly-detector/)를 참조하세요.

## <a name="clean-up"></a>정리

프로젝트가 끝날 때 여기에서 만든 리소스가 계속 필요한지 확인하는 것이 좋습니다. 계속 실행되는 리소스에는 요금이 부과될 수 있습니다. 

AI 기본 사항 모듈을 계속 진행하는 경우 다른 랩에서 사용하기 리소스를 유지할 수 있습니다.

학습을 완료한 경우 Azure 구독에서 리소스 그룹이나 개별 리소스를 삭제할 수 있습니다.

1. [Azure 포털](https://portal.azure.com/)의 **리소스 그룹** 페이지에서 리소스를 만들 때 지정한 리소스 그룹을 엽니다.

2. **리소스 그룹 삭제**를 클릭하고 삭제하고자 하는 리소스 그룹 이름을 입력한 다음 **삭제**를 선택합니다. 리소스를 선택하고 점 세 개를 클릭해 추가 옵션을 표시한 후 **삭제**하여 개별 리소스를 삭제하도록 선택할 수도 있습니다.