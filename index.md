---
layout: default
title: ฟอนต์เกิดใหม่บ้างในบางเวลา ...
cover:
  path: /f0nt/images/fontuni-cover.jpg
  width: 2400
  height: 1260
---

# {{ page.title }}
{: .post-title }

## รายชื่อฟอนต์
{: .hidden }

<ol class="font-list">
  {% assign fonts = site.fonts | sort: 'date') | reverse %}
  {% for font in fonts %}
    {% if font.thumbnail %}
      <li>
        <a class="{{ font.name }}" href="{{ font.url | replace:'index.html','' }}" title="{{ font.title }}">
          <img class="svg" src="{{ font.thumbnail }}" alt="{{ font.title }}"><span>{{ font.title }}</span>
        </a>
      </li>
    {% endif %}
  {% endfor %}
</ol>

