---
layout: default
title: Blog
---

# EchoHollow Labs — Blog

Welcome to the operations log and research drops.

---

<div style="display: flex; flex-wrap: wrap; gap: 20px; justify-content: center;">

{% for post in site.posts %}
  <div style="border: 1px solid #00ffcc; border-radius: 10px; padding: 20px; width: 300px; background-color: #0d0d0d;">
    <h2 style="color: #00ffcc; font-size: 1.5em;">
      <a href="{{ post.url }}" style="text-decoration: none; color: #00ffcc;">
        {{ post.title }}
      </a>
    </h2>
    <p style="font-size: 0.9em; color: #888;">Posted on {{ post.date | date: "%B %d, %Y" }}</p>
    <p style="font-size: 1em; color: #ccc;">{{ post.excerpt }}</p>
  </div>
{% endfor %}

</div>
