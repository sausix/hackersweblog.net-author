---
title: Generelle Infos
date: 2020-02-15
description: Diese Seite beinhaltet ein paar Markdown-Elemente
tags: demo, markdown
sources: http://where-i-stole-my-content.com/article.html
---

# Infos zur Struktur des Projektes hackersweblog.net als Demo-Content 

## Header von Content-Dateien
* Alle Keys in Headern klein
* Jeder Key einmalig. Evtl. überschreiben spätere Keys den vorherigen.
* Ländercodes immer nach `ISO 639-1:2002` (2 Buchstaben, kleingeschrieben)

`---`  
`title: Generelle Infos` Titel möglichst knapp, evtl. Abbildung in URL (Pflichtangabe)  
`date: 2019-02-15` Hauptdatum (erstellt) (Pflichtangabe)  
`revision: 2020-01-31` Datum der letzten Überarbeitung (oder aus git repo meta)  
`publish: Hidden` Standard `Yes`. `No` ignoriert das Dokument, `Hidden` zeigt es *nirgends* an. ISO-Datum (oder mit Uhrzeit) gibt den Zeitpunkt der Publizierung an. update.py muss erneut ausgeführt werden!  
`description: Diese Seite beinhaltet ein paar Markdown-Elemente` Etwas längere Beschreibung, Einzeiler. (Pflichtangabe)  
`tags: demo, markdown` Tags, getrennt mit Komma. Namen immer klein. Leerzeichnen-Tags erlaubt(?) -> unschön.  
`sources: http://where-i-stole-my-content.com/article1.html, http://where-i-stole-my-content.com/article2.html` Liste von Quellangaben, kommagetrennt. Das Komma ist kein gültiges Zeichen in URLs.  
`linkto: some-category/other-content-pointed-to` Meta-Verlinkung auf einen Artikel  
`linkwith: some-category/other-content-linked-vice-versa` Verkettung dieses Artikels mit dem anderen  
`template: hackersweblog.net` Optional wenn bestimmtes Template gewünscht.  
`model: index.html` Optional wenn bestimmtes Modell (HTML-Datei) gewünscht. Vermeiden zwecks Kompatibilität.  
`image: post.jpg` Optionales Bild zum Artikel (für Thumbnail etc.)  
~~`url:`~~ Verboten. Wird generiert. Url zum Artikel.  
~~`author:`~~ Verboten. Wird generiert. Autor-Meta.  
~~`lang:`~~ Verboten. Wird generiert. Sprache des Artikels.  
~~`langs:`~~ Verboten. Wird generiert. Liste aller verfügbaren Sprachen des Artikels.  
~~`otherlangs:`~~ Verboten. Wird generiert. Liste aller anderen Sprachen des Artikels.  
~~`gitsource:`~~ Verboten. Wird generiert. Url zum git repo.  
~~`mdsource:`~~ Verboten. Wird generiert. Pfad zu Quelldatei (md).  
~~`id:`~~ Verboten. Wird generiert. contentid.  
~~`files:`~~ Verboten. Wird generiert. Alle gefundenen Dateien im selben Ordner ausgenommen contents und Sprachvarianten.  
`---`

## Header von author/meta.md
`---`  
´nickname: sausix´ Eindeutiger Name unter dem alle Repos als der selbe Autor gruppiert werden. (Pflichtangabe)  
fullname: Adrian Sausenthaler  
birth: 1984-03-19  
social:  
  https://github.com/sausix: github  
  https://twitter.com/sausix: twitter  
avatar: avatar.jpg  
contentgrant: `hackersweblog.net`  oder `"*"` oder eine Liste `["page1.net", "page2.net"]` (Pflichtangabe)  
~~`langs`:~~ Verboten, Wird aus gefundenem Content generiert.  
~~`contents:`~~ Verboten. Wird generiert.  
~~`gitsources:`~~ Verboten. Wird generiert. Liste von Urls zu git repos.  
`---`

## Root
Webserver Verzeichnis, ziel der Dateigenerierung: `/srv/http/hackersweblog.net/public`  

