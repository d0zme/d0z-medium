---
title: Der einfachste Weg, PDAnet mit Linux oder BSD für unbegrenztes Tethering zu nutzen
layout: post
image: https://i.imgur.com/wLMcNre.jpg
permalink: /de/pdanet-linux-freebsd-unix
---

Mobile Daten werden immer billiger & schneller, und Sie haben wahrscheinlich ein Angebot für unbegrenztes 4G/5G in Ihrer lokalen Umgebung. Der Haken an der Sache ist, dass die Datenmenge für Tethering stark begrenzt ist, und manchmal ist es überhaupt nicht erlaubt.

[PDAnet] (https://pdanet.co) ist die einfachste und wahrscheinlich beliebteste Möglichkeit, Tethering-Datenbeschränkungen zu umgehen. Es gibt eine schicke Anwendung für Windows und Mac OSX, mit der Sie Tethering mit nur wenigen Klicks einrichten können. Für Linux-, FreeBSD- oder Chrome OS-Benutzer müssen wir es selbst herausfinden.

Wenn Ihr *nix-Computer einen funktionierenden Wifi-Adapter hat, ist die Einrichtung glücklicherweise nicht so schwierig.

## Einrichten von PDAnet auf Ihrem Telefon

PDAnet ist im Play Store und im App Store erhältlich, so dass Sie es ziemlich einfach installieren können. Die [APK-Binärdateien] (http://pdanet.co/install/) sind auch auf der offiziellen Website verfügbar, falls Sie keine andere Möglichkeit haben, die App zu installieren.

Öffnen Sie die App, und klicken Sie auf das Kontrollkästchen für **"WiFi Direct Hotspot (neu!) "**, um einen Zugangspunkt zu erstellen.

Sie sollten dann oben blau hervorgehobenen Text sehen. Achten Sie auf die Felder **Name** und **Passwort**, da diese immer zufällig generiert werden, sodass Sie sie jedes Mal manuell eingeben müssen.

**Ich habe dies nur mit Android getestet, aber es ist möglicherweise das Gleiche mit den iOS-, Windows Phone- oder Blackberry-Versionen der App.

## Einrichten von WiFi auf Ihrer Linux/BSD-Box

Suchen Sie mit Ihrem WiFi-Netzwerk-Manager nach Ihrem zufällig generierten Zugangspunkt und verbinden Sie sich mit dem in der App generierten Passwort.

Sie sind dann wie gewohnt verbunden, können aber noch nicht wie beim normalen WiFi-Tethering im Internet surfen. Ein HTTP-Proxy wird auf **http://192.168.49.1:8000** gehostet und Sie haben nur über diesen Zugang zum Internet.

## Browsen im Web

Wenn Sie nur Ihren Webbrowser verwenden möchten, setzen Sie einfach Ihre Proxy-Einstellungen auf **192.168.49.1:8000**.

**In Firefox** gehen Sie zu **Einstellungen -> Netzwerk-Proxy -> Einstellungen**, und füllen Sie Ihre **Manuellen Proxy**-Einstellungen zu:

<pre>
  HTTP-Proxy: 192.168.49.1 

  Port: 8000
</pre>

**Für Chromium oder Chrome** setzen Sie den Proxy über die Kommandozeile:

<pre>
chromium-browser --proxy-server="192.168.49.1:8000"
</pre>

Und setzen Sie unbedingt den Haken bei **Diesen Proxyserver für alle Protokolle verwenden**.

## Verwendung von Apt-get (Apt) mit PDAnet

Auf einer Debian-basierten Distro können Sie Aktualisierungen mit APT installieren, indem Sie Ihre Proxy-Einstellungen vornehmen.

<pre>
  sudo nano /etc/apt/apt.conf.d/proxy.conf
</pre>

Fügen Sie diese Zeile zu Ihrer **/etc/apt/apt.conf.d/proxy.conf** Datei hinzu:

<pre>
  Acquire::http::Proxy "192.168.49.1:8000";
</pre>

Speichern Sie die Datei **proxy.conf**. 

## Proxy-Ketten mit PDAnet

Mit proxychains können Sie ein Programm dazu zwingen, Ihren PDA-Proxy zu verwenden.

Fügen Sie Ihre Server an das Ende der Datei **proxychains.conf** an und entfernen Sie alle anderen Server, die sich in der Datei befinden:

<pre>
  [ProxyList]
  https 192.168.49.1 8000
</pre>

## Zusammenfassung

**PDAnet** ist ein schickes Tool für Reisende wie mich, aber die Testversion hat den lästigen Teil, dass die Verbindung alle 15 Minuten unterbrochen wird. Wenn Sie nicht nur kurze, sporadische Tethering-Sitzungen brauchen, ist es die $15-Lizenz durchaus wert.

Auch **bitte missbrauchen Sie Ihre Verbindung** nicht mit Torrents, da Sie nie wissen, welche anderen Traffic-Shaping-Methoden Ihr Anbieter auf Sie niederhageln wird.
