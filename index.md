---
layout: default
---

<div class="hero">
  <div class="tagline boontook-mon">{{ site.tagline }}</div>
  <!--<p style="font-size:1.5em;">อยากให้เรามีเวลาทำฟอนต์ฟรีมากขึ้น?<br> <a href="http://fontuni.bigcartel.com/">อุดหนุนของชำร่วยที่นี่เลยครับ!</a></p>-->
</div>


<div class="grid font-icon clearfix">
  {% assign fonts = site.fonts | sort: 'date') | reverse %}
  {% for font in fonts %}
    {% if font.thumbnail %}
      <div class="grid-item">
        <a href="{{ font.url }}" title="{{ font.title }}"><img src="{{ font.thumbnail }}" alt="{{ font.title }}"></a>
      </div>
    {% endif %}
  {% endfor %}
</div>

