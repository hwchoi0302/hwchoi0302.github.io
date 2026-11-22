---
layout: default
permalink: /blog/
title: blog
nav: true
nav_order: 1
pagination:
  enabled: true
  collection: posts
  permalink: /page/:num/
  per_page: 6
  sort_field: date
  sort_reverse: true
  trail:
    before: 1
    after: 3
---

<div class="post">

{% assign blog_name_size = site.blog_name | size %}
{% assign blog_description_size = site.blog_description | size %}

{% if blog_name_size > 0 or blog_description_size > 0 %}
  <div class="header-bar">
    <h1>{{ site.blog_name }}</h1>
    <h2>{{ site.blog_description }}</h2>
  </div>
{% endif %}

{% if site.posts.size == 0 %}
  <div style="text-align: center; padding: 3.5rem 1rem; color: var(--global-text-color-light);">
    <p style="font-size: 1.15rem; margin-bottom: 0.5rem;">아직 작성된 글이 없습니다.</p>
    <p style="font-size: 0.95rem;">Posts will be updated soon.</p>
  </div>
{% else %}

  {% if site.display_tags and site.display_tags.size > 0 or site.display_categories and site.display_categories.size > 0 %}
    <div class="tag-category-list">
      <ul class="p-0 m-0">
        {% for tag in site.display_tags %}
          <li>
            <i class="fa-solid fa-hashtag fa-sm"></i> <a href="{{ tag | slugify | prepend: '/blog/tag/' | relative_url }}">{{ tag }}</a>
          </li>
          {% unless forloop.last %}
            <p>&bull;</p>
          {% endunless %}
        {% endfor %}
        {% if site.display_categories.size > 0 and site.display_tags.size > 0 %}
          <p>&bull;</p>
        {% endif %}
        {% for category in site.display_categories %}
          <li>
            <i class="fa-solid fa-tag fa-sm"></i> <a href="{{ category | slugify | prepend: '/blog/category/' | relative_url }}">{{ category }}</a>
          </li>
          {% unless forloop.last %}
            <p>&bull;</p>
          {% endunless %}
        {% endfor %}
      </ul>
    </div>
  {% endif %}

  <ul class="post-list">
    {% if page.pagination.enabled %}
      {% assign postlist = paginator.posts %}
    {% else %}
      {% assign postlist = site.posts %}
    {% endif %}

    {% for post in postlist %}
      {% assign read_time = post.content | strip_html | number_of_words | divided_by: 180 | plus: 1 %}
      {% assign year = post.date | date: '%Y' %}
      {% assign tags = post.tags | join: '' %}
      {% assign card_image = post.cover | default: post.thumbnail %}

      <li>
        {% if card_image %}
          <div class="row align-items-center">
            <div class="col-sm-8">
        {% endif %}
              <h3>
                <a class="post-title" href="{{ post.url | relative_url }}">{{ post.title }}</a>
              </h3>
              <p>{{ post.description }}</p>
              <p class="post-meta">
                {{ read_time }} min read &nbsp;&middot;&nbsp;
                {{ post.date | date: '%B %d, %Y' }}
              </p>
              <p class="post-tags">
                <a href="{{ year | prepend: '/blog/' | relative_url }}">
                  <i class="fa-solid fa-calendar fa-sm"></i> {{ year }}
                </a>
                {% if tags != '' %}
                  &nbsp;&middot;&nbsp;
                  {% for tag in post.tags %}
                    <a href="{{ tag | slugify | prepend: '/blog/tag/' | relative_url }}">
                      <i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}
                    </a>
                    {% unless forloop.last %}&nbsp;{% endunless %}
                  {% endfor %}
                {% endif %}
              </p>
        {% if card_image %}
            </div>
            <div class="col-sm-4">
              <a href="{{ post.url | relative_url }}">
                <img
                  class="card-img"
                  src="{{ card_image | relative_url }}"
                  style="object-fit: cover; width: 100%; height: 150px; border-radius: 8px;"
                  alt="{{ post.title | escape }}"
                >
              </a>
            </div>
          </div>
        {% endif %}
      </li>
    {% endfor %}
  </ul>

  {% if page.pagination.enabled %}
    {% include pagination.liquid %}
  {% endif %}

{% endif %}

</div>
