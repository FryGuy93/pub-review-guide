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

  .chart-section { 
    background: var(--card-bg); padding: 25px; border-radius: 12px; 
    box-shadow: 0 4px 12px rgba(0,0,0,0.05); margin-bottom: 30px; 
  }

  .pub-table { width: 100%; border-collapse: collapse; background: white; border-radius: 12px; overflow: hidden; margin-top: 20px; }
  .pub-table th { background: var(--primary); color: white; padding: 15px; text-align: left; }
  .pub-table td { padding: 12px 15px; border-bottom: 1px solid #eee; }
  .total-cell { font-weight: bold; color: var(--primary); }
</style>

# 🍻 Ian & Ellie's Pub Reviews

<div class="stats-grid">
  <div class="stat-card"><h3>Total Visits</h3><p>{{ site.data.pubs.size }}</p></div>
  <div class="stat-card"><h3>Top Score</h3><p>86%</p></div>
  <div class="stat-card"><h3>Avg Score</h3><p>64%</p></div>
</div>

<div class="chart-section">
  <h3 style="margin-top:0; color:var(--primary);">📊 Scoring Weights</h3>
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

<table class="pub-table">
  <thead>
    <tr>
      <th>Establishment</th>
      <th>Date</th>
      <th>Taste</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
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
      <tr>
        <td><strong>{{ pub.Name }}</strong></td>
        <td>{{ pub.Date }}</td>
        <td>{{ t }}/20</td>
        <td class="total-cell">{{ total }}%</td>
      </tr>
    {% endfor %}
  </tbody>
</table>
