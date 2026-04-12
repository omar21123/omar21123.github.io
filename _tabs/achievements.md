---
layout: page
title: Achievements
icon: fas fa-trophy
order: 5
---

<div class="achievements-list">
  
  <div class="achievement-card">
    <div class="ach-icon"><i class="fas fa-medal"></i></div>
    <div class="ach-content">
      <h3></h3>
      <p></p>
    </div>
  </div>

  <div class="achievement-card">
    <div class="ach-icon"><i class="fas fa-flag"></i></div>
    <div class="ach-content">
      <h3></h3>
      <p>CTF Team Competition - ENSA Fès</p>
    </div>
  </div>

</div>

{% include cursor.html %}

<style>
  .achievement-card {
    display: flex;
    align-items: center;
    gap: 20px;
    background: rgba(136, 136, 136, 0.05);
    border: 1px solid rgba(136, 136, 136, 0.2);
    padding: 20px;
    border-radius: 12px;
    margin-bottom: 15px;
    transition: all 0.3s ease;
  }

  .achievement-card:hover {
    border-color: #ff3333;
    transform: translateX(10px);
    background: rgba(255, 51, 51, 0.02);
  }

  .ach-icon {
    font-size: 2rem;
    color: #ff3333;
  }

  .ach-content h3 {
    margin: 0;
    font-size: 1.2rem;
    color: var(--text-color);
  }

  .ach-content p {
    margin: 5px 0 0;
    color: #888;
    font-family: monospace;
  }
</style>