---
title: Le moyen le plus simple d'utiliser PDAnet avec Linux ou BSD pour une connexion illimitée
layout: post
image: https://i.imgur.com/wLMcNre.jpg
permalink: /fr/pdanet-linux-freebsd-unix
---

Les données mobiles deviennent moins chères et plus rapides, et vous avez probablement une offre pour la 4G/5G illimitée dans votre zone locale. Cette offre s'accompagne généralement d'une série d'allocations de données très limitées pour la connexion, et parfois elle n'est pas du tout autorisée.

[PDAnet] (https://pdanet.co) est le moyen le plus simple, et probablement le plus populaire, d'éviter le plafonnement des données. Ils disposent d'une application astucieuse pour Windows et Mac OSX qui vous permet de vous connecter en quelques clics seulement. Pour les utilisateurs de Linux, FreeBSD ou Chrome OS, nous devons nous débrouiller seuls.

Heureusement, si votre ordinateur *nix dispose d'un adaptateur Wifi fonctionnel, ce n'est pas si difficile à configurer.

## Configuration de PDAnet pour votre téléphone

PDAnet est disponible sur le Play Store, l'App Store, donc il est assez simple à installer. [APK binaires](http://pdanet.co/install/) sont également disponibles sur leur site officiel au cas où vous n'auriez pas d'autre moyen de l'installer.

Ouvrez l'application, et cliquez sur la case à cocher **"WiFi Direct Hotspot (new !) "** pour créer un point d'accès.

Vous devriez alors voir un texte surligné en bleu en haut de l'écran. Prenez note des champs **Nom** et **Mot de passe** car ils sont toujours générés de manière aléatoire et vous devrez donc les saisir manuellement à chaque fois.

**Je n'ai testé cela qu'avec Android, mais il est possible que ce soit la même chose avec les versions iOS, Windows Phone ou Blackberry de l'application.**

## Configurer le WiFi sur votre Linux/BSD

À l'aide de votre gestionnaire de réseau WiFi, recherchez votre point d'accès généré au hasard et connectez-vous à celui-ci en utilisant le mot de passe généré dans l'application.

Vous serez alors connecté normalement, mais vous n'êtes pas encore prêt à naviguer sur le web comme avec un WiFi Tethering normal. Un proxy HTTP sera hébergé sur **http://192.168.49.1:8000** et vous n'aurez accès à l'internet que par ce biais.

## Naviguer sur le web

Si vous ne devez utiliser que votre navigateur web, il vous suffit de régler les paramètres de votre proxy sur **192.168.49.1:8000**.

**Dans Firefox**, allez dans **Préférences -> Proxy réseau -> Paramètres**, et remplissez vos paramètres de **Proxy manuel** pour :

<pre>
  Proxy HTTP : 192.168.49.1 

  Port : 8000
</pre>

**Pour Chromium ou Chrome**, vous définissez le proxy via la ligne de commande :

<pre>
chromium-browser --proxy-server="192.168.49.1:8000"
</pre>

Et n'oubliez pas de vérifier **Utilisez ce serveur proxy pour tous les protocoles**

## Utilisation d'Apt-get (Apt) avec PDAnet

Sur une distribution basée sur Debian, vous pouvez installer des mises à jour avec APT en configurant vos paramètres de proxy.

<pre>
  sudo nano /etc/apt/apt.conf.d/proxy.conf
</pre>

Ajoutez cette ligne à votre fichier **/etc/apt/apt.conf.d/proxy.conf** :

<pre>
  Acquire::http::Proxy "192.168.49.1:8000";
</pre>

Enregistrez le fichier **proxy.conf**. 

## Chaînes de proxy avec PDAnet

Vous pouvez forcer un programme à utiliser le proxy de votre PDA avec des chaînes de proxy.

Ajoutez vos serveurs à la fin de **proxychains.conf**, en supprimant tous les autres serveurs qui se trouvent dans le fichier :

<pre>
  [Liste de procurations]
  https 192.168.49.1 8000
</pre>

## Conclusion

**PDAnet** est un outil très pratique pour les voyageurs comme moi, mais la version d'essai a l'inconvénient de vous déconnecter toutes les 15 minutes. À moins que vous n'ayez besoin de brèves sessions de connexion sporadiques, cela vaut entièrement la licence de 15 $.

De plus, **veuillez ne pas abuser de votre connexion** avec les torrents, car vous ne savez jamais quelles autres méthodes de gestion du trafic votre transporteur va vous proposer.
