---
layout: post
title:  ALERTA: CANTV impulsa phishing contra plataforma voluntarios X Venezuela, poniendo en riego a disidentes y opositores.
small:  ALERTA: CANTV impulsa phishing contra plataforma
excerpt: Hemos identificado y seguimos analizando un grave caso de phishing impulsado, al menos en parte, por el ISP estatal de Venezuela CANTV
permalink: /noticias/alerta-phishing_voluntariado/
date:   2019-02-12 17:20:00 -0400
categories: bloqueos
image: 
author: "Andrés Azpúrua (Venezuela Inteligente / VEsinFiltro)"
---

Hemos identificado y seguimos analizando un grave caso de phishing impulsado, al menos en parte, por el ISP estatal de Venezuela CANTV https://voluntariosxvenezuela.com. Un portal asociado a la oposición venezolano para el registro de voluntarios en la distribución de ayuda humanitaria.

Este caso es sumamente grave por la historia de percusión a activistas, manifestantes y opositores en Venezuela; particularmente el uso de listas de ciudadanos usadas para discriminar en contra de opositores al gobierno.

Esta campaña de phishing utiliza un sitio web virtualmente idéntico al original para captar los datos de voluntarios y es impulsada por técnicas sofisticadas de interceptación y _spoofing_ DNS en la red de CANTV/Movilnet.

Desde tempranas horas de la tarde hemos estado alertando a los usuarios para que tengan cuidado y no sedan su información privada en el sitio falso colocado para engañarlos.

Los usuarios de CANTV intentan navegar a https://voluntariosxvenezuela.com (hospedado en AWS) *terminan accediendo a otro servidor completamente distinto,* porque las respuestas DNS sobre ese dominio apuntan a 159.65.65.194, la dirección IP del servidor que hospeda el sitio falso.

En CANTV *todo el tráfico DNS está siendo inspeccionado y cualquier solicitud por el IP de voluntariosxvenezuela.com es interceptada y el equipo recibe una respuesta forjada*, esto incluye tráfico a servidores DNS externos a CANTV, como 8.8.8.8 y 1.1.1.1 así como servidores DNS inexistentes.

El servidor en 159.65.65.194 está hospedado en Digital Ocean y responde al dominio voluntariovenezuela.com (sin la s y sin x) además de voluntariosxvenezuela.com. Tiene un certificado SSL para el dominio falso con el que intentan confundir.

Cuando el usuario de CANTV intenta navegar al dominio real en na conexión insegura (HTTP) el servidor malicioso redirije a www.voluntariovenezuela.com, si accede mediante una conexión HTTPS el navegador mostrará una alerta indicado la consistencias entre el dominio navegado y el del certificado. Si el usuario navega directamente al sitio malicioso no tendrá forma de saber que no es el sitio correcto.

VE sin Filtro publicará mañana un informe más completo de estos hallazgos.

## Recomendaciones

Es sumamente importante reconocer el URL (dirección)del sitio que uno esta visitando y asegurarse que haya una conexión segura (HTTPS://) sin errores o alertas de parte del navegador. Si el navegador dice que no es segura, desconfía inmediatamente del sitio.

Los administradores de sitios similares deben asegurarse de colocar certificados SSL y usar DNSsec para minimizar las probabilidades de éxito phishing (engaños dirigidos) a sus usuarios

Para acceder sitios bloqueados o inaccesibles en Venezuela tenemos estas recomendaciones generales