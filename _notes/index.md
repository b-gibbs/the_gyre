---
title: Notes
excerpt: Section header for all notes.
layout: archive
permalink: /notes/index.html
---
Each notes page should have two menus:
- a menu that accesses all other notes in the section
- a table of contents menu

On screens wider than iPad vertical, both menus should be always visible and fixed to the side of the Jupyter notebook.  They should probably scroll independently, too.

On iPad Pro 12.9" vertical and narrower, these menus should be available via popover, whose button is fixed in a right thumb-friendly location.

<div>
{% if site.data.navigation.notes[0] %}
  {% for item in site.data.navigation.notes %}
    <h3><a href="{{ item.url }}">{{ item.title }}</a></h3>
    <p>{{ item.excerpt }}</p>
    {% endfor %}
{% endif %}
</div>