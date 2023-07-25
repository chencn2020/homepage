---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---


You can also find my full paper list on <u><a href="https://scholar.google.com/citations?user=ozllxV4AAAAJ">my Google Scholar profile</a>.</u>

{% include base_path %}

<table style="border-collapse: separate; border: none;">
<tbody>

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
</tbody>
</table>