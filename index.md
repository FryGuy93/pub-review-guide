---
layout: home
title: The Leaderboard
---

# 🍻 The Pub Rankings

We've visited **{{ site.data.pubs.size }}** establishments so far. 

### 🏆 Top 10 Establishments
| Pub Name | Overall Score | Cost |
| :--- | :--- | :--- |
{% assign sorted_pubs = site.data.pubs | sort: "Overall (100)" | reverse %}
{% for pub in sorted_pubs limit:10 %}
| **{{ pub.Name }}** | **{{ pub["Overall (100)"] }}%** | {{ pub.Cost }} |
{% endfor %}

<br>

### 📍 Full History
| Pub Name | Date | Overall |
| :--- | :--- | :--- |
{% for pub in site.data.pubs reversed %}
| {{ pub.Name }} | {{ pub.Date }} | {{ pub["Overall (100)"] }}% |
{% endfor %}
