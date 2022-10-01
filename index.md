---
title: 온라인 호스팅 지침
permalink: index.html
layout: home
ms.openlocfilehash: 86fa2da9bfa9e4d7edb0c853f77e95fe69e97411
ms.sourcegitcommit: 3fc8440b350b498c2f50ab4ce531a0f906792584
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2022
ms.locfileid: "147866009"
---
# <a name="azure-ai-fundamentals-exercises"></a>Azure AI 기본 사항 연습

이러한 실습 연습은 [Microsoft Learn](https://docs.microsoft.com/training/)의 교육 콘텐츠를 지원하도록 설계되었습니다.

이 연습을 완료하려면 Microsoft Azure 구독이 필요합니다. [https://azure.microsoft.com](https://azure.microsoft.com)에서 무료 평가판에 등록할 수 있습니다.

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| 연습 |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
