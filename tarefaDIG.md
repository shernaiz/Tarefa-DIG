# Tarefa-DIG

## 1-Realiza unha consulta `dig danielcastelao.org` e identifica cada parte da resposta (IN, CNAME, A, QUERY SECTION, AUTHORITY SECTION, etc)

Ao lanzar o comando anterior, como resposta imos ver un montón de información.

*IN* indicarnos que se trara dun rexistro de internet.

*A* esta letra indicaranos o tipo de rexistro, e indica que contén a dirección IP que está asignada ao domino que indicamos ao lanzar o coamndo.

*QUERY SECTION* esta refírese a sección de pregunta, mostrará a consulta que se realizou indicando o dominio e a clase da consulta, neste caso _IN_.

*AUTHORITY SECTION* esta sección indicara os servidores de nomes de autoridade para o dominio indicado. Estos son os servidores encargados de responder as consultas sin embarno na consulta que lanzamos non aparece esta sección.

*QUERY TIME* aquí mostrarase o tempo que tardou a consulta en realizarse, neste caso foron _163 msec_.

*SERVER* indica o servidor DNS empregado para a consulta, neste caso foi o _127.0.0.53_.

Ademáis nesta seccióin encontrarase máis información como *WHEN*, que indicara a fecha e hora na que se realizou a consulta e *MSG SIZE* que indica o tamaño da resposta recivida.

## 2-Realiza consultas dos seguintes nomes e identifica as diferencias:
## `moodle.danielcastelao.org`
## `www.danielcastelao.org`

Ao realizar as duas consultas podemos observar varias diferencias.
    
A primeira diferencia que vemos e na sección da cabeceira, na seccion de *STATUS* podemos ver que na consulta de moodle responde *NXDOMAIN* esto implica que o dominio ou non existe ou non o pode atopar no DNS.

Na misma sección na parte de *ANSWER* podemos comprobar que tamén a consulta de moodle dinos que ten 0 respostas.

Na sección de *ANSWER* podemos comprobar tamén que na consulta de moodle non nos aparece ningunha dirección IP.

Na consulta de moodle sin embargo si que nos aparece a sección *AUTHORITY SECTION* onde nos aparece `danielcastelao.org` sin embargo na coutra consulta non nos mostra esta sección.

## 3-Averigua o nome e IP dos servidores de DNS autoritativos de `www.danielcatelao.org`, por qué soen ser 2 servidores autoritativos?

Como ao lanzar dig directamente ca dirección non nos aparece a sección de *AUTHORITY SECTION* teremos que lanzar a consulta da seguinte forma _dig NS www.danielcastelao.org_. 

A resposta que obteremos serán dúas direccións `ns1.hover.com` e `dnsmaster.hover.com`. Os servidores autoritativos sempre serán dous ou mais para tratar de garantizar a seguridade, redundancia e a dispoñibilidade, isto garantiza que se un falla, o outro pode dar servicio, ademáis que se estos servidores se están localizados en diferentes puntos xeográficos facilitarán a dispoñibilidade do servicio.

Para conocer a dirección destos servidores podemos lanzar o comando `dig` e o nome dos servidores.

`ns1.hover.com` a dirección IP é `216.40.47`

`dnsmaster.hover.com` a dirección IP é `216.40.34.41`

## 4-Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran

Para facer as consultas de nomes á inversa teremos que escruibir o comando `dig` coma antes pero empregaremos o modificador `-x`, quedando o comando tal que así **dig -x 130.206.164.68**.

Consultas realizadas:

`104.18.5.124`

`2.22.221.49`

## 5-A que servidor DNS estás consultando? Cómo podes cambiar sen tocar os ficheiros de configuración do sistema?

Para saber o servidor ao que estamos consultando poderíamos velo en calquera das consultas anteriores, na última sección móstranos o servidor ao que estamos consultando, de todas formas podemos volver a lanzar o comando por exemplo a google para observar esto. 

O servidor ao que estamos consultando é o  `127.0.0.53`.

Esto é unha dirección de loopback xa que realizamos a consulta desde unha máquina virtual, en caso de facelo desde a máquina original a dirección do servidor DNS será o `8.8.8.8`.

Para cambiar o servidor ao que estamos consultando teremos que facer a consulta pero indicando a que servidor queremos acceder, por exemplo **dig @8.8.8.8 www.danielcastelao.org**. Esto fará a consulta desde o DNS indicado.

## 6-Obtén o rexistro SOA (Start of Authority) do dominio `moodle.danielcastelao.org` preguntándolle ó servidor DNS de google e logo preguntándollo directamente ó servidor primario do dominio danielcastelao.org

Para obter o rexistro SOA do dominio moodle teremos que lanzar o comando dig acompañado das letras SOA da seguinte forma **dig moodle.danielcastelao.org SOA** e nos mostrará unha información similar as anteriores consultas.

