---
lab:
  title: 언어 이해 살펴보기
  module: Module 4 - Natural Language Processing (NLP)
---

# <a name="explore-language-understanding"></a>언어 이해 살펴보기

> **참고** 이 랩을 완료하려면 관리 액세스 권한이 있는 [Azure 구독](https://azure.microsoft.com/free?azure-portal=true)이 필요합니다.

점점 더 많은 컴퓨터에서 자연어의 음성 또는 입력된 명령을 이해하기 위해 AI를 사용할 수 있기를 기대합니다. 예를 들어 "조명 켜기" 또는 "팬 켜기"와 같은 음성 명령을 사용하여 홈에서 디바이스를 제어하고, AI 기반 디바이스에서 명령을 이해하여 적절한 조치를 취할 수 있도록 하는 홈 자동화 시스템을 구현할 수 있습니다.

대화형 언어 이해 서비스의 기능을 테스트하기 위해 Cloud Shell에서 실행되는 명령줄 애플리케이션을 사용합니다. 웹 사이트 또는 휴대폰 앱과 같은 실제 솔루션에는 동일한 원칙과 기능이 적용됩니다.

## <a name="create-a-language-service-resource"></a>언어 서비스 리소스 만들기

**언어 서비스** 리소스를 만들어 대화형 언어 이해 서비스를 사용할 수 있습니다.

아직 만들지 않았다면 Azure 구독에서 **언어 서비스** 리소스를 만듭니다.

1. 다른 브라우저 탭의 [https://portal.azure.com](https://portal.azure.com?azure-portal=true)에서 Azure Portal을 열고 Microsoft 계정을 사용하여 로그인합니다.

1. **&#65291;리소스 만들기** 단추를 클릭하고 언어 서비스를 검색한 후 다음 설정을 사용하여 **언어 서비스** 리소스를 만듭니다.
    - 추가 기능 선택: 기본 기능을 유지하고 계속을 클릭하여 리소스를 만듭니다.  
    - **구독**: *자신의 Azure 구독*.
    - **리소스 그룹**: *고유한 이름이 있는 리소스 그룹을 선택하거나 생성*합니다.
    - **지역**: 미국 동부 2
    - **이름**: *고유한 이름을 입력*합니다.
    - **가격 책정 계층**: S(분당 호출 1,000개)
    - **이 확인란을 선택하여 책임 있는 AI 알림의 조항을 검토하고 승인했음을 확인**: 선택하였습니다.

1. 리소스를 검토 및 만들고 배포가 완료될 때까지 기다립니다.

### <a name="create-a-conversational-language-understanding-app"></a>Conversational Language Understanding 앱 만들기

Conversational Language Understanding을 통해 자연어 이해를 구현하려면 앱을 만든 다음, 엔터티, 의도, 발화를 추가하여 앱이 실행할 명령을 정의합니다.

1. 새 브라우저 탭에서 [https://language.azure.com](https://language.azure.com?azure-portal=true)의 Language Studio 포털을 열고 Azure 구독과 연결된 Microsoft 계정을 사용하여 로그인합니다.

1. 언어 리소스를 선택하라는 메시지가 표시되면 다음 설정을 선택합니다.
    - **Azure Directory**: 구독이 포함된 Azure Directory입니다.
    - **Azure 구독**: Azure 구독입니다.
    - **언어 리소스**: 이전에 만든 언어 리소스입니다.

    >**팁** 언어 리소스를 선택하라는 메시지가 표시되지 않으면 구독에 여러 언어 리소스가 있기 때문일 수 있습니다. 이 경우 다음을 수행합니다.******
    >1. 페이지의 위쪽에 있는 막대에서 **설정(&#9881;)** 단추를 클릭합니다.
    >1. **설정** 페이지에서 **리소스** 탭을 봅니다.
    >1. 언어 리소스를 선택하고 **리소스 전환**을 클릭합니다.
    >1. 페이지 맨 위에서 **Language Studio**를 클릭하여 Language Studio 홈페이지로 돌아갑니다.

1. 포털 위쪽의 **새로 만들기** 메뉴에서 **대화형 언어 이해**을 선택합니다.

1. **기본 정보 입력** 페이지의 **프로젝트 만들기** 대화 상자에 다음 세부 정보를 입력하고 **다음**을 클릭합니다.
    - **이름**: 고유 이름 만들기
    - **설명**: 간단한 홈 자동화
    - **발화 기본 언어**: 영어
    - **프로젝트에서 여러 언어 사용**: 선택하지 마세요.

    ![프로젝트의 세부 정보를 입력합니다.](media/conversational-language-understanding/create-project.png)

    >**팁** 프로젝트 이름을 적어 두세요. 나중에 사용할 수 있습니다.

1. 검토 및 완료 페이지에서 **만들기**를 클릭합니다.

### <a name="create-intents-utterances-and-entities"></a>의도, 발화 및 엔터티 만들기

의도는 수행하려는 작업입니다. 예를 들어 조명을 켜거나 팬을 끌 수 있습니다. 이 경우 디바이스 켜기와 디바이스 쓰기의 두 가지 의도를 정의합니다. 각 의도에 대해 의도를 나타내는 데 사용되는 언어의 종류를 나타내는 샘플 *발화*를 지정합니다.

1. **스키마 정의** 창에서 **의도**가 선택되었는지 확인합니다. 그런 다음, **추가**를 클릭하고, 이름이 **switch_on**(소문자)인 의도를 추가하고, **의도 추가**를 클릭합니다.

    ![빌드 스키마 창에 있는 의도 아래에서 추가를 클릭합니다.](media/conversational-language-understanding/build-schema.png)
    ![switch_on 의도를 추가한 다음, 의도 추가를 선택합니다.](media/conversational-language-understanding/add-intent.png)

1. **switch_on** 의도를 선택합니다. **데이터 레이블 지정** 페이지로 이동됩니다. **의도** 드롭다운에서 **switch_on**을 선택합니다. **switch_on** 의도 옆에 발화 ***turn the light on***을 입력하고 **Enter** 키를 눌러 이 발화를 목록에 제출합니다.

    ![발화 아래에 “turn the light on”을 입력하여 학습 집합에 발화를 추가합니다.](media/conversational-language-understanding/add-utterance-on.png)

1. 언어 서비스를 사용하려면 언어 모델을 충분히 학습시키기 위해 각 의도에 대해 5개 이상의 다른 발화 예제가 필요합니다. **switch_on** 의도에 5개의 발화 예제를 더 추가합니다.  
    - ***switch on the fan***
    - ***put the fan on***
    - ***조명을 켜 둡니다.***
    - ***switch on the light***
    - ***turn the fan on***

1. 화면 오른쪽의 **학습을 위한 엔터티 레이블 지정** 창에서 **레이블**을 선택한 다음, **엔터티 추가**를 선택합니다. **device**(소문자)를 입력하고, **목록**을 선택하고, **완료**를 선택합니다.

    ![학습 패널의 태그 지정 엔터티에서 태그를 선택하여 엔터티를 추가한 다음 엔터티 추가를 선택합니다.](media/conversational-language-understanding/add-entity.png) 
    ![엔터티 이름 아래에 device를 입력하고 목록을 선택한 다음, 엔터티 추가를 선택합니다.](media/conversational-language-understanding/add-entity-device.png)

1. ***turn the fan on*** 발화에서 단어 “fan”을 강조 표시합니다. 그런 다음, 표시되는 목록의 엔터티 검색 상자에서 **device**를 선택합니다.

    ![발화에서 단어 fan을 강조 표시하고 device를 선택합니다.](media/conversational-language-understanding/switch-on-entity.png)

1. 모든 발화에 대해 동일한 작업을 수행합니다. 나머지 *fan* 또는 *light* 발화를 **device** 엔터티로 레이블 지정합니다. 작업을 마쳤으면 다음과 같은 발화가 있는지 확인한 후 **변경 내용 저장**을 선택합니다.

    | **의도** | **발화** | **엔터티** |
    | --------------- | ------------------ | ------------------ |
    | switch_on   | Put on the fan      | 디바이스 - 팬 선택 |
    | switch_on   | Put on the light    | 디바이스 - 조명 선택 |
    | switch_on   | Switch on the light | 디바이스 - 조명 선택 |
    | switch_on   | Turn the fan on     | 디바이스 - 팬 선택 |
    | switch_on   | Switch on the fan   | 디바이스 - 팬 선택 |
    | switch_on   | Turn the light on   | 디바이스 - 조명 선택 |

    ![완료되면 변경 내용 저장을 선택합니다.](media/conversational-language-understanding/save-changes.png) 

1. 왼쪽 창에서 **스키마 정의**를 클릭하고 **switch_on** 의도가 나열되는지 확인합니다. 그런 다음 **추가**를 클릭하고 이름이 **switch_off**(소문자)인 새 의도를 추가합니다.

    ![스키마 빌드 화면으로 돌아가서 switch_off 의도를 추가합니다.](media/conversational-language-understanding/add-switch-off.png) 

1. **switch_off** 의도를 클릭합니다. **데이터 레이블 지정** 페이지로 이동됩니다. **의도** 드롭다운에서 **switch_off**를 선택합니다. **switch_off** 의도 옆에 ***turn the light off*** 발화를 추가합니다.

1. **switch_off** 의도에 5개의 발화 예제를 더 추가합니다.
    - ***switch off the fan***
    - ***팬을 끈 상태로 둡니다.***
    - ***put the light off***
    - ***turn off the light***
    - ***switch the fan off***

1. 단어 *light* 또는 *fan*을 **device** 엔터티로 레이블 지정합니다. 작업을 마쳤으면 다음과 같은 발화가 있는지 확인한 후 **변경 내용 저장**을 선택합니다.  

    | **의도** | **발화** | **엔터티** | 
    | --------------- | ------------------ | ------------------ |
    | switch_off   | Put the fan off    | 디바이스 - 팬 선택 | 
    | switch_off   | Put the light off  | 디바이스 - 조명 선택 |
    | switch_off   | Turn off the light | 디바이스 - 조명 선택 |
    | switch_off   | Switch the fan off | 디바이스 - 팬 선택 |
    | switch_off   | Switch off the fan | 디바이스 - 팬 선택 |
    | switch_off   | Turn the light off | 디바이스 - 조명 선택 |

### <a name="train-the-model"></a>모델 학습

이제 앱에 Conversational Language 모델을 학습하기 위해 정의한 의도 및 엔터티를 사용할 준비가 되었습니다.

1. Language Studio의 왼쪽에서 **학습 작업**을 선택한 다음, **학습 작업 시작**을 선택합니다. 다음 설정을 사용합니다. 
    - **새 모델 학습**: 선택하고 모델 이름을 선택합니다.
    - **학습 모드**: 표준 학습(무료)
    - **데이터 분할**: 학습 데이터에서 테스트 세트 자동 분할 선택, 기본 백분율 유지
    - 페이지 아래쪽에서 **학습**을 클릭합니다.

1. 학습이 완료되기를 기다립니다. 

### <a name="deploy-and-test-the-model"></a>모델 배포 및 테스트

클라이언트 애플리케이션에서 학습된 모델을 사용하려면 클라이언트 애플리케이션이 새 발화를 보낼 수 있는 엔드포인트로 배포해야 합니다. 그러면 의도 및 엔터티를 예측할 수 있습니다.

1. Language Studio의 왼쪽에서 **모델 배포**를 클릭합니다.

1. 모델 이름을 선택하고 **배포 추가**를 클릭합니다. 다음 설정을 사용합니다.
    - **기존 배포 이름 만들기 또는 선택**: 새 배포 이름 만들기 선택, 고유한 이름 추가
    - **배포 이름에 학습된 모델 할당**: 학습된 모델의 이름 선택
    - **배포** 클릭

    >**팁** 배포 이름을 적어 두세요. 나중에 사용할 수 있습니다. 

1. 모델이 배포되면 페이지 왼쪽에서 **배포 테스트**를 클릭한 다음, **배포 이름** 아래에서 배포된 모델을 선택합니다.

1. 다음 텍스트를 입력한 후 **테스트 실행**을 클릭합니다.

    *조명 켜기*

    ![배포된 모델을 선택한 다음, 텍스트를 입력하고 테스트 실행을 선택하여 모델을 테스트합니다.](media/conversational-language-understanding/test-model.png) 

    반환되는 결과를 검토합니다. 예측된 의도(**switch_on**) 및 예측된 엔터티(**device**)에 대해 모델이 계산한 확률을 나타내는 신뢰도 점수와 함께 예측된 의도 및 엔터티가 포함되는 것을 알 수 있습니다. JSON 탭은 각 잠재적 의도에 대한 비교 신뢰도를 표시합니다(신뢰도 점수가 가장 높은 것이 예측된 의도임).

1. 텍스트 상자를 지우고 텍스트 입력 또는 텍스트 문서 업로드에서 다음 발화로 모델을 테스트합니다.
    - *팬 끄기*
    - *조명을 켜 둡니다.*
    - *팬을 끈 상태로 둡니다.*

## <a name="run-cloud-shell"></a>Cloud Shell 실행

이제 배포된 모델을 사용해 보겠습니다. 이를 위해 Azure의 Cloud Shell에서 실행되는 명령줄 애플리케이션을 사용합니다. 

1. 브라우저 탭에서 Language Studio가 열려 있는 상태로 Azure Portal을 포함하는 브라우저 탭으로 다시 전환합니다.

1. Azure Portal에서 검색 상자 오른쪽 페이지 맨 위에 있는 **[>_]**(*Cloud Shell*) 단추를 선택합니다. 이 단추를 클릭하면 포털 아래쪽에 Cloud Shell 창이 열립니다.

    ![맨 위 검색 상자 오른쪽에 있는 아이콘을 클릭하여 Cloud Shell을 시작합니다.](media/conversational-language-understanding/powershell-portal-guide-1.png)

1. Cloud Shell을 처음 열면 사용할 셸 유형(*Bash* 또는 *PowerShell*)을 선택하라는 메시지가 표시될 수 있습니다. **PowerShell**을 선택합니다. 이 옵션이 표시되지 않으면 단계를 건너뜁니다.  

1. Cloud Shell에 대한 스토리지를 만들라는 메시지가 표시되면 구독이 지정되었는지 확인하고 **스토리지 만들기**를 선택합니다. 그런 다음, 스토리지가 만들어질 때까지 1분 정도 기다립니다. 

    ![확인을 클릭하여 스토리지를 만듭니다.](media/conversational-language-understanding/powershell-portal-guide-2.png)

1. Cloud Shell 창의 왼쪽 위에 표시된 셸 형식이 *PowerShell*로 전환되었는지 확인합니다. *Bash*인 경우 드롭다운 메뉴를 사용하여 *PowerShell*로 전환합니다.

    ![PowerShell로 전환하기 위해 왼쪽 드롭다운 메뉴를 찾는 방법](media/conversational-language-understanding/powershell-portal-guide-3.png) 

1. PowerShell이 시작될 때까지 기다립니다. Azure Portal에 다음 화면이 표시되어야 합니다.  

    ![PowerShell이 시작될 때까지 기다립니다.](media/conversational-language-understanding/powershell-prompt.png) 

## <a name="configure-and-run-a-client-application"></a>클라이언트 애플리케이션 구성 및 실행

이제 클라이언트 애플리케이션을 실행할 미리 작성된 스크립트를 열고 편집해 보겠습니다.

1. 명령 셸에서 다음 명령을 입력하여 샘플 애플리케이션을 다운로드하고 ai-900이라는 폴더에 저장합니다.

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    >**참고** 다른 랩에서 이미 이 명령을 사용하여 *ai-900* 리포지토리를 복제했다면 이 단계를 건너뛰어도 됩니다.

1. 파일은 **ai-900**이라는 폴더에 다운로드됩니다. 이제 이 폴더의 모든 파일을 보고 작업하려고 합니다. 셸에 다음 명령을 입력합니다.

     ```PowerShell
    cd ai-900
    code .
    ```

    이 스크립트가 아래 이미지와 같은 편집기를 여는 방식을 살펴보세요. 

    ![코드 편집기.](media/conversational-language-understanding/powershell-portal-guide-4.png)

1. 왼쪽의 **파일** 창에서 **ai-900** 폴더의 **understand.ps1** 파일을 선택합니다. 이 파일에는 다음과 같이 Conversational Language Understanding 모델을 사용하는 코드가 포함되어 있습니다. 

    ![프로그램을 실행하기 전에 수정하고 저장해야 하는 자격 증명 주위에 상자가 있는 언어 이해 랩의 코드입니다.](media/conversational-language-understanding/understand-code.png)

    코드의 세부 정보에 대해 너무 걱정하지 마세요. 중요한 점은 아래 지침을 통해 파일을 수정하여 학습시킨 언어 모델을 지정한다는 것입니다. 

1. **Language Studio**가 포함된 브라우저 탭으로 다시 전환합니다. 그런 다음, Language Studio에서 **모델 배포** 페이지를 열고 모델을 선택합니다. 그런 다음, **예측 URL 가져오기** 단추를 클릭합니다. 필요한 두 가지 정보는 이 대화 상자에 있습니다.
    - 모델의 엔드포인트 - **예측 URL** 상자에서 엔드포인트를 복사할 수 있습니다.
    - 모델의 키 - 키는 **Ocp-Apim-Subscription-Key** 매개 변숫값으로 **샘플 요청**에 포함되어 있으며 ***0ab1c23de4f56gh7i8901234jkl567m8***과 유사합니다.

1. 엔드포인트 값을 복사한 다음, Cloud Shell이 포함된 브라우저 탭으로 다시 전환하여 코드 편집기에서 붙여넣습니다. 여기서 **YOUR_ENDPOINT**(따옴표로 묶여 있음)를 바꿉니다. 키에 대해 이 프로세스를 반복하고 **YOUR_KEY**를 바꿉니다.

1. 다음으로, **YOUR_PROJECT_NAME**을 프로젝트 이름으로 바꾸고 **YOUR_DEPLOYMENT_NAME**을 배포된 모델 이름으로 바꿉니다. 코드의 첫 번째 줄은 아래 표시되는 것처럼 표시되어야 합니다.

    ```PowerShell
    $endpointUrl="https://some-name.cognitiveservices.azure.com/language/..."
    $key = "0ab1c23de4f56gh7i8901234jkl567m8"
    $projectName = "name"
    $deploymentName = "name"
    ```

1. 편집기 창의 오른쪽 위에서 **...** 단추를 사용하여 메뉴를 열고 **저장**을 선택하여 변경 내용을 저장합니다. 그런 다음, 메뉴를 다시 열고 **편집기 닫기**를 선택합니다.

1. PowerShell 창에서 다음 명령을 입력하여 코드를 실행합니다.

    ```PowerShell
    ./understand.ps1 "Turn on the light"
    ```

1. 결과를 검토합니다. 앱은 의도된 동작이 조명을 켜는 것이라고 예측했어야 합니다.

1. 이제 다른 명령을 시도해 보세요.

    ```PowerShell
    ./understand.ps1 "Switch the fan off"
    ```

1. 이 명령의 결과를 검토합니다. 앱은 의도된 동작이 팬을 끄는 것이라고 예측했어야 합니다.

1. 몇 가지 명령을 추가로 시험해 보세요. 모델에서 지원하도록 학습하지 않은 명령(예: "Hello" 또는 "오븐 켜기")을 포함합니다. 앱은 일반적으로 해당 언어 모델이 정의된 명령을 이해해야 하며, 다른 입력에 대해서는 정상적으로 실패해야 합니다.

>**참고** 매번 **./understand.ps1**로 시작하고 구가 뒤따라야 합니다. 구 주위에 따옴표를 포함합니다.

## <a name="learn-more"></a>자세한 정보

이 간단한 앱은 언어 서비스의 대화형 언어 이해 기능 중 일부만 보여 줍니다. 이 서비스를 사용하여 수행할 수 있는 작업을 자세히 알아보려면 [Conversational Language Understanding 페이지](https://docs.microsoft.com/azure/cognitive-services/language-service/conversational-language-understanding/overview)를 참조하세요. 
