---
layout: home
title: Pub Reviews
---

# 🍻 The Pub Rankings

Welcome to the definitive guide! We've reviewed **{{ site.data.pubs.size }}** visits so far. 

### 🏆 Top 10 Establishments
Here are our highest-rated spots to date:

| Rank | Pub Name | Date | Overall Score | Cost |
| :--- | :--- | :--- | :--- | :--- |
{% assign sorted_pubs = site.data.pubs | sort: "Overall (100)" | reverse %}
{% for pub in sorted_pubs limit:10 %}
| {{ pub.Rank | default: "-" }} | **{{ pub.Name }}** | {{ pub.Date }} | **{{ pub["Overall (100)"] }}%** | {{ pub.Cost }} |
{% endfor %}

<br>

### 📍 All Reviews
*Sorted by our most recent visits*

| Pub Name | Date | Taste | Atmosphere | Overall |
| :--- | :--- | :--- | :--- | :--- |
{% for pub in site.data.pubs reversed %}
| {{ pub.Name }} | {{ pub.Date }} | {{ pub["Taste (20)"] }}/20 | {{ pub["Atmosphere(10)"] }}/10 | {{ pub["Overall (100)"] }}% |
{% endfor %}
