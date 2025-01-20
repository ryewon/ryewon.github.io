---
title: Main
nav_order: 1
permalink: /
---

# 전체 페이지
{: .fs-8 }


<nav aria-label="Main" id="site-nav" class="site-nav">
  {% assign pages_top_size = site.html_pages
        | where_exp:"item", "item.title != nil"
        | where_exp:"item", "item.parent == nil"
        | where_exp:"item", "item.nav_exclude != true"
        | size %}
  {% if pages_top_size > 0 %}
    {% include components/nav/pages.html pages=site.html_pages all=include.all %}
  {% endif %}
  {%- if site.nav_external_links -%}
    <ul class="nav-list">
      {%- for node in site.nav_external_links -%}
        <li class="nav-list-item external">
          <a href="{{ node.url | absolute_url }}" class="nav-list-link external"
            {% if node.opens_in_new_tab or node.opens_in_new_tab == nil and site.nav_external_links_new_tab %}
              target="_blank" rel="noopener noreferrer"
            {% endif %}
          >
            {{ node.title }}
            {% unless node.hide_icon %}<svg viewBox="0 0 24 24" aria-labelledby="svg-external-link-title"><use xlink:href="#svg-external-link"></use></svg>{% endunless %}
          </a>
        </li>
      {%- endfor -%}
    </ul>
  {%- endif -%}
</nav>
