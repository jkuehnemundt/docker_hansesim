# Docker Container für Hansesim

# Voraussetzung
- Docker
- Kitematic
- Git

# Installation

Docker und Kitematic installieren.
Repository in einen beliebigen Ordner klonen.

```sh
$ git clone https://github.com/jkuehnemundt/docker_hansesim.git
$ cd docker_hansesim
```
Das Hansesim-Projekt in den "hansesim" Ordner klonen und in diesen den Inhalt des Ordners "move_to_hansesim" verschieben. Danach Kitematic starten, auf der linken Seite "dockerhansesim_php7_1 anklicken und das Terminal (Exec) öffnen. Folgende Befehle nacheinander eingeben.

Aufgrund der fehlenden Datenbankstruktur wird der erste Befehl nicht vollständig ausgeführt.
```sh
$ php composer.phar update
$ php app/console doctrine:schema:update --force
$ php app/console doctrine:fixtures:load
$ php composer.phar update
```

