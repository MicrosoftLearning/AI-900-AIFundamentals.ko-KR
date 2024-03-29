---
lab:
  title: Bing에서 Copilot을 사용하여 생성 AI 살펴보기
---

연습 - Bing Copilot를 사용하여 생성형 AI 살펴보기 

## 시작하기 전에
개인 MSA(Microsoft 계정). 없는 경우 signup.live.com[ 이동하여 ](https://signup.live.com/signup?azure-portal=true)등록합니다.

# Bing을 사용하여 생성 AI 살펴보기

1. Bing.com[ 열고 ](https://www.bing.com?azure-portal=true)개인 Microsoft 계정으로 로그인합니다.

**참고**: 회사 또는 학교 계정으로 로그인할 수 있지만 개인 계정 로그인하는 것과는 약간 다른 사용자 환경이 표시됩니다. 회사 또는 학교 계정을 사용하면 Bing Enterprise 채팅이 표시됩니다. 

1. 화면 상단의 메뉴에서 **내보내기**를 선택합니다. 채팅을 통해 Bing Copilot로 이동하여 생성 AI를 사용하여 검색 결과를 제공합니다. 즉, 기존 콘텐츠를 반환하는 검색과 달리 Bing Copilot는 자연어 모델링 및 웹 정보에 따라 새로운 응답을 결합할 수 있습니다.  
    
1. 화면 아래쪽에 아무 것도** 묻는 창**이 표시됩니다. 창에 프롬프트를 입력할 때 Bing Copilot는 전체 대화 스레드를 사용하여 응답을 반환합니다. 예를 들어 여행에 대해 일련의 질문을 해 보겠습니다. 

## 프롬프트를 사용하여 응답 생성

1. 프롬프트를 입력합니다 `What are 3 pros and cons of traveling in the winter?`. 검색: *...* 및 *생성 중이* 응답 앞에 표시됩니다. 모델은 검색된 응답을 접지 정보로 사용하여 원래 응답을 생성합니다. 응답의 끝에는 해당 원본에 대한 링크가 포함되어 있습니다. 

![프로용 글머리 기호 3개와 단점용 글머리 기호 3개가 있는 여행 프롬프트에 대한 Bing copilot의 응답 스크린샷.](../media/generative-ai/bing-copilot-response-traveling.png) 

**참고**: **생성 중...* 메시지 또는 글머리 기호 목록 응답이 표시되지 않으면 아직 Bing Copilot가 작동하는 것을 볼 수 없습니다. 로그인 메뉴로 돌아가서 사용 중인 현재 계정을 개인 계정 연결해야 합니다. 
 
1. 프롬프트를 입력합니다 `Find me 3 more pros`. 이 프롬프트의 의미는 아직 나열되지 않은 겨울에 여행하는 3 가지 더 긍정적 인 이유를 보고 싶다는 것입니다. 이 프롬프트를 사용하면 Bing Copilot에게 검색만으로는 수행되지 않는 두 가지 작업을 수행하도록 요청합니다. 이전 채팅 응답을 사용하여 새 응답에 반환된 내용을 제외하고 명시적으로 명시하지 않고 이전 채팅의 항목을 사용합니다. 

1. 프롬프트를 입력합니다 `Where are 3 places I can go to find fewer crowds?`. 

**참고**: Bing Copilot는 관련 응답을 제공할 수 있지만 계속되면 대화 스레드의 이전 "추억"을 삭제할 수 있습니다. 결과적으로, 당신이 얻을 응답은 겨울에 여행과 직접 관련이없을 수 있습니다. 이는 주로 토큰 입력 제한과 관련이 있습니다. 채팅이 대화의 이전 부분을 "기억"할 때 대화에서 일정량의 토큰을 저장했기 때문입니다. 새 프롬프트 및 응답을 통해 새 토큰이 도입되면 채팅에서 이전 토큰을 삭제합니다. 

1. 채팅 창 옆의 **새 토픽 단추는 새 토픽** 응답이 이전 항목을 기반으로 하지 않도록 이전 대화 스레드를 지우는 데 유용한 Bing Copilot입니다. 채팅 창 옆에 있는 **새 토픽** 아이콘을 사용하여 메시지 기록을 지울 수 있습니다. 

## 이미지 세대

1. 이제 이미지 생성의 예를 살펴보겠습니다. 프롬프트를 입력합니다 `Create an image of an elephant eating a hamburger`. Bing Copilot가 응답을 반환하기 전에 만들*려는 메시지가 *나타납니다. 

![햄버거를 먹는 코끼리의 스크린샷.](../media/generative-ai/dall-e-elephant.png)

중요한 것은 응답이 비슷하지만 동일하지는 않을 수 있다는 점입니다. 응답이 다양하기 때문입니다.  

1. 응답에는 아래쪽에 "DALL-E로 구동됨"이라는 텍스트가 있습니다. 자연어 입력에서 이미지를 생성할 때 DALL-E가 큰 언어 모델을 기반으로 하는 방법을 고려합니다. 

1. 화면의 오른쪽 위 모서리에 있는 Microsoft Bing 아이콘을 클릭하여 Bing Copilot의 채팅으로 돌아갑니다. 

## 잘못된 코드 생성

1. 이제 코드 생성 및 번역의 예를 살펴보겠습니다. 프롬프트를 입력합니다 `Use Python to create a list`. 

1. 메시지가 표시되면 `Translate that into C#`를 입력합니다. Bing Copilot가 대화 기록을 참조하는 것을 알고 있기 때문에 "그"가 무엇인지 지정할 필요가 없습니다. 

## Bonus 

1. 프롬프트를 입력합니다 `What are 3 examples of generative AI helping people?`. 당신은 당신의 자신의 부조종사 아이디어를 브레인 스토밍하는 방법으로 이것을 사용할 수 있습니다!  

