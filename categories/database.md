---
layout: page
title: 数据库
permalink: /categories/database/
---

<div class="category-page">
  <h1>数据库相关文章</h1>
  
  {%- assign database_posts = site.posts | where_exp: "post", "post.path contains 'Database'" -%}
  
  {%- if database_posts.size > 0 -%}
    <ul class="post-list">
      {%- for post in database_posts -%}
      <li>
        {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
        <span class="post-meta">{{ post.date | date: date_format }}</span>
        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>
        {%- if site.show_excerpts -%}
          {{ post.excerpt }}
        {%- endif -%}
      </li>
      {%- endfor -%}
    </ul>
  {%- else -%}
    <p>暂无数据库相关文章。</p>
  {%- endif -%}
</div>
