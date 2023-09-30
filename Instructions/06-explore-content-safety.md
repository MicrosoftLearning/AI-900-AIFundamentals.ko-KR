---
lab:
  title: 콘텐츠 안전 스튜디오 살펴보기
---

Content Safety Studio를 사용하면 텍스트 및 이미지 콘텐츠를 조정하는 방법을 탐색할 수 있습니다. 샘플 텍스트 또는 이미지에서 테스트를 실행하고 각 범주에 대해 안전에서 높음까지의 심각도 점수를 얻을 수 있습니다. 콘텐츠 안전 AI 서비스의 작동 방식과 가능한 기능을 빠르게 확인할 수 있습니다. 

이 랩 연습에서는 Azure Portal 다중 서비스 Azure AI Services 리소스를 만들고 해당 엔드포인트 및 키를 검사합니다. 그런 다음 Content Safety Studio를 사용하여 콘텐츠 안전 AI 서비스의 기능을 탐색합니다. 

## AI Services 리소스 만들기

1.  다른 브라우저 탭의 [https://portal.azure.com](https://portal.azure.com?azure-portal=true)에서 Azure Portal을 열고 Microsoft 계정을 사용하여 로그인합니다.
1.  **&#65291;리소스 만들기** 단추를 클릭하고 *Azure AI 서비스를 검색합니다*. **Azure AI 서비스** 계획 **만들기**를 선택합니다. 페이지로 이동하여 Azure AI 서비스 리소스를 만듭니다. 다음 설정을 사용하여 구성합니다.
- **구독**: Azure 구독.
- **리소스 그룹**: 적합한 리소스 그룹을 선택하거나 만듭니다.
- **지역**: 사용 가능한 지역을 선택합니다.
- **이름**: 고유한 이름을 입력합니다.
- **가격 책정 계층**: F0 
2.  리소스를 검토하고 만들고 배포가 완료되기를 기다립니다. 

## Content Safety Studio에 리소스 연결 
별도의 브라우저 탭에서 Content Safety Studio를 열고 로그인합니다. 시작 화면이 표시됩니다.

1.  오른쪽 위 메뉴에서 설정 코그를 클릭합니다.
2.  방금 만든 Azure AI 서비스 리소스를 선택한 다음 리소스 사용을 클릭합니다.
3.  필요한 경우 스크롤하여 리소스의 엔드포인트 및 키를 봅니다. Azure Portal에서 검사 경우 리소스를 Content Safety 스튜디오와 성공적으로 연결했음을 보여 주는 리소스의 엔드포인트 및 키임을 알 수 있습니다.
4.  콘텐츠 안전 스튜디오를 클릭하여 홈 페이지로 돌아갑니다. 조정 텍스트 콘텐츠에서 사용해 보기를 클릭합니다.
5.  간단한 테스트 실행에서 안전한 콘텐츠를 클릭합니다. 아래 상자에 텍스트가 표시됩니다. 
6.  테스트 실행을 클릭합니다. 
7.  결과 패널에서 결과를 검사합니다. 안전에서 높음까지의 4가지 심각도 수준과 4가지 유형의 유해한 콘텐츠가 있습니다. Content Safety AI 서비스는 이 샘플을 허용 가능한 것으로 간주하나요? 
8.  이제 다른 샘플을 사용해 보세요. 철자가 틀린 폭력적인 콘텐츠 아래에서 텍스트를 선택합니다. 콘텐츠가 아래 상자에 표시되는지 확인합니다.
9.  테스트 실행을 클릭하고 아래 결과 패널에서 결과를 검사합니다. 이 샘플은 허용 가능한가요? 그렇지 않다면 그 이유는 무엇인가요?

제공된 모든 샘플에서 테스트를 실행한 다음 결과를 검사할 수 있습니다.

완료되면 Azure Portal에서 Azure AI 서비스 리소스를 삭제합니다. 