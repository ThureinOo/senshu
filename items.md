---
layout: page
title: Items
---

## What You Have — Item Descriptions

| Item | Description |
|------|-------------|
{% for i in site.data.items %}| **{{ i.label }}** | {{ i.description }} |
{% endfor %}

### Target OS

| OS | Description |
|----|-------------|
{% for o in site.data.target_os %}| **{{ o.label }}** | {{ o.description }} |
{% endfor %}
