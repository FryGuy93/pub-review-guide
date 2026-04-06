---
layout: home
title: Pub Review Dashboard
---

# 🍻 Ian & Ellie's Pub Reviews

We've visited **{{ site.data.pubs.size }}** establishments. Here is the leaderboard based on our 8-category scoring system.

<div style="display: flex; gap: 20px; margin-bottom: 30px;">
  <div style="background: #f0f4f8; padding: 20px; border-radius: 10px; flex: 1; text-align: center;">
    <h3>Total Visits</h3>
    <p style="font-size: 24px; font-weight: bold; color: #005f73;">{{ site.data.pubs.size }}</p>
  </div>
</div>

### 🏆 Calculated Rankings
| Pub Name | Date | Taste | Atmos | Total Score |
| :--- | :--- | :--- | :--- | :--- |
{% for pub in site.data.pubs %}
  {% assign t = pub.Taste | plus: 0 %}
  {% assign p = pub.Portion | plus: 0 %}
  {% assign pr = pub.Presentation | plus: 0 %}
  {% assign s = pub.Service | plus: 0 %}
  {% assign a = pub.Atmosphere | plus: 0 %}
  {% assign l = pub.Location | plus: 0 %}
  {% assign f = pub.Facilities | plus: 0 %}
  {% assign c = pub.Cleanliness | plus: 0 %}
  {% assign total = t | plus: p | plus: pr | plus: s | plus: a | plus: l | plus: f | plus: c %}
| **{{ pub.Name }}** | {{ pub.Date }} | {{ t }}/20 | {{ a }}/10 | **{{ total }}/100** |
{% endfor %}

### 📊 Scoring Weights
```mermaid
pie title How we calculate the 100%
    "Taste & Presentation" : 40
    "Portion" : 10
    "Service" : 10
    "Atmosphere" : 10
    "Location" : 10
    "Facilities" : 10
    "Cleanliness" : 10
