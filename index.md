---
title: 온라인 호스팅 지침
permalink: index.html
layout: home
---

# Azure AI 기본 사항 연습

이 리포지토리에는 Microsoft 과정 [AI-900 *Microsoft Azure 인공 지능*](https://docs.microsoft.com/ko-kr/learn/certifications/courses/ai-900t00)에 대한 실습 랩 연습 그리고 Microsoft Learn에서 이에 해당하는 자기 주도적 모듈이 포함되어 있습니다. [Azure에서 인공 지능 시작하기](https://docs.microsoft.com/learn/paths/get-started-with-artificial-intelligence-on-azure/), [Azure Machine Learning으로 코드 없는 예측 모델 만들기](https://docs.microsoft.com/ko-kr/learn/paths/create-no-code-predictive-models-azure-machine-learning/), [Microsoft Azure에서 Computer Vision 탐구](https://docs.microsoft.com/learn/paths/explore-computer-vision-microsoft-azure/), [자연어 처리 탐구](https://docs.microsoft.com/learn/paths/explore-natural-language-processing/), 및 [대화식 AI 탐구](https://docs.microsoft.com/learn/paths/explore-conversational-ai/). 연습은 학습 자료와 함께 진행할 수 있으며, 설명되어 있는 기술을 사용하여 연습할 수 있게 도와줍니다. 

이 연습을 완료하려면 Microsoft Azure 구독이 필요합니다. 강사가 구독을 제공하지 않은 경우 [https://azure.microsoft.com](https://azure.microsoft.com)에서 등록을 하면 무료 평가판을 받을 수 있습니다.

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| 연습 |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
