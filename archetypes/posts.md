---
title: "{{ replaceRE "[-_]" " " .Name | title }}"
date: {{ .Date }}
draft: true
math: true
menu:
  sidebar:
    name: "{{ replaceRE "[-_]" " " .Name | title }}"
    identifier: "{{ .Name | lower }}"
    parent:
    weight: 10
hero: 
---