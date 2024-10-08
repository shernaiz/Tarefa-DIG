# Tarefa-DIG

**1-Realiza unha consulta `dig danielcastelao.org` e identifica cada parte da resposta (IN, CNAME, A, QUERY SECTION, AUTHORITY SECTION, etc)**
    Ao lanzar o comando anterior, como resposta imos ver un montón de información.
    -*IN* indicarnos que se trara dun rexistro de internet.
    -*A* esta letra indicaranos o tipo de rexistro, e indica que contén a dirección IP que está asignada ao domino que indicamos ao lanzar o coamndo.
    - *QUERY SECTION* esta refírese a sección de pregunta, mostrará a consulta que se realizou indicando o dominio e a clase da consulta, neste caso _IN_.
    - *AUTHORITY SECTION* esta sección indicara os servidores de nomes de autoridade para o dominio indicado. Estos son os servidores encargados de responder as consultas sin embarno na consulta que lanzamos non aparece esta sección.
    - *QUERY TIME* aquí mostrarase o tempo que tardou a consulta en realizarse, neste caso foron _163 msec_.
    - *SERVER* indica o servidor DNS empregado para a consulta, neste caso foi o _127.0.0.53_.
    Ademáis nesta seccióin encontrarase máis información como *WHEN*, que indicara a fecha e hora na que se realizou a consulta e *MSG SIZE* que indica o tamaño da resposta recivida.

**2-Realiza consultas dos seguintes nomes e identifica as diferencias:**
    **`moodle.danielcastelao.org`**
    **`www.danielcastelao.org`**
    Ao realizar as duas consultas podemos observar varias diferencias.
    -> A primeira diferencia que vemos e na sección da cabeceira, na seccion de *STATUS* podemos ver que na consulta de moodle responde *NXDOMAIN* esto implica que o dominio ou non existe ou non o pode atopar no DNS.
    -> Na misma sección na parte de *ANSWER* podemos comprobar que tamén a consulta de moodle dinos que ten 0 respostas.
    -> Na sección de *ANSWER* podemos comprobar tamén que na consulta de moodle non nos aparece ningunha dirección IP.
    -> Na consulta de moodle sin embargo si que nos aparece a sección *AUTHORITY SECTION* onde nos aparece _danielcastelao.org_ sin embargo na coutra consulta non nos mostra esta sección.

**3-Averigua o nome e IP dos servidores de DNS autoritativos de `www.danielcatelao.org`, por qué soen ser 2 servidores autoritativos?**
    Como ao lanzar dig directamente ca dirección non nos aparece a sección de *AUTHORITY SECTION* teremos que lanzar a consulta da seguinte forma _dig NS www.danielcastelao.org_. 
    A resposta que obteremos serán dúas direccións `ns1.hover.com` e `dnsmaster.hover.com`. Os servidores autoritativos sempre serán dous ou mais para tratar de garantizar a seguridade, redundancia e a dispoñibilidade, isto garantiza que se un falla, o outro pode dar servicio, ademáis que se estos servidores se están localizados en diferentes puntos xeográficos facilitarán a dispoñibilidade do servicio.
    Para conocer a dirección destos servidores podemos lanzar o comando `dig` e o nome dos servidores.
    -> `ns1.hover.com` a dirección IP é `216.40.47`
    -> `dnsmaster.hover.com` a dirección IP é `216.40.34.41`

**4-Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran**
    Para facer as consultas de nomes á inversa teremos que escruibir o comando `dig` coma antes pero empregaremos o modificador `-x`, quedando o comando tal que así `dig -x 130.206.164.68`.
    Consultas realizadas:
        -> `104.18.5.124`
        -> `2.22.221.49`

**5-A que servidor DNS estás consultando? Cómo podes cambiar sen tocar os ficheiros de configuración do sistema?**
    Para saber o servidor ao que estamos consultando poderíamos velo en calquera das consultas anteriores, na última sección móstranos o servidor ao que estamos consultando, de todas formas podemos volver a lanzar o comando por exemplo a google para observar esto. 
    O servidor ao que estamos consultando é o  `127.0.0.53`.
    Esto é unha dirección de loopback xa que realizamos a consulta desde unha máquina virtual, en caso de facelo desde a máquina original a dirección do servidor DNS será o `8.8.8.8`.

**6-Obtén o rexistro SOA (Start of Authority) do dominio `moodle.danielcastelao.org` preguntándolle ó servidor DNS de google e logo preguntándollo directamente ó servidor primario do dominio danielcastelao.org**
    Para obter o rexistro SOA do dominio moodle teremos que lanzar o comando dig acompañado das letras SOA da seguinte forma `dig moodle.danielcastelao.org SOA` e nos mostrará unha información similar as anteriores consultas.
    Para facer a consulta ó servidor DNS de google teremos que escribir o comando de antes pero indicándolle o DNS de google da seguinte forma `dig @8.8.8.8 moodle.danielcastelao.org`.
    Para facelo ao servidor primario do dominio teremos que facer teríamos que lanzar o comando dig normal ca dirección de `danielcastelao.com` o que nos dirá que o servidor primario e o `ns1.hover.com`. Unha vez feito esto termos que lanzar o comando de antes pero co novo nome da seguinte forma `dig @ns1.hover.com moodle.danielcastelao.org SOA`.
    
**7-Consulta a IP de www.elpais.com. Cánto tempo queda almacenado o rexistro de recurso no DNS local? Se preguntas o DNS local por este recurso, que observas no TTL do rexistro**

**8-Busca o TTL de distintos nomes de dominio de servicios que escollas, a qé se polden deber as diferencias?**

**9-Determina o TTL máximo (original) dun nome de dominio.**

**10-Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, semore son as mesmas e na mesma orde? por que?**

**11-Pregunta o mesmo a un server raiz (J:ROOTSERVERS.NET) e comproba na respota se o server acepta o modo recursivo**

**12-Se queremos ver todas as queies que fai o servidor de DNS, que opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados**

**13-Usando a información dispñible a traves do DNs especifica a máquina (nome e IP) iu máquinas que actúan como servers de correo do dominio danielcastelao.org**

**14-Podes obter os rexistros AAAA de www.facebook.com? a que corresponden?**

