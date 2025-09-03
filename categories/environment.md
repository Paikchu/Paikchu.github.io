---
layout: page
title: 环境配置
permalink: /categories/environment/
---

<div class="category-page">
  <h1>环境配置相关文章</h1>
  
  {%- assign environment_posts = site.posts | where_exp: "post", "post.path contains '环境配置'" -%}
  
  {%- if environment_posts.size > 0 -%}
    <ul class="post-list">
      {%- for post in environment_posts -%}
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
    <p>暂无环境配置相关文章。</p>
  {%- endif -%}
</div>
