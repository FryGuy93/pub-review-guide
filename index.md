---
layout: home
title: The Pub Dashboard
---

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
  :root { --primary: #005f73; --platinum: #ffd700; --gold: #c0c0c0; --silver: #cd7f32; }
  
  /* Dashboard Cards */
  .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 15px; margin: 20px 0 40px 0; }
  .stat-card { background: white; padding: 20px; border-radius: 12px; border-top: 4px solid var(--primary); text-align: center; box-shadow: 0 4px 12px rgba(0,0,0,0.08); }
  .stat-card h3 { margin: 0; font-size: 0.8rem; text-transform: uppercase; letter-spacing: 1px; color: #666; }
  .stat-card p { margin: 10px 0 0; font-size: 2rem; font-weight: 800; color: var(--primary); }

  /* Chart Styles */
  .chart-section { background: white; padding: 20px; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.08); margin-bottom: 40px; }
  
  /* Table Styles */
  .table-container { overflow-x: auto; background: white; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.08); }
  .pub-table { width: 100%; border-collapse: collapse; min-width: 600px; }
  .pub-table th { background: var(--primary); color: white; padding: 15px; text-align: left; font-weight: 600; }
  .pub-table td { padding: 12px 15px; border-bottom: 1px solid #eee; font-size: 0.95rem; }
  .pub-table tr:hover { background-color: #f9f9f9; }

  /* Badges */
  .badge { padding: 4px 8px; border-radius: 4px; font-size: 0.7rem; font-weight: bold; text-transform: uppercase; }
  .plat-bg { background: var(--platinum); color: #443a00; }
  .gold-bg { background: var(--gold); color: #333; }
</style>

# 🍻 Ian & Ellie's Pub Odyssey

<div class="stats-grid">
  <div class="stat-card">
    <h3>Visits</h3>
    <p>{{ site.data.pubs.size }}</p>
  </div>
  <div class="stat-card">
    <h3>Avg Score</h3>
    {% assign total = 0 %}{% for pub in site.data.pubs %}{% assign total = total | plus: pub["Overall (100)"] %}{% endfor %}
    <p>{{ total | divided_by: site.data.pubs.size }}%</p>
  </div>
  <div class="stat-card">
    <h3>Elite Spots</h3>
    {% assign elite = site.data.pubs | where_exp: "item", "item['Overall (100)'] >= 75" %}
    <p>{{ elite.size }}</p>
  </div>
</div>

<div class="chart-section">
  <h3>Score Trends Over Time</h3>
  <canvas id="scoreChart" height="100"></canvas>
</div>

### 🏆 The Leaderboard
<div class="table-container">
  <table class="pub-table">
    <thead>
      <tr>
        <th>Establishment</th>
        <th>Date</th>
        <th>Taste</th>
        <th>Overall</th>
        <th>Cost</th>
        <th>Award</th>
      </tr>
    </thead>
    <tbody>
      {% assign sorted_pubs = site.data.pubs | sort: "Overall (100)" | reverse %}
      {% for pub in sorted_pubs limit:20 %}
      <tr>
        <td><strong>{{ pub.Name }}</strong></td>
        <td>{{ pub.Date }}</td>
        <td>{{ pub["Taste (20)"] }}/20</td>
        <td><strong>{{ pub["Overall (100)"] }}%</strong></td>
        <td>{{ pub.Cost }}</td>
        <td>
          {% if pub["Overall (100)"] >= 75 %}
            <span class="badge plat-bg">Platinum</span>
          {% elsif pub["Overall (100)"] >= 65 %}
            <span class="badge gold-bg">Gold</span>
          {% endif %}
        </td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
</div>

<script>
  const ctx = document.getElementById('scoreChart').getContext('2d');
  new Chart(ctx, {
    type: 'line',
    data: {
      labels: [{% for pub in site.data.pubs %}"{{ pub.Date }}",{% endfor %}],
      datasets: [{
        label: 'Overall %',
        data: [{% for pub in site.data.pubs %}{{ pub["Overall (100)"] | default: 0 }},{% endfor %}],
        borderColor: '#005f73',
        backgroundColor: 'rgba(0, 95, 115, 0.1)',
        fill: true,
        tension: 0.4,
        pointRadius: 2
      }]
    },
    options: {
      responsive: true,
      scales: {
        y: { beginAtZero: false, min: 20, max: 100 }
      },
      plugins: {
        legend: { display: false }
      }
    }
  });
</script>
