---
title: 온라인 호스팅 지침
permalink: index.html
layout: home
---

# Azure Data Fundamentals 연습

이러한 실습 연습은 [Microsoft Learn](https://docs.microsoft.com/training/)의 교육 콘텐츠를 지원하도록 설계되었습니다.

이 연습을 완료하려면 Microsoft Azure 구독이 필요합니다. [https://azure.microsoft.com](https://azure.microsoft.com)에서 무료 평가판에 등록할 수 있습니다.

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| 연습 |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