Para facer a consulta ó servidor DNS de google teremos que escribir o comando de antes pero indicándolle o DNS de google da seguinte forma **dig @8.8.8.8 moodle.danielcastelao.org**.

Para facelo ao servidor primario do dominio teremos que facer teríamos que lanzar o comando dig normal ca dirección de `danielcastelao.com` o que nos dirá que o servidor primario e o `ns1.hover.com`. Unha vez feito esto termos que lanzar o comando de antes pero co novo nome da seguinte forma **dig @ns1.hover.com moodle.danielcastelao.org SOA**.
    
## 7-Consulta a IP de `www.elpais.com`. Cánto tempo queda almacenado o rexistro de recurso no DNS local? Se preguntas o DNS local por este recurso, que observas no TTL do rexistro

Para saber o tempo que queda almacenado o rexistro de recurso no DNS teremos que volver a lanzar o comando dig ca dirección indicada. Na sección de *ANSWER* podremos ver a dirección consultada e ao lado un número. Este número indicará o tempo que permanecerá almacenado. Neste casó será *115* o que sería **1 minuto e 15 segundos**

## 8-Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se polden deber as diferencias?

O TTL dos servidores vai variando dependendo de si o DNS cambia con frecuencia, o que faría que tivera un TTL máis baixo, ou o contrario, o TTL alto indicaría que o servidor DNS a penas cambia.

Isto pódese ver por exemplo ao facer un dig de `www.wikipedia.es`que ten un TTL **21600** en contraposición de o de `www.google.com` que ten un TTL de **219**.

## 9-Determina o TTL máximo (original) dun nome de dominio.

Para determinar o TTL máximo dun nome de dominio teremos que volver a lanzar o comando dig, e mostrarános o TTL, para asegurarnos de que estamos vendo o orixinal, teremos que facer o comando dig pero co servidor autoritativo. 

Neste caso por exemplo sería primeiro lanzar o comando para identificar o servidor autoritativo `dig wwww.google.es SOA` que nos dará o servidor autoritario, unha vez identificado faremos o seguinte comando **dig @ns1.google.com www.google.es SOA**, esto mostraranos o TTL orixinal, que sería de **60**.

## 10-Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por que?

Para coñecer cántas máquinas con distintas IPs están detrás dun dominio teremos que lanzar o comando dig co modificador _+short_ da seguinte forma **dig +short www.google.es**. Isto contestará cas IPs que están detrás do dominio.

No caso de google darános unha dirección IP e sempre será a misma.

**11-Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET) e comproba na respota se o server acepta o modo recursivo**

Se preguntamos o mesmo pero a un servidor raiz co comando **dig @a.root-server.net www.google.es** mostraranos un bloque de información adicional onde podremos ver varias direccións IP e MAC.

Na sección de cabeceira da resposta podremos ver como aparece a seguinte mensaxe _*WARNING*: recursion requested but not avaliable_ o que nos indica que o server NON acepta o modo recursivo.

**12-Se queremos ver todas as queries que fai o servidor de DNS, que opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados**

Para ver todas as consultas que fai o servidor DNS nn podremos usar o comando dig xa que non o contempla, teremos que usar algun outro programa que si nos permita ver todo o tráfico como por exemplo _wireshark_

Se lanzamos o seguinte comando **dig www.timesonline.co.uk SOA** diranos o serpvidor autoritario do dominio. Unha vez obtido o servidor teremos que lanzar o seguinte comando **dig @ns-1826.awsdns-36.co.uk www.timesonline.co.uk**.

Cando nos responda, na información do final veremos a IP do server ao que estamos consultando, neste caso a IP sería **205.251.199.34**.

## 13-Usando a información dispoñible a traves do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org

Para ver os nomes das máquinas que actúan como servers de dominio teremos que lanzar o comando **dif danielcastelao.org mx**. Unha vez feito para comprobar as direccións IP teremos que lanzar o ocmando dig pero empleando o server do que queremos averguar a dirección IP, neste caso son os seguintes:

**aspmx4.googlemail.com** --> 142.250.150.26

**aspmx.l.google.com** --> 64.233.166.27

**aspmx2.googlemail.com** --> 142.250.153.27

**alt2.aspmx.l.google.com** --> 142.251.9.26

**aspmx3.googlemail.com** --> 142.251.9.27

**alt1.aspmx.l.google.com** --> 142.250.153.27

**aspmx5.googlemail.com** --> 74.125.200.27

**14-Podes obter os rexistros AAAA de www.facebook.com? a que corresponden?**

Se lanzamos o comando **dig @a.root-servers.net www.facebook.com** podremos ver os rexistros A e AAAA, os primeiros corresponderán a dirección *IPv4* e os AAAA corresponderán as direccións *IPv6*.

