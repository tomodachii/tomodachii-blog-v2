---
tags: [{% for t in tags %}{{t.tag}}{% if not loop.last %}, {% endif %}{% endfor %}]
date_created: {{dateAdded | format("YYYY-MM-DD HH:mm")}}
status: reference
MOC: []
source_type: {{itemType}}
citekey: {{citationKey}}
title: "{{title}}"
edition: {{edition}}
authors: [{{authors}}]
year: {{date | format("YYYY")}} 
ISBN: {{ISBN}}
source:
URL: {{url}}
summary:
---
# Abstract / Intro
{{abstractNote}}
# Problem Formulation

# Objectives / Purpose 

# Methods 

# Results 

# Discussion / Conclusion 

# Reference
