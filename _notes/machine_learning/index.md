---
title: Notes - Machine Learning
excerpt: Section header for all machine learning notes.
layout: single
permalink: /notes/machine_learning/index.html
---


{{ page.title }}

<div>
  {% if site.data.navigation.notes_machine_learning[0] %}
    {% for item in site.data.navigation.notes_machine_learning %}
      <h3><a href="{{ item.url }}">{{ item.title }}</a></h3>
      <p>{{ item.excerpt }}</p>
      {% endfor %}
  {% endif %}
</div>