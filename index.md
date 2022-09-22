---
title: 온라인 호스팅 지침
permalink: index.html
layout: home
---

# <a name="azure-ai-fundamentals-exercises"></a>Azure AI 기본 사항 연습

이러한 실습 연습은 [Microsoft Learn](https://docs.microsoft.com/training/)의 교육 콘텐츠를 지원하도록 설계되었습니다.

To complete these exercises, you'll need a Microsoft Azure subscription. You can sign up for a free trial at <bpt id="p1">[</bpt><ph id="ph1">https://azure.microsoft.com</ph><ept id="p1">](https://azure.microsoft.com)</ept>.

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| 연습 |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
