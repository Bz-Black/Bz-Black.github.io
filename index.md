---
layout: home
title: Bz-Black | Algorithm Notes
---

# Bz-Black

👋 Hi，我在这里记录算法学习笔记

## 📚 最新文章
## 🧠 Algorithms
{% for post in site.categories.Algorithms %}
- [{{ post.title }}]({{ post.url }})
{% endfor %}

## 🗄️ MySQL
{% for post in site.categories.MySQL %}
- [{{ post.title }}]({{ post.url }})
{% endfor %}
