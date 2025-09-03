---
layout: page
title: LeetCode
permalink: /categories/leetcode/
---

<div class="category-page">
  <h1>LeetCode相关文章</h1>
  
  {%- assign leetcode_posts = site.posts | where_exp: "post", "post.path contains 'Leetcode'" -%}
  
  {%- if leetcode_posts.size > 0 -%}
    <ul class="post-list">
      {%- for post in leetcode_posts -%}
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
    <p>暂无LeetCode相关文章。</p>
  {%- endif -%}
</div>
