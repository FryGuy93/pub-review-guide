---
layout: home
title: Pub Review Dashboard
---

<style>
  :root { --primary: #005f73; --bg: #f8f9fa; --card-bg: #ffffff; }
  
  body { background-color: var(--bg); font-family: "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
  
  .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 20px; margin: 20px 0; }
  
  .stat-card { 
    background: var(--card-bg); 
    padding: 20px; 
    border-radius: 12px; 
    text-align: center; 
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    border-top: 5px solid var(--primary);
  }
  
  .stat-card h3 { font-size: 0.8rem; color: #666; text-transform: uppercase; margin-bottom: 5px; }
  .stat-card p { font-size: 1.8rem; font-weight: bold; color: var(--primary); margin: 0; }

  .chart-section { 
    background: var(--card-bg); 
    padding: 20px; 
    border-radius: 12px; 
    box-shadow: 0 4px 12px rgba(0,0,0,0.05); 
    margin-bottom: 30px; 
  }

  table { width: 100%; border-collapse: collapse; background: white; border-radius: 10px; overflow: hidden; }
  th { background: var(--primary); color: white; padding: 15px; text-align: left; }
  td { padding: 12px 15px; border-bottom: 1px solid #eee; }
  tr:hover { background-color: #f1f1f1; }
</style>

# 🍻 Ian & Ellie's Pub Odyssey

<div class="stats-grid">
  <div class="stat-card">
    <h3>Total Visits</h3>
    <p>{{ site.data.pubs.size }}</p>
  </div>
  <div class="stat-card">
    <h3>Top Rated</h3>
    <p>86%</p>
  </div>
</div>

<div class="chart-section">
  <h3>🏆 Score Distribution</h3>
```mermaid
pie title Category Weightings
    "Taste" : 20
    "Presentation" : 20
    "Atmosphere" : 10
    "Other" : 50
