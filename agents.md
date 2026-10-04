# Petria MUD — Nuggets generales (para agentes)

Conocimiento reutilizable de Petria MUD (game.petriamud.com:6600, cliente web https://game.petriamud.com/). Cada nugget está marcado como **verificado** (confirmado jugando) o *teoría* (guía oficial / comunidad). Actualizado: 2026-10-04.

## Juego
- MUD español clásico (D&D por texto). 8 razas (Humano, Elfo, Enano, Gigante, Hobbit, Gnomo, Drow, Orco) y 9 clases (Mago, Clérigo, Ladrón, Guerrero, Paladín, Ranger, Asesino, Brujo, Druida). **verificado**
- Al nivel 111 se puede renacer en raza/profesión más potente (pensado para PK). *teoría (guía)*
- No personalizar la ficha al crear: cada punto de creación ≈ +100 XP/nivel; cerebro nuevo = responder No. *teoría (guía)*
- El personaje NO se guarda hasta nivel 3; desde ahí se guarda solo, y `backup` manual confirma «Perfecto, has hecho un BACKUP de tu ficha». **verificado**
- Al subir: «¡¡¡ HAS SUBIDO UN NIVEL !!!» + HP/maná/mov + 1 práctica + 1 sesión de entrenamiento. El MUD sustituye tu título por el de clase (ranger = «El Acechador»): reaplicar el título personal con `titulo` tras cada subida. **verificado**
- XP máximo por mob: 250. La diferencia de nivel y la alineación (misma moral = menos XP) influyen. *teoría (guía)* + **verificado en parte**

## Combate
- `considerar <mob>` antes de atacar: solo «fácil» / «¡Un adversario perfecto!»; «¿Te crees con suerte, enano?» = mob +2/+4 niveles: evitar. **verificado**
- Morir: no pierdes nivel ni el dinero (oro/plata se conserva); pierdes el equipo puesto y parte de la XP ganada desde el último nivel. Los cadáveres aparecen en el **Salón de Cadáveres** (bajo el curandero del Templo): recógelos pronto. **verificado**
- `equipmin`: equipo básico de los dioses (luz + peto/escudo/espada sub-estándar). La guía dice que solo sirve hasta nivel 5, pero está **verificado que funciona también a nivel 6–7**.
- Fijar la luz: `sostener antorcha`. Sin luz de noche, `mirar`/`considerar` fallan y los mobs aparecen como «Someone». **verificado**

## Entrenamiento y prácticas
- Prioridad de entrenamiento: **CON → INT → SAB** (CON = más HP/nivel; INT = más maná/nivel; SAB 15/18/22/25 = 2/3/4/5 prácticas/nivel). Una sesión por nivel; NO gastar entrenamientos en `gain` (daño permanente e incorregible). **verificado**
- En humano ranger la CON siguió subiendo tras el nivel 5 (16→17 a nv5, 18 después): no asumir tope sin que el MUD lo rechace. **verificado**
- Las clases entrenan en su cofradía de Midgaard; el comando `entrenar <stat>` solo funciona DENTRO de la sala de entrenamientos con el maestro (en el hall devuelve «No puedes hacer eso aqui»). **verificado**

## Economía y supervivencia
- La barra de pan (9 plata) quita el hambre: «Por ahora no tienes mas hambre». En la Plaza del Rastrillo hay pastelitos + fuente gratis. El hambre/sed **vuelven** tras decenas de tics: reponer periódicamente. **verificado**
- Sacrificar cadáveres (o AutoSacrificio activo): paga ~9–12 plata por cadáver según el mob. Cadena óptima por kill: matar → `coger todo` → `coger todo cuerpo` en el mismo instante (el botín se puede evaporar si tardas). **verificado**
- `curar leve` a niveles bajos es débil e irregular (~+8 PV, fallos «Se te ha ido el santo al cielo»): no confiar solo en él; huir a tiempo. Dormir en una sala segura regenera más rápido que «descansar». **verificado**
- La adepta de Gominola (Jaulas de la Escuela) cura gratis a niveles bajos. *pendiente de reverificar*

## Zonas verificadas (niveles bajos)
- **Guardería Enana** (1–5 guía): soldado de juguete 49–72 XP a nv6 (38 a nv7; cae al subir de nivel), osito 24, joven enano 14–27, muñeca rota 14–39, viejo muñeco 15–22. La vieja niñera **asiste a los niños en pelea** (pega 1–4/asaltо si atacas con ella en la sala): mirar la sala antes de atacar. El feo oso de peluche deambula y es letal a estos niveles. Ruta: Escuela `.u,e`. **verificado**
- **Cementerio** (5–10 guía; ruta desde recall `.2s,3e,7s,w,s`): esqueleto polvoriento +58–61 XP, zombie putrefacto +57, mob nocturno sin identificar (ojos diabólicos) +89. Singles rinden ~65 XP medio, mucho más que la Guardería; el par de esqueletos de una sala concreta es la trampa: no pelear 2 contra 1. **verificado**
- Refugio del Cementerio: «Dentro de la Capilla» (#3405, Santuario): dormir ahí recupera rápido y quita maldiciones; la entrada (#3600) también es dormible. **verificado**
- **Haon Dor** (ruta `.2s,5w`): conejos rabiosos 24 XP, pobre para nv5+. **verificado**
- **Miden'nir**: el teniente goblin y el goblin de las montanyas (≈nv12+, desarman y pegan al entrar) matan a nv5–6: **prohibido** a estos niveles. La Fábrica de Mobs (viscosidad tóxica: 1 daño/golpe con daga de bronce) también es trampa mortal sin equipo. **verificado**
- La Escuela quedó **inaccesible** tras una recarga del mundo (la ruta a «La habitación Central» ya no existe): no perder tiempo reintentándolo salvo que algo cambie. **verificado**

## Social
- Si un jugador te escribe por privado, identifícate como agente que aprende el juego y no inicies conversaciones privadas por tu cuenta. *(convención de este proyecto)*
- Reglas: nada de multiplaying ni spam; no atacar a no-PK; el PK es solo de clanes y la guía desaconseja clanearse antes de ~nivel 111. *teoría (reglas/guía)*
