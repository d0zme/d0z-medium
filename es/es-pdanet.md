---
title: La forma más fácil de usar PDAnet con Linux o BSD para ataduras ilimitadas
layout: post
image: https://i.imgur.com/wLMcNre.jpg
permalink: /es/pdanet-linux-freebsd-unix
---

Los datos móviles son cada vez más baratos y rápidos, y probablemente tengas una oferta de 4G/5G ilimitada en tu área local. Normalmente viene con una captura de asignaciones de datos severamente limitadas para la inmovilización, y a veces no está permitido en absoluto.

[PDAnet](https://pdanet.co) es la forma más fácil, y probablemente la más popular de evitar las tapas de datos de ataduras. Tienen una ingeniosa aplicación para Windows y Mac OSX que permite atar con sólo unos pocos clics. Para los usuarios de Linux, FreeBSD, o Chrome OS, tenemos que resolverlo por nuestra cuenta.

Afortunadamente, si tu ordenador *nix tiene un adaptador Wifi que funciona, no es tan difícil de configurar.

## Configurando PDAnet tu teléfono

PDAnet está disponible a través de la Play Store, App Store, por lo que es bastante sencillo de instalar. Los [binarios APK](http://pdanet.co/install/) también están disponibles en su sitio web oficial en caso de que no tengas otro medio para instalarlo.

Abre la aplicación, y haz clic en la casilla de verificación de **"WiFi Direct Hotspot (¡nuevo!) "** para crear un punto de acceso.

Entonces deberías ver el texto resaltado en azul en la parte superior. Toma nota de los campos **Nombre** y **Contraseña** ya que siempre se generan al azar, por lo que tendrás que escribirlos manualmente cada vez.

**Sólo he probado esto con Android, pero posiblemente sea lo mismo con las versiones de iOS, Windows Phone o Blackberry de la aplicación.**

## Configurando WiFi en tu caja de Linux/BSD

Utilizando el gestor de la red WiFi, busca tu punto de acceso generado aleatoriamente y conéctate a él utilizando la contraseña generada en la aplicación.

Entonces estarás conectado como de costumbre, pero aún no estás listo para navegar por la web como con la conexión WiFi normal. Un proxy HTTP estará alojado en **http://192.168.49.1:8000** y sólo tendrás acceso a Internet a través de él.

## Navegando por la web

Si sólo necesita usar su navegador web, simplemente establezca la configuración del proxy en **192.168.49.1:8000**.

**En Firefox**, vaya a **Preferencias -> Proxy de red -> Configuración**, y rellene su **Proxy manual** configuración a:

<pre>
  Proxy HTTP: 192.168.49.1 

  Puerto: 8000
</pre>

**Para el Cromo o el Cromo**, establecerás el proxy a través de la línea de comandos:

<pre>
chromium-browser --proxy-server="192.168.49.1:8000"
</pre>

Y asegúrate de comprobar **Utiliza este servidor proxy para todos los protocolos**

## Usando Apt-get (Apt) con PDAnet

En una distribución basada en Debian, puede instalar actualizaciones con APT configurando su configuración de proxy.

<pre>
  sudo nano /etc/apt/apt.conf.d/proxy.conf
</pre>

Añade esta línea a tu archivo **/etc/apt/apt.conf.d/proxy.conf**:

<pre>
  Acquire::http::Proxy "192.168.49.1:8000";
</pre>

Guarda el archivo **proxy.conf**. 

## Proxychains con PDAnet

Puede obligar a un programa a usar el proxy de su PDA con cadenas de proxy.

Añade tus servidores al final de **proxychains.conf**, eliminando cualquier otro servidor que esté en el archivo:

<pre>
  [ProxyList]
  https 192.168.49.1 8000
</pre>

## Wrapping up

**PDAnet** es una herramienta ingeniosa para viajeros como yo, pero la versión de prueba tiene la parte molesta de desconectarte cada 15 minutos. A menos que sólo necesites sesiones de atadura breves y esporádicas, vale la pena la licencia de 15 dólares.

Además, **por favor no abuse de su conexión** con los torrentes, ya que nunca se sabe qué otros métodos de control de tráfico su compañía aérea le va a dar.


Traducción realizada con la versión gratuita del traductor www.DeepL.com/Translator
