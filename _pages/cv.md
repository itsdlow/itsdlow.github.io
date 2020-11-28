---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
file_url: "files/2020-07-08-resume.pdf"
file_title: "Resume"
file_type: "application/pdf"
---

{% include base_path %}




{% assign rel_url=page.file_url | absolute_url %}
{% include {{ page.file_include }} title=page.file_title url=rel_url media_type=page.file_type %}
