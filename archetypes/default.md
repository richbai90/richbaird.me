---
title: "{{ replaceRE "[-_]" " " .Name | title }}"
date: {{ .Date }}
draft: true
math: true
menu:
  sidebar:
    name: "{{ replaceRE "[-_]" " " .Name | title }}"
    identifier: "{{ .Name | lower }}"
    parent: {{ strings.TrimSuffix "/" (path.Split .File.Dir).Dir | path.Dir | path.Base }}
    weight: 10
hero: 
---