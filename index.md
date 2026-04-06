---
layout: home
title: Pub Review Dashboard
---

<script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
<script>mermaid.initialize({startOnLoad:true});</script>

<style>
  :root { --primary: #005f73; --bg: #f8f9fa; --card-bg: #ffffff; }
  body { background-color: var(--bg); font-family: "Segoe UI", Roboto, Helvetica, sans-serif; }
  
  .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 20px; margin: 20px 0; }
  .stat-card { 
    background: var(--card-bg); padding: 20px; border-radius: 12px; text-align: center; 
    box-shadow: 0 4px 12px rgba(0,0,0,0.05); border-top: 5px solid var(--primary);
  }
  .stat-card h3 { font-size: 0.7rem; color: #666; text-transform: uppercase; margin: 0; }
  .stat-card p { font-size: 2rem; font-weight: bold; color: var(--primary); margin: 5px 0 0; }

  .chart-section { 
    background: var(--card-bg); padding: 25px; border-radius: 12px; 
    box-shadow: 0 4px 12px rgba(0,0,0,0.05); margin-bottom: 30px; 
  }

  .table-container { background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 4px 12px rgba(0,0,0,0.05); }
  table { width: 100%; border-collapse: collapse; }
  th { background: var(--primary); color: white; padding: 15px; text-align: left; font-size: 0.9rem; }
  td { padding: 12px 15px; border-bottom: 1px solid #eee; font-size: 0.9rem; }
  tr:hover { background-color: #f8f9fa; }
  .total-cell { font-weight: bold; color: var(--primary); }
</style>

# 🍻 Ian & Ellie's Pub Odyssey

<div class="stats-grid">
  <div class="stat-card">
    <h3>Total Visits</h3>
    <p>{{ site.data.pubs.size }}</p>
  </div>
  <div class="stat-card">
    <h3>Top Score</h3>
    <p>86%</p>
  </div>
  <div class="stat-card">
    <h3>Avg Score</h3>
    <p>64%</p>
  </div>
</div>

<div class="chart-section">
  <h3 style="margin-top:0; color:var(--primary);">📊 Scoring Distribution</h3>
  <div class="mermaid">
  pie title 100% Score Weightings
    "Taste" : 20
    "Presentation" : 20
    "Atmosphere" : 10
    "Portion" : 10
    "Service" : 10
    "Location" : 10
    "Facilities" : 10
    "Cleanliness" : 10
  </div>
</div>

### 🏆 The Leaderboard
<div class="table-container">
| Establishment | Date | Taste | Total |
| :--- | :--- | :--- | :--- |
{% for pub in site.data.pubs limit:20 %}
  {% assign t = pub["Taste \n(20)"] | plus: 0 %}
  {% assign p = pub["Portion \n(10)"] | plus: 0 %}
  {% assign pr = pub["Presentation\n(20)"] | plus: 0 %}
  {% assign s = pub["Service \n(10)"] | plus: 0 %}
  {% assign a = pub["Atmosphere\n(10)"] | plus: 0 %}
  {% assign l = pub["Location\n(10)"] | plus: 0 %}
  {% assign f = pub["Facilities\n(10)"] | plus: 0 %}
  {% assign c = pub["Cleanliness \n(10)"] | plus: 0 %}
  {% assign total = t | plus: p | plus: pr | plus: s | plus: a | plus: l | plus: f | plus: c %}
| **{{ pub.Name }}** | {{ pub.Date }} | {{ t }}/20 | <span class="total-cell">{{ total }}%</span> |
{% endfor %}
</div>

<br>

### 📈 Visit Timeline
<div class="chart-section">
  <div class="mermaid">
  graph LR
    A[Start: 2017] --> B[Current: 2025]
    B --> C[Total Reviews: {{ site.data.pubs.size }}]
  </div>
</div>
