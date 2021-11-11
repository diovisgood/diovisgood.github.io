---
layout: home
author_profile: true
---

<h3 class="archive__subtitle">Recent Projects</h3>

{% assign posts = site.portfolio | sort: 'date' | reverse %}

{% assign entries_layout = 'grid' %}
<div class="entries-{{ entries_layout }}">
  {% for post in posts | limit: 4 %}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>

<br/>

[View full Portfolio](/portfolio/){: .btn .btn--info}
