---
layout: page
title: projects
permalink: /projects/
description: Research and outreach projects I have participated in
nav: true
nav_order: 2
display_categories: #[funded, outreach]
horizontal: false
---

<style>
/* Desativa o masonry e usa uma grade CSS comum: cards da mesma linha têm a mesma altura */
.projects .grid {
  display: grid !important;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
  height: auto !important;
}
.projects .grid-sizer { display: none !important; }
.projects .grid-item {
  position: static !important;
  width: auto !important;
  left: auto !important;
  top: auto !important;
  transform: none !important;
  margin: 0 !important;
}
.projects .grid-item > a { display: block; height: 100%; }
.projects .card { height: 100%; }

/* Imagens todas com a mesma proporção */
.projects .card picture { display: block; }
.projects .card img {
  display: block;
  width: 100% !important;
  height: auto !important;
  aspect-ratio: 16 / 9;
  object-fit: cover;
}

/* Título menor e com a capitalização original */
.projects .card-title.text-lowercase {
  text-transform: none !important;
  font-size: 1.35rem;
}

/* Descrição limitada a 3 linhas */
.projects .card-text {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>

<!-- pages/projects.md -->
<div class="projects">
{%- if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {%- for category in page.display_categories %}
  <h2 class="category">{{ category }}</h2>
  {%- assign categorized_projects = site.projects | where: "category", category -%}
  {%- assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-1">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
  {% endfor %}

{%- else -%}
<!-- Display projects without categories -->
  {%- assign sorted_projects = site.projects | sort: "importance" -%}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
{%- endif -%}
</div>
