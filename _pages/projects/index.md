---
layout: default
title: "Projects — Unlearnable Data Series"
permalink: /projects/
author_profile: false
---

# Projects — Unlearnable Data Series

Overview of research projects and paper pages.

<div class="projects-grid">
{% for p in site.data.projects %}
  <article class="project-card">
    <div class="project-card__image">
      <a href="{{ p.page }}">
        <img src="{{ p.thumb }}" alt="{{ p.title }}">
      </a>
    </div>
    <div class="project-card__content">
      <h2 class="project-card__title">
        <a href="{{ p.page }}">{{ p.title }}</a>
      </h2>
      <p class="project-card__description">{{ p.short }}</p>
      <div class="project-card__links">
        <a href="{{ p.paper }}" class="btn btn--small">Paper</a>
        {% if p.code %}<a href="{{ p.code }}" class="btn btn--small">Code</a>{% endif %}
        <a href="{{ p.page }}" class="btn btn--small">Project</a>
      </div>
    </div>
  </article>
{% endfor %}
</div>
