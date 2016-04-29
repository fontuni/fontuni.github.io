---
layout: default
title: ฟอนต์เกิดใหม่บ้างในบางเวลา ...
excerpt: "สำนักอักขระฟอนต์อยู่นี่  มุ่งผลิตฟอนต์เสรีให้แสดงผลได้ถูกต้องและดีพอ เน้นมาตรฐานยูนิโค้ดและโอเพ่นไทป์ เพื่อให้ทุกคนมีอิสระในการใช้งาน แจกจ่าย หรือดัดแปลงได้อย่างสบายใจ"
---

# {{ page.title }}
{: .post-title }

## รายชื่อฟอนต์
{: .hidden }

<ol class="font-list">
  {% assign fonts = site.fonts | sort: 'date' | reverse %}
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

