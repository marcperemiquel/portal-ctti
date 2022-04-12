+++
date = "2022-04-11"
title = "Canigó. Publicació nova versió 3.6.4"
description = "S'ha publicat la nova versió de Canigó 3.6.4 per a corregir la vulnerabilitat Spring4Shell detectada (entre d'altres)"
#sections = ["Notícies", "home"]
#categories = ["canigo"]
#key = "MAIG2022"
+++

S'ha alliberat la **versió 3.6.4 del Framework Canigó** per a actualitzar `org.springframework` de 5.3.9 a 5.3.18 i
`org.springframework.boot` de 2.5.4 a 2.5.12 amb l'objectiu de corregir la vulnerabilitat detectada.

Podeu consultar l'abast complet de les noves versions a les [Release Notes 3.6](/canigo-download-related/release-notes-canigo-36).

## Introducció Spring

**Spring Framework és un marc d'aplicació de codi obert per a la plataforma Java** les característiques de la qual poden
ser utilitzades per qualsevol aplicació.

## Vulnerabilitat Spring4Shell

Sobre aquest tema, **el passat 29 de març es va publicar una nova vulnerabilitat d'execució remota de codi que afecta a
Spring Core**, un framework que permet el desenvolupament d'aplicacions web amb Java i, l'explotació de les quals
permetria a atacants executar remotament codi arbitrari en els sistemes de la víctima per mitjà d'una petició
no autenticada d'HTTP.

Aquesta vulnerabilitat és coneguda sota el nom de Spring4Shell o SpringShell i afecta a spring-*core que, segons els investigadors
de Praetorian, es tracta d'un bypass per a una CVE més antiga [CVE-2010-1622](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2010-1622)
quea causa d'una característica de JDK9 pot haver estat restablerta.

En aquest sentit, les aplicacions de Spring que s'executen amb Jdk 9 o superior només es veuen afectades si es compleixen
una sèrie de requisits perquè l'aplicació sigui vulnerable, a saber:

- Utilitzar Spring Beans.

- Utilitzar Spring Parameter Binding.

- Almenys, un Spring Parameter Binding ha d’estar configurat per utilitzar un tipus de paràmetre no bàsic.

Les vulnerabilitats detectades són les següents:

- Spring4Shell [CVE-2022-22965](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-22965): es tracta d'una vulnerabilitat
crítica que permet l'execució remota de codi arbitrari en els sistemes de la víctima per mitjà d'una petició no atenticada d'HTTP.

- [CVE-2022-22963](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-22963): es tracta d'una vulnerabilitat de gravetat mitja
a Spring Cloud Function que pot ser explotada per accedir als recursos locals.

- [CVE-2022-22950](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-22950): es tracta d'una vulnerabiliatat de DoS de
gravetat mitja que afecta a Spring Framework.

S'ha publicat la **versió 5.3.18 de `org.springframework` i la versió 2.5.12 de `org.springframework.boot` per a mitigar aquestes vulnerabilitats**.

Per més informació podeu consultar [Spring Framework RCE](https://spring.io/blog/2022/03/31/spring-framework-rce-early-announcement).

Des de l'Agència de Ciberseguretat de la Generalitat s'han considerat aquestes vulnerabilitats com a crítiques i d'un potencial
gran impacte, recomanant als usuaris i administradors de sistemes que prenguin mesures de forma urgent.

## Canigó 3.6.4

S'han publicat tots els mòduls del Framework Canigó 3.6 perquè passin a fer ús de la **versió 5.3.18 de `org.springframework`
i la versió 2.5.12 de `org.springframework.boot` per a mitigar aquestes vulnerabilitats** alliberant la corresponent nova
versió 3.6.4.

Podeu consultar la informació de les versions a: [Binaris Canigó 3.6](/canigo/download/canigo-36/).

Podeu consultar les matrius de compatibilitat de cada mòdul a: [Matriu compatibilitat Canigó 3.6]
(/canigo-download-related/matrius-compatibilitats/canigo-36/).

Des de CS Canigó es recomana actualitzar-se de forma urgent a aquestes versions de Canigó i/o seguir les
indicacions del [Howto vulnerabilitat Log4j](/howtos/2021-12-13-Howto-canigo-log4jshell/)
per a resoldre aquestes vulnerabilitats.

<br/><br/>
Per qualsevol dubte relatiu a aquesta nova versió del Framework Canigó us podeu posar en contacte amb el CS Canigó
al [servei CAN](https://cstd.ctti.gencat.cat/jiracstd/projects/CAN) del JIRA CSTD o enviant-nos un correu electrònic
a la [bústia del CS Canigó](mailto:oficina-tecnica.canigo.ctti@gencat.cat).