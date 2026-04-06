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
    background: white; padding: 20px; border-radius: 12px; text-align: center; 
    box-shadow: 0 4px 12px rgba(0,0,0,0.05); border-top: 5px solid var(--primary);
  }

  .chart-section { 
    background: white; padding: 25px; border-radius: 12px; 
    box-shadow: 0 4px 12px rgba(0,0,0,0.05); margin-bottom: 30px; 
  }

  /* Expanded Table styling */
  .table-scroll { overflow-x: auto; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.05); }
  .pub-table { width: 100%; border-collapse: collapse; background: white; min-width: 1000px; }
  .pub-table th { background: var(--primary); color: white; padding: 12px 8px; text-align: center; font-size: 0.85rem; }
  .pub-table th.name-col { text-align: left; padding-left: 15px; }
  .pub-table td { padding: 10px 8px; border-bottom: 1px solid #eee; text-align: center; font-size: 0.85rem; }
  .pub-table td.name-col { text-align: left; padding-left: 15px; }
  
  .total-cell { font-weight: bold; color: var(--primary); background: #e9f5f8; }
  tr:hover { background-color: #f1f8f9; }
  
  .low-score { color: #ae2012; } /* Highlights scores of 3 or less */
</style>

# 🍻 Ian & Ellie's Pub Reviews

<div class="stats-grid">
  <div class="stat-card"><h3>Total Visits</h3><p>{{ site.data.pubs.size }}</p></div>
  <div class="stat-card"><h3>Top Score</h3><p>86%</p></div>
  <div class="stat-card"><h3>Avg Score</h3><p>64%</p></div>
</div>

### 🏆 Complete Review Leaderboard

<div class="table-scroll">
<table class="pub-table">
  <thead>
    <tr>
      <th class="name-col">Establishment</th>
      <th>Date</th>
      <th>Taste (20)</th>
      <th>Portion (10)</th>
      <th>Pres. (20)</th>
      <th>Serv. (10)</th>
      <th>Atmos. (10)</th>
      <th>Loc. (10)</th>
      <th>Fac. (10)</th>
      <th>Clean. (10)</th>
      <th style="background: #003d4d;">TOTAL</th>
    </tr>
  </thead>
  <tbody>
    {% assign sorted_pubs = site.data.pubs | sort: "Date" | reverse %}
    {% for pub in sorted_pubs %}
      {% assign t = pub.Taste | plus: 0 %}
      {% assign p = pub.Portion | plus: 0 %}
      {% assign pr = pub.Presentation | plus: 0 %}
      {% assign s = pub.Service | plus: 0 %}
      {% assign a = pub.Atmosphere | plus: 0 %}
      {% assign l = pub.Location | plus: 0 %}
      {% assign f = pub.Facilities | plus: 0 %}
      {% assign c = pub.Cleanliness | plus: 0 %}
      {% assign total = t | plus: p | plus: pr | plus: s | plus: a | plus: l | plus: f | plus: c %}
      <tr>
        <td class="name-col"><strong>{{ pub.Name }}</strong></td>
        <td>{{ pub.Date }}</td>
        <td>{{ t }}</td>
        <td>{{ p }}</td>
        <td>{{ pr }}</td>
        <td {% if s <= 3 %}class="low-score"{% endif %}>{{ s }}</td>
        <td {% if a <= 3 %}class="low-score"{% endif %}>{{ a }}</td>
        <td>{{ l }}</td>
        <td>{{ f }}</td>
        <td>{{ c }}</td>
        <td class="total-cell">{{ total }}%</td>
      </tr>
    {% endfor %}
  </tbody>
</table>
</div>

<br>

<div class="chart-section">
  <h3 style="margin-top:0; color:var(--primary);">📊 Scoring Breakdown</h3>
  <div class="mermaid">
  pie title Maximum Points per Category
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
