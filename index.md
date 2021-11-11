---
layout: home
author_profile: true
---

<h3 class="archive__subtitle">Recent Projects</h3>

{%- assign projects = site.portfolio | where_exp:"item", "item.tags contains 'featured'" | sort: 'date' | reverse -%}
{%- assign entries_layout = 'grid' -%}
<div class="entries-{{ entries_layout }}">
  {%- for post in projects | limit: 4 -%}
    {%- include archive-single.html type=entries_layout -%}
  {%- endfor -%}
</div>

[View full Portfolio](/portfolio/){: .btn .btn--info}

<br/>
