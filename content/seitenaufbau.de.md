---
title: Generelle Infos
date: 2020-02-15
description: Diese Seite beinhaltet ein paar Markdown-Elemente
tags: demo, markdown
source: http://where-i-stole-my-content.com/article.html
---

# Infos zur Struktur des Projektes hackersweblog.net als Demo-Content 

## Header von Content-Dateien
* Alle Keys in Headern klein
* Jeder Key einmalig. Evtl. überschreiben spätere Keys den vorherigen.

`---`  
`title: Generelle Infos` Titel möglichst knapp, evtl. Abbildung in URL  
`date: 2019-02-15` Hauptdatum (erstellt)  
`revision: 2020-01-31` Datum der letzten Überarbeitung (oder aus git repo meta)  
`publish: Hidden` Standard `Yes`. `No` ignoriert das Dokument, `Hidden` zeigt es *nirgends* an  
`publish-after: 2020-02-15 12:00` Optional, wenn Publish nicht `No`, überschreibst mit `Publish: Hidden` bzw. `Publish: Yes` je nach Datum. cron-python-html/update.py muss erneut ausgeführt werden!  
`description: Diese Seite beinhaltet ein paar Markdown-Elemente` Etwas längere Beschreibung, Einzeiler.  
`tags: demo, markdown` Tags, getrennt mit Komma. Namen immer klein. Leerzeichnen-Tags erlaubt(?) -> unschön.  
`source: http://where-i-stole-my-content.com/article1.html, http://where-i-stole-my-content.com/article2.html` Liste von Quellangaben, kommagetrennt. Das Komma ist kein gültiges Zeichen in URLs.  
`linkto: some-category/other-content-pointed-to` Meta-Verlinkung auf einen Artikel  
`linkwith: some-category/other-content-linked-vice-versa` Verkettung dieses Artikels mit dem anderen  
`template: hackersweblog.net` Optional wenn bestimmtes Template gewünscht.  
`model: index.html` Optional wenn bestimmtes Modell (HTML-Datei) gewünscht. Vermeiden zwecks Kompatibilität.  
`image: post.jpg` Optionales Bild zum Artikel (für Thumbnail etc.)  
~~`url:`~~ Verboten. Wird generiert.  
~~`author:`~~ Verboten. Wird generiert.  
`---`

## Header von author/meta.md
`---`  
Nickname: sausix  
Fullname: Adrian Sausenthaler  
Birth: 1984-03-19  
Social:  
  https://github.com/sausix: github  
  https://twitter.com/sausix: twitter  
Avatar: avatar.jpg  
Lang: de, en  
ContentGrant: hackersweblog.net  
~~`contents:`~~ Verboten. Wird generiert.  
`---`

## Root
Webserver Verzeichnis, ziel der Dateigenerierung: `/srv/http/hackersweblog.net/public`  

## Autoren-Repo
* `/author/meta.md` Infos zum Autor
* `/author/{lang}.md` Text zum Autor in bestimmter Sprache. Idealerweise für jedes author.lang
* `/author/*` Bilder und Dateien referenziert in {lang}.md
* `/content/*` Daraus wird der Content des Autors generiert. Unterordner ok. Ordnerstruktur möglichst mit Tags gleich halten, zumindest den Hauptordner -> content/linux/terminal/tricks.de.md

## Template-Repo
Lauffähige Html-Seiten als "MODEL" mit Jinja-Tags: https://palletsprojects.com/p/jinja/  
Möglichst allgemein und logisch halten, damit templates und content keine harten abhängikeiten haben.  
Zugehörige Scripte, Bilder, CSS direkt im root. Ist besser, da es weniger Konflikte gäbe: Ordner "css" vs. tag css.

* `/content.html` "default" für content.
* `/tag.html` Spezialseite zu einem bestimmten tag. Spezielle Variablen vorhanden.
* `/author.html` Spezialseite zu einem bestimmten author. Spezielle Variablen vorhanden.
* weitere Modelle wären stark abhängig vom Template. Vielleicht doch den "content.model"-Tag verbieten?

## Pfade und Links in Templates und Content
Immer relativ zum Repo-Root halten. Externe Fonts etc. natürlich absolut.

## URL-Mappings SEO:
`"ISOLATED": False` (default und am nicesten):
* `http://hackersweblog.net/demo/demofile/de`  -> `repo://content/demo/demofile.de.md`
* `http://hackersweblog.net/demo/demofile/en` -> `repo://content/demo/demofile.en.md`
* `http://hackersweblog.net/demo/demofile` -> `repo://content/demo/demofile.`default oder first`.md`
* `http://hackersweblog.net/deatplayer/de` -> `repo://author/de.md`
* `http://hackersweblog.net/linux`  -> (generiert)
* `http://hackersweblog.net/bla.css`  -> `repo://bla.css`

`"ISOLATED": True` (Konflikte unwahrscheinlicher):
* `http://hackersweblog.net/author/sausix/en` -> `repo://author/en.md`
* `http://hackersweblog.net/author/deatplayer/de` -> `repo://author/de.md`
* `http://hackersweblog.net/content/demo/demofile/de` -> `repo://content/demo/demofile.de.md`
* `http://hackersweblog.net/tag/linux` -> (generiert)
* `http://hackersweblog.net/bla.css` -> `repo://bla.css` Ausnahmsweise immer relativ zu root weil sonst Templates nicht mehr eigenständig laufen wenn zugehörige Dateien je nach "ISOLATED" an verschiedenen Orten zu finden wären.


## Generelle Stichpunkte
* Ein TEMPLATE ist ein globaler "Style". Nur einmal pro Repo, direkt im root. Unterordner für CSS, Bilder optional.
* Ein MODEL ist eine von mehreren HTML-Dateien (index.html, tag.html, author.html) eines Templates.
* Ein CONTENT sind die Artikel bzw. eigentlichen Inhalte.

## Tags für Templates
* now.year _usw._
* author."metakey"
* author (Eigenbeschreibung)
* content."metakey"
* content (Der Content selber)

## Listen
Listen direkt angesprochen geben die Anzahl dahinter zurück.

### Listen mit inhalt "tag"
* content.tags
* tags (alle Tags, sortiert nach häufigkeit)
* content.author.tags (alle Tags des authors, sortiert nach häufigkeit)
* tag (gültig nur auf der Index-Seite eines Tags)

"tag" hat properties:
* tag.name
* tag.url (url zu tag-index)
* tag.count (wieviele Contents haben den)
* tag.contents (liste aller contents mit diesem tag)


### Listen mit inhalt "content"
* contents (alle contents, zeitlich sortiert)
* author.contents (contents eines autors, zeitlich sortiert)

"content" hat properties:
* content."metakey"


### Listen mit inhalt "author"
* authors (alle Autoren)

jeweils:
* author."metakey"
* author.contents
