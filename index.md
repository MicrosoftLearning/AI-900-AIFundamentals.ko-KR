---
title: 온라인 호스팅 지침
permalink: index.html
layout: home
ms.openlocfilehash: b85af520a10e63a2f9a5696db03bfd946aff968f
ms.sourcegitcommit: 1ef64e3008a439d0d0bb3d93a27d3df68d3d64a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/17/2022
ms.locfileid: "140688695"
---
# <a name="azure-ai-fundamentals-exercises"></a>Azure AI 기본 사항 연습

아래 링크를 사용하여 Microsoft 과정 [AI-900 *Microsoft Azure AI Fundamentals*](https://docs.microsoft.com/learn/certifications/courses/ai-900t00)에 대한 실습 랩 연습을 완료합니다.

이 연습을 완료하려면 Microsoft Azure 구독이 필요합니다. 강사가 Microsoft Azure 구독을 제공하지 않은 경우 [https://azure.microsoft.com](https://azure.microsoft.com)에서 무료 평가판에 등록할 수 있습니다.

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| 연습 |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
