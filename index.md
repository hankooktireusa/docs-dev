---
layout: default
title: Home
permalink: /
nav: false
---

<!-- Instant redirect (works with baseurl) -->
<script>
  window.location.replace('{{ "/en/" | relative_url }}');
</script>
<meta http-equiv="refresh" content="0; url={{ "/en/" | relative_url }}">
<p>If you are not redirected, <a href="{{ "/en/" | relative_url }}">click here</a>.</p>
