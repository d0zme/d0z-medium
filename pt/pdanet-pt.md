---
title: A maneira mais fácil de usar PDAnet com Linux ou BSD para amarrar ilimitadamente
layout: post
image: https://i.imgur.com/wLMcNre.jpg
permalink: /pt/pdanet-linux-freebsd-unix
---

Os dados móveis estão a ficar mais baratos & rápidos, e provavelmente tem uma oferta ilimitada de 4G/5G na sua área local. Normalmente vem com um apanhado de atribuições de dados severamente limitados para amarrar, e por vezes não é permitido de todo.

[PDAnet](https://pdanet.co) é a forma mais fácil, e provavelmente a mais popular, de evitar amarrar os limites de dados. Têm uma aplicação elegante para Windows & Mac OSX que lhe permite amarrar com apenas alguns cliques. Para os utilizadores de Linux, FreeBSD, ou Chrome OS, ficamos por nossa conta.

Felizmente, se o seu computador *nix tiver um adaptador Wifi funcional, não é tão difícil de configurar.

## Configurar PDAnet o seu telefone

O PDAnet está disponível através da Play Store, App Store, por isso é bastante simples de instalar. [binários APK](http://pdanet.co/install/) também estão disponíveis no seu site oficial no caso de não ter outros meios para a instalar.

Abra a aplicação, e Clique na caixa de verificação para **"WiFi Direct Hotspot (novo!) "** para criar um ponto de acesso.

Deverá então ver o texto destacado a azul no topo. Tome nota dos campos **Nome** e **Senha**, pois são sempre gerados aleatoriamente, pelo que terá de os digitar manualmente em cada vez.

**Só testei isto com o Android, mas é possivelmente o mesmo com as versões iOS, Windows Phone, ou Blackberry da aplicação.**

## Configurando o WiFi na sua caixa Linux/BSD

Usando o seu gestor de rede WiFi, procure o seu ponto de acesso gerado aleatoriamente e ligue-se a ele usando a palavra-passe gerada na aplicação.

Será então ligado normalmente, mas ainda não está preparado para navegar na web como com o Tethering WiFi normal. Um proxy HTTP será alojado em **http://192.168.49.1:8000*** e só terá acesso à Internet através dele.

## Navegando na web

Se precisar apenas de utilizar o seu navegador web, basta definir as suas definições de proxy para **192.168.49.1:8000***.

**No Firefox***, vá a **Preferências -> Network Proxy -> Settings**, e preencha as suas **Proxy Manual*** configurações para:

>pre>
  Proxy HTTP: 192.168.49.1 

  Porto: 8000
</pre>

**Para Crómio ou Crómio**, definirá o proxy através da linha de comando:

<pre>
chromium-browser --proxy-server="192.168.49.1:8000"
</pre>

E não se esqueça de verificar **Utilizar este servidor proxy para todos os protocolos***.

## Usando Apt-get (Apt) com PDAnet

Numa distro baseada em Debian, pode instalar actualizações com APT, configurando as suas definições de proxy.

<pre>
  sudo nano /etc/apt/apt.conf.d/proxy.conf
</pre>

Adicione esta linha ao seu ficheiro **/etc/apt/apt.conf.d/proxy.conf***:

<pre>
  Acquire::http::Proxy "192.168.49.1:8000";
</pre>

Guardar o ficheiro **proxy.conf***. 

## Proxychains com PDAnet

Pode forçar um programa a utilizar o seu PDA proxy com cadeias de proxy.

Adicione os seus servidores ao final de **proxychains.conf**, removendo quaisquer outros servidores que por acaso estejam no ficheiro:

<pre>
  [ProxyList]
  https 192.168.49.1 8000
</pre>

## Envolvimento

**PDAnet*** é uma ferramenta elegante para viajantes como eu, mas a versão experimental tem a parte irritante de o desligar de 15 em 15 minutos. A menos que precise apenas de sessões breves e esporádicas de amarração, vale inteiramente a licença de $15.

Além disso, **por favor, não abuse da sua ligação** com torrentes, pois nunca se sabe que outros métodos de formação de tráfego o seu portador lhe irá chamar a atenção.
