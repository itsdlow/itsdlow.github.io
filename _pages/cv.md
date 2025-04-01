---
layout: archive
title: "Resume"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
file_url: "files/DeAngelo-Wilson_Resume-25.pdf"
file_type: "application/pdf"
last_update_date: "March 2025"
---

{% include base_path %}




{% assign rel_url=page.file_url | absolute_url %}
{% include {{ page.file_include }} url=rel_url media_type=page.file_type update_date=page.last_update_date %}
