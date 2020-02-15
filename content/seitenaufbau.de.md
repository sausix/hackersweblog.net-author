---
Title: Generelle Infos
Date: 2020-02-15
Publish: Hidden
Publish-after: 2020-02-15 12:00
Description: Diese Seite beinhaltet ein paar Markdown-Elemente
Tags: demo, markdown
Source: http://where-i-stole-my-content.com/article.html
Linkto: some-category/other-content-pointed-to
Linkwith: some-category/other-content-linked-vice-versa
---

# Infos zur Struktur des Projektes hackersweblog.net


## Header von Content-Dateien

`---`  
`Title: Generelle Infos` Titel möglichst knapp  
`Date: 2019-02-15` Hauptdatum (erstellt)  
`Revision: 2020-01-31` Datum einer überarbeitung (oder aus git repo meta) 
`Publish: Hidden` Standard `Yes`. `No` ignoriert das Dokument, `Hidden` zeigt es *nirgends* an  
`Publish-after: 2020-02-15 12:00` Optional, wenn Publish nicht `No`, überschreibst mit `Publish: Hidden` bzw. `Publish: Yes` je nach Datum.  
`Description: Diese Seite beinhaltet ein paar Markdown-Elemente` Etwas längere Beschreibung, Einzeiler?  
`Tags: demo, markdown` Tags, getrennt mit Komma. Leerzeichnen-Tags erlaubt?  
`Source: http://where-i-stole-my-content.com/article1.html` Liste von Quellangaben  
`Source: http://where-i-stole-my-content.com/article2.html`  
`Linkto: some-category/other-content-pointed-to` Meta-Verlinkung auf einen Artikel  
`Linkwith: some-category/other-content-linked-vice-versa` Verkettung dieses Artikels mit dem anderen  
`---`


## URLs
Webserver Verzeichnis: `/srv/http/hackersweblog.net/public`  

public/  
* `static/` wirklich static, Templates usw.  
* `content/` dynamisch generiert durch backend  

Links SEO:
* `http://hackersweblog.net/content/demo/demofile/de`  -> `repo://content/demo/demofile.de.md`  
* `http://hackersweblog.net/content/demo/demofile/en` -> `repo://content/demo/demofile.en.md`  
* `http://hackersweblog.net/content/demo/demofile` -> `repo://content/demo/demofile.`default oder first`.md`  


## Generelle Stichpunkte
* Feste Liste von Git-Adressen, die auf Repos mit zwei Unterordnern zeigen. Siehe diese Repo.
* Regelmäßig git clone (ist das ok so? Wenig traffic wenn keine Changes? Gibt es bessere git-Options? Kein Blocking auf github oder so?
