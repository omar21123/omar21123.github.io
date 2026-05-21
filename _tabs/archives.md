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
        <div class="year-circle-wrapper">
          <div class="year-circle"></div>
        </div>
      </div>
      {% assign last_year = cur_year %}
    {% endif %}

    <div class="archive-row-cyber">
      <div class="date-side">
        <span class="date-day">{{ post.date | date: "%d" }}</span>
        <span class="date-month">{{ post.date | date: "%b" }}</span>
      </div>

      <div class="timeline-axis">
        <div class="dot-v"></div>
      </div>

      <a href="{{ post.url | relative_url }}" class="link-txt">
        {{ post.title }}
      </a>
    </div>
  {% endfor %}
</div>

<style>
  /* --- BASE WRAPPER SETTINGS --- */
  #archives-cyber {
    padding: 20px 0;
    font-family: 'JetBrains Mono', 'Courier New', monospace;
    position: relative;
    /* Uses Chirpy's native dynamic background variable */
    background-color: var(--main-bg); 
  }

  /* --- TIMELINE VERTICAL AXIS --- */
  #archives-cyber::before {
    content: '';
    position: absolute;
    left: 114px; /* Matches line alignment precisely */
    top: 0;
    bottom: 0;
    width: 2px;
    background: var(--timeline-color, #3a3a3a); /* Dynamic dynamic theme track line */
    z-index: 1;
  }

  /* --- YEAR SEGMENTATION NODES --- */
  .year-block {
    display: flex;
    align-items: center;
    height: 44px;
    position: relative;
    z-index: 2;
  }

  .year-label {
    font-size: 1.6rem;
    color: var(--text-muted-color, #757575);
    width: 90px;
    text-align: right;
    font-weight: 700;
    letter-spacing: -0.5px;
  }

  .year-circle-wrapper {
    width: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .year-circle {
    width: 12px;
    height: 12px;
    border: 3px solid var(--timeline-node-bg, #666666);
    background: var(--main-bg);
    border-radius: 50%;
  }

  /* --- POST ROWS LOGIC --- */
  .archive-row-cyber {
    display: flex;
    align-items: center;
    height: 44px;
    position: relative;
    z-index: 2;
    border-bottom: 1px solid var(--main-border-color, rgba(0,0,0,0.05));
  }

  /* Alternating Zebra Striping adapted for both themes */
  .archive-row-cyber:nth-of-type(even) {
    background: var(--checkerboard-color, rgba(0, 0, 0, 0.02));
  }

  /* Hover Overlay Background Highlight */
  .archive-row-cyber:hover {
    background: var(--trending-tag-hover-bg, rgba(0, 0, 0, 0.05)) !important;
  }

  /* --- LEFT DATE LAYOUT --- */
  .date-side {
    width: 90px;
    display: flex;
    justify-content: flex-end;
    gap: 6px;
    font-size: 0.95rem;
    color: var(--text-muted-color, #757575);
    font-weight: 500;
  }

  .date-day {
    font-weight: 600;
  }

  /* --- NODE INTERSECTIONS (DOTS) --- */
  .timeline-axis {
    width: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .dot-v {
    width: 8px;
    height: 8px;
    background: var(--timeline-node-bg, #828282);
    border-radius: 50%;
    transition: all 0.2s ease;
  }

  /* --- RIGHT HYPERLINK TEXT (COMPATIBLE THEMES) --- */
  .link-txt {
    text-decoration: none !important;
    font-size: 0.95rem;
    font-weight: 500;
    flex: 1;
    padding-left: 10px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    transition: all 0.2s ease;
  }

  /* --- HARD CONTEXT SWITCHES FOR DARK VS LIGHT --- */
  
  /* Dark Mode specific colors (Terminal Cyber Pink/Red) */
  html[data-mode="dark"] .link-txt {
    color: #ff5577 !important;
  }
  html[data-mode="dark"] .archive-row-cyber:hover .link-txt {
    color: #ff2255 !important;
    text-shadow: 0 0 10px rgba(255, 34, 85, 0.4);
  }
  html[data-mode="dark"] .archive-row-cyber:hover .dot-v {
    background: #ff2255;
    box-shadow: 0 0 10px #ff2255;
  }

  /* Light Mode specific colors (Professional Deep Crimson Red) */
  html[data-mode="light"] .link-txt {
    color: #b3002d !important; /* Elegant dark red for readability on white backgrounds */
  }
  html[data-mode="light"] .archive-row-cyber:hover .link-txt {
    color: #e6003c !important;
  }
  html[data-mode="light"] .archive-row-cyber:hover .dot-v {
    background: #e6003c;
    box-shadow: 0 0 6px rgba(230, 0, 60, 0.4);
  }

  /* Universal row hover dynamics */
  .archive-row-cyber:hover .link-txt {
    padding-left: 14px; /* Sleek shift translation effect */
  }
  
  .archive-row-cyber:hover .dot-v {
    transform: scale(1.25);
  }
</style>