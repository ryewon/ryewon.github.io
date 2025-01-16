---
title: Main
layout: home
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
permalink: /
---

# 전체 페이지
{: .fs-9 }

{%- comment -%}
  Include as: {%- include_cached components/site_nav.html all=bool -%}
  Depends on: site.
  Results in: cached HTML for the main navigation when `all` is nil or false;
    includes links to pages excluded from the main navigation when `all` is true.
  Includes:
    components/nav/pages.html
  Overwrites:
    pages_top_size, collections_size, collection_entry,
    collection_key, collection_value, collection.
{%- endcomment -%}

{% if site.just_the_docs.collections %}
  {% assign collections_size = site.just_the_docs.collections | size %}
  {% for collection_entry in site.just_the_docs.collections %}
    {% assign collection_key = collection_entry[0] %}
    {% assign collection_value = collection_entry[1] %}
    {% assign collection = site[collection_key] %}
    {% if collection_value.nav_exclude != true %}
      {% if collections_size > 1 or pages_top_size > 0 %}
        {% if collection_value.nav_fold == true %}
          <ul class="nav-list nav-category-list">
            <li class="nav-list-item">
              {%- if collection.size > 0 -%}
              <button class="nav-list-expander btn-reset" aria-label="Toggle collection {{ collection_value.name }}" aria-pressed="false">
                <svg viewBox="0 0 24 24" aria-hidden="true"><use xlink:href="#svg-arrow-right"></use></svg>
              </button>
              {%- endif -%}
              <div class="nav-category">{{ collection_value.name }}</div>
              {% include components/nav/pages.html pages=collection all=include.all %}
            </li>
          </ul>
        {% else %}
          <div class="nav-category">{{ collection_value.name }}</div>
          {% include components/nav/pages.html pages=collection all=include.all %}
        {% endif %}
      {% else %}
        {% include components/nav/pages.html pages=collection all=include.all %}
      {% endif %}
    {% endif %}
  {% endfor %}
{% endif %}