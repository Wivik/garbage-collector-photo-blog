---
{{- $imgglob := printf "*%s" (path.Join .File.Dir "**") -}}
{{- $resources := where (resources.Match $imgglob) "ResourceType" "image" }}
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
albumthumb: "{{ cond (gt (len $resources) 0) (index $resources 0) "" }}"
draft: false
## Optional additional meta info for resources list
#  alt: Image alternative and screen-reader text
#  phototitle: A title for the photo
#  description: A sub-title or description for the photo
tags:
  - Album
---

{{ range $elem_index, $elem_val := $resources -}}
{{- printf "{{" -}}< exif src="/{{ . }}" >{{- printf "}}\n\n" -}}
{{ end -}}