## Autoren-Repo
* `/author/meta.md` Infos zum Autor
* `/author/`**lang**`}.md` Text zum Autor in bestimmter Sprache. Idealerweise für jedes author.lang
* `/author/*` Bilder und Dateien referenziert in {lang}.md
* `/content/*/*.`**lang**`.md` Daraus wird der Content des Autors generiert. Unterordner ok. Ordnerstruktur möglichst mit Tags gleich halten, zumindest den Hauptordner -> content/linux/terminal/tricks.de.md. Sprachcode ist Pflicht!

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
* `http://hackersweblog.net/demo/demofile/de`  -> `repo://content/demo/demofile.de.md`
* `http://hackersweblog.net/demo/demofile/en` -> `repo://content/demo/demofile.en.md`
* `http://hackersweblog.net/demo/demofile` -> `repo://content/demo/demofile.`**pagedefault**`.md` oder:
* `http://hackersweblog.net/demo/demofile` -> `repo://content/demo/demofile.`**first**`.md` oder:
* `http://hackersweblog.net/deatplayer/de` -> `repo://author/de.md`
* `http://hackersweblog.net/linux` -> (taglist, generiert)
* `http://hackersweblog.net/bla.css` -> `templaterepo://bla.css`

## Generelle Stichpunkte
* Ein TEMPLATE ist ein globaler "Style". Nur einmal pro Repo, direkt im root. Unterordner für CSS, Bilder optional.
* Ein MODEL ist eine von mehreren HTML-Dateien (index.html, tag.html, author.html) eines Templates.
* Ein CONTENT sind die Artikel bzw. eigentlichen Inhalte.
* Eine CONTENTID ist der minimale relative Pfad unterhalb von repo://content/ ohne lang und ohne md.

## Datentypen und Strukturen
Datentypen sind per Jinja in bestimmten Template-Models verfügbar.

### Datentyp "generationtime"
Beinhaltet die Datums und Zeitinformationen, wann die Contents generiert wurden.

Vorhanden in:
* generationtime (Global)

Properties:
* day (01..31)
* month (01..12)
* year (2020)
* hour (14)
* minute (59)
* second (59)

Predefined by formats in Config.DATETIME_FORMATS or PageConfig.DATETIME_FORMATS:
* date
* time
* datetime

### Datentyp "tag"
Vorhanden in:
* content.tags (Liste aller Tags des Contents)
* tags (alle Tags, sortiert nach häufigkeit)
* content.author.tags (alle Tags des authors, sortiert nach häufigkeit)
* tag (gültig nur auf der Index-Seite eines Tags)

"tag" hat properties:
* tag.name
* tag.url (url zu tag-index)
* tag.count (wieviele Contents haben den)
* tag.contents (liste aller contents mit diesem tag)


### Datentyp "content"
Vorhanden in:
* content (Aktueller Content)
* contents (Liste aller Contents, zeitlich sortiert)
* author.contents (Liste aller Contents eines Autors, zeitlich sortiert)

Properties:
* content."metakey" (Tags aus YAML-Header)
* content.url (Link auf den Content)
* content.author (Autor-Meta)
* lang (contentlang-Struktur)
* langs (Liste aller Sprachversionen des Contents)

### Datentyp "author"
Vorhanden in:
* authors (Liste aller Autoren)
* content.author (Autot-Meta zum Content)

Properties:
* author."metakey"
* author.contents (Liste von Contents des Autors)

### Datentyp "contentlang"
Vorhanden in:
* content.langs (Liste aller Sprachen zum Content)
* content.lang (Sprache zum Content)

Properties:
* contentlang.langcode (Sprachcode, 2 Buchstaben)
* contentlang.url (Url zum Content in dieser Sprache)

### Datentyp "authorlang"
Vorhanden in:
* author.langs (Liste aller Sprachen der verfassten Contents des Autors)

Properties:
* authorlang.langcode (Sprachcode, 2 Buchstaben)
* authorlang.contents (Liste aller Contents des Autors einer bestimmten Sprache)
