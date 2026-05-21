---
title: Categories
icon: fas fa-stream
order: 2
---

<div id="page-category">
  <div class="category-grid">
    {% for category in site.categories %}
      {% capture category_name %}{{ category | first }}{% endcapture %}
      {% capture posts_size %}{{ category | last | size }}{% endcapture %}
      
      <a href="{{ site.baseurl }}/categories/{{ category_name | slugify }}/" 
         class="category-card-wrapper" 
         data-cat="{{ category_name | slugify }}">
        <div class="category-card-inner">
          <div class="category-card-content">
            <h2 class="cat-name">{{ category_name }}</h2>
            <div class="cat-stats">
              <span class="num">{{ posts_size }}</span>
              <span class="label">POSTS</span>
            </div>
          </div>
        </div>
      </a>
    {% endfor %}
  </div>
</div>

<style>
/* 1. Create the Grid Layout */
.category-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    margin-top: 1rem;
}

/* 2. Remove default blue links */
.category-card-wrapper {
    text-decoration: none !important;
    display: block;
}

/* 3. Style the Card Box */
.category-card-inner {
    position: relative;
    height: 220px;
    border-radius: 8px;
    border: 2px solid #b30000;
    background-color: #1a1a1a;
    background-size: cover;
    background-position: center;
    overflow: hidden;
    transition: transform 0.3s ease, border-color 0.3s ease;
}

/* 4. Add a dark overlay */
.category-card-inner::before {
    content: "";
    position: absolute;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(0, 0, 0, 0.65);
    z-index: 1;
}

/* 5. Hover Effect */
.category-card-wrapper:hover .category-card-inner {
    transform: translateY(-5px);
    border-color: #ff3333;
    box-shadow: 0 10px 20px rgba(255, 0, 0, 0.2);
}

/* 6. Center the Text Content */
.category-card-content {
    position: relative;
    z-index: 2;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
}

/* 7. Style the Category Title */
.cat-name {
    font-size: 2rem;
    font-weight: 700;
    color: white !important;
    margin-bottom: 10px;
    text-shadow: 2px 2px 4px #000;
}

/* 8. Style the Post Count */
.cat-stats {
    font-size: 1.2rem;
    font-weight: bold;
    color: #ffcccc;
}

/* =========================================
   9. IMAGES DE FOND PAR CATÉGORIE
   ========================================= */
.category-card-wrapper[data-cat="offensive-security"] .category-card-inner {
    background-image: url('/assets/img/banners/offensive.jpg');
}
.category-card-wrapper[data-cat="defensive-security"] .category-card-inner {
    background-image: url('/assets/img/banners/defensive.jpg');
}

/* Matches any link pointing to project or Project */
.category-card-wrapper[href*='/categories/project/'] .category-card-inner,
.category-card-wrapper[href*='/categories/Project/'] .category-card-inner,
.category-card-wrapper[data-cat='project'] .category-card-inner {
  background-image: url('/assets/img/banners/project.jpg') !important;
}
</style>
