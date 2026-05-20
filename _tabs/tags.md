---
layout: page
title: Tags
icon: fas fa-tags
order: 3
---

<div id="tags-page">
  <div class="tag-cloud">
    {% assign tags = site.tags | sort %}
    {% for tag in tags %}
      {% assign tag_name = tag | first %}
      {% assign posts_size = tag | last | size %}
      
      <a href="{{ site.baseurl }}/tags/{{ tag_name | slugify }}/" class="tag-card">
        <span class="tag-icon"><i class="fas fa-terminal"></i></span>
        <span class="tag-name">{{ tag_name }}</span>
        <span class="tag-count">{{ posts_size }}</span>
      </a>
    {% endfor %}
  </div>
</div>


<style>
/* --- MISE EN PAGE GLOBALE --- */
.tag-cloud {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
    padding: 20px 0;
}

.tag-card {
    display: flex;
    align-items: center;
    padding: 10px 15px;
    border-radius: 8px;
    text-decoration: none !important;
    transition: all 0.3s ease;
    border: 1px solid transparent;
}

.tag-icon {
    margin-right: 10px;
    color: #ff3333;
    font-size: 0.9rem;
}

.tag-name {
    font-weight: 600;
    font-family: monospace;
    margin-right: 10px;
}

.tag-count {
    font-size: 0.75rem;
    padding: 2px 8px;
    border-radius: 10px;
    transition: all 0.3s ease;
}

/* --- MODE SOMBRE (DARK MODE) --- */
html[data-mode="dark"] .tag-card {
    background: #1e1e1e; /* Fond gris très sombre */
    border-color: #333;
    color: #f1f1f1 !important;
}

html[data-mode="dark"] .tag-count {
    background: #333;
    color: #aaa;
}

html[data-mode="dark"] .tag-card:hover {
    border-color: #ff3333;
    background: #252525;
    box-shadow: 0 5px 15px rgba(255, 51, 51, 0.3);
    color: #ffffff !important;
}

/* --- MODE CLAIR (LIGHT MODE) --- */
html[data-mode="light"] .tag-card {
    background: #ffffff;
    border-color: #eee;
    color: #333 !important;
    box-shadow: 0 2px 5px rgba(0,0,0,0.05);
}

html[data-mode="light"] .tag-count {
    background: #f0f0f0;
    color: #666;
}

html[data-mode="light"] .tag-card:hover {
    border-color: #ff3333;
    background: #fffafa;
    box-shadow: 0 5px 15px rgba(255, 51, 51, 0.1);
    color: #ff3333 !important;
}

/* --- HOVER COMMUN --- */
.tag-card:hover .tag-count {
    background: #ff3333;
    color: white;
}

.tag-card:hover {
    transform: translateY(-3px);
}
/* Style des Tags "Trending" à droite */
.post-tag {
    display: inline-block;
    background: transparent !important;
    border: 1.5px solid #ff3333 !important; /* Bordure rouge fine */
    color: #ff3333 !important;
    border-radius: 20px !important; /* Très arrondi */
    padding: 2px 12px !important;
    margin: 4px 2px !important;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem !important;
    transition: all 0.2s ease;
}

.post-tag:hover {
    background: #ff3333 !important;
    color: #000 !important; /* Texte noir sur fond rouge au survol */
    box-shadow: 0 0 10px rgba(255, 51, 51, 0.4);
}
</style>