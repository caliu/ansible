# Ansible per als servidors de Caliu

## Com utilitzar aquest repositori

Podeu fer propostes de canvis sempre que vulgueu, però només hauríeu
d'acceptar-les o fer canvis directament a la branca `main` si sou
masover.

Necessitareu tenir instal·lat `ansible` localment. Trobareu documentació
sobre com funciona ansible a <http://docs.ansible.com/>. La versió que
heu d'utilitzar és la 2.7 com a mínim (és la que porta Debian 10). Podeu
utilitzar versions posteriors però assegureu-vos que no es perd la
compatibilitat.

El model bàsic és que ansible utilitza ssh per comunicar-se amb els
servidors que voleu configurar per copiar-hi scripts de python
especialitzats en fer les tasques necessàries. Per tant, us caldrà
utilitzar l'ansible des d'un lloc on tingueu la clau privada que us
doni accés al servidor corresponent.

## Organització dels playbooks

El fitxer `site.yml` hauria de contenir les referències a tots els rols
d'ús general i hauria de ser idempotent, és a dir, hauria de reflectir
l'estat actual del sistema (es poden utilitzar altres fitxers per a
tasques especialitzades, si cal). Els _playbooks_ (`*.yml`) normalment
operen sobre un sol rol, tot i que alguns rols podrien referenciar-ne
d'altres mitjançant el directori `meta`.

En tots els casos, l'ansible s'executa directament sobre el directori
de treball del repositori.

*   Mostrar els canvis que s'executarien pels playbooks del repositori:

    $ ansible-playbook site.yml --check --diff --ask-become-pass

*   Aplicar els canvis de veritat:

    $ ansible-playbook site.yml --ask-become-pass

## Recomanacions i bones pràctiques

* En general és preferible no fer canvis directament a la configuració
  del sistema (habitualment sobre /etc o els paquets instal·lats) sense
  actualitzar ansible. Si per algun motiu això fos necessari, creeu una
  _issue_ per reflexar la divergència.
* Els canvis que efectueu s'haurien de publicar el més aviat possible al
  repositori remot, tant si és abans com després de fer-los, per poder
  compartir l'estat de la configuració amb la resta de l'equip.
* Comenteu els canvis que puguin generar controvèrsia amb l'equip dels
  masovers o mitjançant propostes de canvi.
