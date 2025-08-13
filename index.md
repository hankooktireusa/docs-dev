---
layout: default
title: Home
permalink: /
---

{% include lang-toggle.html %}

<!-- JS redirect (respects baseurl) -->
<script>window.location.replace('{{ "/en/" | relative_url }}');</script>

<!-- Meta refresh fallback -->
<meta http-equiv="refresh" content="0; url={{ "/en/" | relative_url }}">

# IT Docs

If you aren’t redirected automatically:
- Go to **English** → [{{ "/en/" | relative_url }}]({{ "/en/" | relative_url }})
- Go to **한국어** → [{{ "/ko/" | relative_url }}]({{ "/ko/" | relative_url }})

> Tip: once everything’s stable, you can remove this content block entirely and keep only the redirects.
