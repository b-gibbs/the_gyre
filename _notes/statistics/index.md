---
title: Notes - Statistics
excerpt: Section header for all statistics notes.
layout: default
permalink: /notes/statistics/index.html
---

Statistics notes.

<div>
{% if site.data.navigation.notes_statistics[0] %}
  {% for item in site.data.navigation.notes_statistics %}
    <h3><a href="{{ item.url }}">{{ item.title }}</a></h3>
    <p>{{ item.excerpt }}</p>
    {% endfor %}
{% endif %}
</div>