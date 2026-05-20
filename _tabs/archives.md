---
layout: page
title: Archives
icon: fas fa-archive
order: 4
---

<div id="archives-cyber">
  {% for post in site.posts %}
    {% capture cur_year %}{{ post.date | date: '%Y' }}{% endcapture %}

    {% if cur_year != last_year %}
      <div class="year-block">
        <span class="year-label">{{ cur_year }}</span>
        <div class="year-circle"></div>
      </div>
      {% assign last_year = cur_year %}
    {% endif %}

    <div class="archive-row-cyber">
      <div class="meta-side">
        <span class="date-txt">{{ post.date | date: "%d %b" }}</span>
        <div class="line-v"></div>
        <div class="dot-v"></div>
      </div>
      <a href="{{ post.url | relative_url }}" class="link-txt">
        {{ post.title }}
      </a>
    </div>
  {% endfor %}
</div>


<style>
  #archives-cyber {
      padding: 10px 0;
      font-family: 'JetBrains Mono', monospace;
  }

  /* --- L'ANNÉE --- */
  .year-block {
      display: flex;
      align-items: center;
      margin: 25px 0 15px 0;
  }

  .year-label {
      font-size: 1.3rem;
      color: #999;
      margin-right: 15px;
      font-weight: bold;
  }

  .year-circle {
      width: 10px;
      height: 10px;
      border: 2px solid #555;
      border-radius: 50%;
  }

  /* --- RANGÉE ARTICLE --- */
  .archive-row-cyber {
      display: flex;
      align-items: center;
      padding: 6px 10px;
      transition: all 0.2s ease;
      border-radius: 4px;
      margin-left: -10px;
  }

  /* L'effet de survol (fond sombre, texte rouge) */
  .archive-row-cyber:hover {
      background: rgba(255, 255, 255, 0.03);
  }

  .meta-side {
      display: flex;
      align-items: center;
      min-width: 90px;
      position: relative;
  }

  .date-txt {
      font-size: 0.8rem;
      color: #666;
      margin-right: 20px;
  }

  /* La ligne verticale */
  .line-v {
      position: absolute;
      left: 60px;
      top: -15px;
      bottom: -15px;
      width: 2px;
      background: #333;
  }

  .dot-v {
      width: 6px;
      height: 6px;
      background: #555;
      border-radius: 50%;
      z-index: 2;
      margin-left: -4px;
  }

  /* --- LIEN --- */
  .link-txt {
      color: #888 !important; /* Gris par défaut */
      text-decoration: none !important;
      font-size: 0.95rem;
      margin-left: 25px;
      transition: all 0.2s;
  }

  /* Couleur rouge vif au survol de la ligne */
  .archive-row-cyber:hover .link-txt {
      color: #ff3333 !important;
      text-shadow: 0 0 8px rgba(255, 51, 51, 0.3);
  }

  .archive-row-cyber:hover .dot-v {
      background: #ff3333;
      box-shadow: 0 0 8px #ff3333;
  }

  /* Adaptation Dark Mode */
  html[data-mode="dark"] #archives-cyber {
      color: #eee;
  }
</style>