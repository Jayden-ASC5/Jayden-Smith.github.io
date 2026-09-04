---
layout: homepage
title: Portfolio | Jayden Smith
---

# Portfolio

A collection of research, internship, club, and personal projects, grouped by category. Use the filters below to jump to a specific group, or click any title to read the full write-up.

<div class="category-filters">
<a href="#" class="filter-btn active" data-filter="all">All</a>
{% for category in site.project_categories %}
{% assign items = site.projects | where: "category", category %}
{% if items.size > 0 %}<a href="#{{ category | slugify }}" class="filter-btn" data-filter="{{ category | slugify }}">{{ category }}</a>{% endif %}
{% endfor %}
</div>

{% for category in site.project_categories %}
{% assign items = site.projects | where: "category", category | sort: "order" %}
{% if items.size > 0 %}

<section class="portfolio-group" id="{{ category | slugify }}" data-category="{{ category | slugify }}" markdown="1">

## {{ category }}

{% for project in items %}
### [{{ project.title }}]({{ project.url | relative_url }})

*{{ project.period }}*

{% if project.image %}![{{ project.title }}]({{ project.image | relative_url }}){% endif %}

{{ project.summary }}

{% if project.topics %}**Topics:** {{ project.topics | join: " · " }}{% endif %}

[Read more →]({{ project.url | relative_url }})

---
{% endfor %}

</section>
{% endif %}
{% endfor %}

*Last updated {{ site.time | date: "%B %Y" }}*

<script>
(function () {
  var buttons = document.querySelectorAll('.category-filters .filter-btn');
  var groups = document.querySelectorAll('.portfolio-group');
  if (!buttons.length || !groups.length) return;

  function applyFilter(filter) {
    groups.forEach(function (g) {
      g.style.display = (filter === 'all' || g.getAttribute('data-category') === filter) ? '' : 'none';
    });
    buttons.forEach(function (b) {
      b.classList.toggle('active', b.getAttribute('data-filter') === filter);
    });
  }

  buttons.forEach(function (btn) {
    btn.addEventListener('click', function (e) {
      var filter = btn.getAttribute('data-filter');
      if (filter === 'all') e.preventDefault();
      applyFilter(filter);
    });
  });
})();
</script>
