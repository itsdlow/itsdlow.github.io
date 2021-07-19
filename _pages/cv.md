---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
file_url: "files/2021_Resume_DeAngelo.pdf"
file_type: "application/pdf"
last_update_date: "July 2021"
---

{% include base_path %}




{% assign rel_url=page.file_url | absolute_url %}
{% include {{ page.file_include }} url=rel_url media_type=page.file_type update_date=page.last_update_date %}
