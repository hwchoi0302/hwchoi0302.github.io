---
layout: page
permalink: /publications/
title: publications
description: Graduate research papers and preprints.
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

{% capture pub_output %}{% bibliography %}{% endcapture %}
{% if pub_output contains '<li' %}
  <!-- Bibsearch Feature -->
  {% include bib_search.liquid %}
  <div class="publications">
    {{ pub_output }}
  </div>
{% else %}
  <div style="text-align: center; padding: 3.5rem 1rem; color: var(--global-text-color-light);">
    <p style="font-size: 1.15rem; margin-bottom: 0.5rem;">추후 연구 논문이 추가될 예정입니다.</p>
    <p style="font-size: 0.95rem;">Publications will be updated later.</p>
  </div>
{% endif %}
