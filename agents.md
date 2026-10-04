# Petria MUD — agents.md (conocimiento general para agentes)

> Conocimiento reutilizable de Petria para CUALQUIER personaje/agente. Lo específico de un personaje vive en su propio archivo.
> Lo marcado **verificado** se confirmó jugando; el resto es teoría de la guía oficial hasta que una pasada lo confirme.
---

## 1. Qué es Petria

- MUD (Multi-User Dungeon) español clásico, RPG 100% texto estilo D&D.
- Creas un personaje, subes de nivel matando mobs (NPCs controlados por el servidor), exploras áreas, haces quests, te equipas, comercias y, a nivel alto, puedes entrar a clanes PK (player-killing).
- A nivel 111 existe la opción de **renacer** en raza/profesión más potente (pensado para PK).
- Comunidad activa en Discord y WhatsApp de ayuda a nuevos.
- Sitio oficial: https://www.petriamud.com
- Guía de principiantes (fuente principal de teoría): https://www.petriamud.com/wp-content/uploads/2024/08/guia_principiantes_v2.html
- Mapas y rutas: https://www.petriamud.com/mapas/
- Reglas: https://www.petriamud.com/reglas/

## 2. Cómo conectarse

| Vía | Datos |
|---|---|
| Servidor MUD | `game.petriamud.com` puerto `6600` |
| Cliente web | https://game.petriamud.com/ — Lociterm, se conecta por WebSocket `wss://game.petriamud.com/` y de ahí al MUD |
| Cliente recomendado por la comunidad | Mudlet (gratis) apuntando al mismo host/puerto |

### Flujo de entrada en el cliente web (verificado 2026-10-02)
1. Splash «Petria – Vive tu Leyenda / ✦ Comienza tu Aventura ✦» → clic o tecla para empezar; el cliente conecta solo.
2. Banner con castillo ASCII + `PETRIA` en letras grandes, web/Discord/host-puerto.
3. Pregunta: «Por que nombre quieres ser conocido? / What name would you like to use?»
4. Si el nombre es nuevo: «Nuevo personaje.» → pide password y confirmación.
5. Si el nombre ya existe: pide el password de ese personaje. Nunca probar variantes si falla: reportar el mensaje exacto.

## 3. Creación de personaje (flujo verificado)

Orden exacto de preguntas al crear (2026-10-02):

1. Nombre → 2. Idioma `[1] Español` → 3. Confirmar nombre (Sí) → 4. Password + repetir → 5. Modo accesible lector de pantalla (No) → 6. Raza (lista numerada) → 7. Sexo (M/F) → 8. Clase (lista numerada) → 9. Alineación (B/N/M) → 10. ¿Personalizar? (S/N) → 11. Arma inicial.

### Razas (8) y clases (9 en la lista actual)
- **Razas:** Humano, Elfo, Enano, Gigante, Hobbit, Gnomo, Drow, Orco.
- **Clases ofrecidas al crear:** Mago, Clérigo, Ladrón, Guerrero, Paladín, Ranger, Asesino, Brujo, Druida.
- La guía advierte: mago/clérigo/brujo son difíciles para empezar. **Recomendadas para principiante: Paladín o Ranger** (autosuficientes, equilibrio ataque/defensa). Humano es la raza más polivalente y sin debilidades específicas.
- **Personalización:** si eres nuevo, responder **No**. Personalizar mal sube el costo de XP por nivel. Regla de la guía: nunca pasar de 50–60 puntos de creación (cada punto ≈ +100 XP/nivel; pasado 60 cobra el doble).
- **Arma inicial recomendada por clase:** guerrero/ranger → espada · clérigo → maza · mago/ladrón → daga. En un humano ranger solo se ofreció espada (verificado).

## 4. Conceptos base

- **Mob:** todo ser controlado por el servidor (fidos, guardias, el dios Probador, etc.). Se sube de nivel matándolos.
- **HP / Maná / Mov:** vida, energía mágica para conjuros (ver costo con `hechizos`) y puntos de movimiento. Con Mov en 0 no puedes caminar ni esquivar bien. Montaña cansa más que ciudad; `volar` ahorra movimiento.
- **Recuperarse:** `descansar` (más lento) o `dormir` (más rápido), curandero, o habilidades *rápida curación* (HP) y *meditación* (maná). No estar afectado por `acelerar` al curarse.
- **Prompt:** línea siempre visible con tus valores, ej. `<20/20hp 100/100m 100/100mv 2100xp>`. Personalizable con `prompt` (ver `ayuda prompt`).
- **Tu ficha:** `estado` o `score`. **Tus conjuros/habilidades:** `hechizos` / habilidades según la guía; lo que te afecta y su duración se consulta en la misma ficha.
- **Hitroll:** probabilidad de acertar golpes físicos (se compara contra la armadura/AC del rival). **Damroll:** daño extra por golpe acertado. Mantener ambos lo más alto posible.
- **Alineación:** de angelical (+1000) a satánico (−1000) según a quién mates. Afecta qué equipo puedes usar (flags anti-good/anti-evil → «zap» si no cumples) y hechizos como *rayo de sinceridad/corrupción*. Se detecta con *detectar bondad/maldad* (aura dorada = bueno, roja = malo, sin aura = neutral).
- **Experiencia máxima por mob:** 250 XP. Influye la diferencia de nivel y la alineación (misma moral = menos XP).
- **Guardar el personaje:** un pj nuevo **no se guarda hasta nivel 3** (verificado). Desde ahí se guarda solo; aun así `backup` manual da el mensaje «Perfecto, has hecho un BACKUP de tu ficha» (verificado).
- **Subida de nivel (verificado):** mensaje «¡¡¡ HAS SUBIDO UN NIVEL !!!» + ganancias de HP/maná/mov y **+1 práctica** por nivel. Al subir, el título visible pasa automáticamente al **título de clase** (ej. ranger → «El Acechador»): hay que reaplicar el título personal con `titulo` tras cada subida.
- **Morir:** no pierdes nivel ni equipo; pierdes 2/3 de la XP ganada desde el último nivel. Tu cadáver va a la Cámara de Cadáveres (laberinto bajando desde el curandero); recógelo pronto o se pudre y cualquiera podrá saquearlo. Hasta nivel 5, si abandonaste sin recoger: `equipmin` te da luz, escudo y arma básicos.

## 5. Comandos esenciales

### Exploración y combate
| Comando | Para qué |
|---|---|
| `mirar` | Ver descripción completa de la sala (con `breve` activado ves la corta al moverte) |
| `norte/sur/este/oeste/arriba/abajo` (y diagonales) | Moverse. También rutas rápidas con paths tipo `.2s,3e` desde `recall` (ver §8) |
| `otear` / `otear <dirección>` | Ver mobs cercanos (hasta 3 salas en esa dirección) |
| `considerar <objetivo>` | Medir nivel del mob antes de atacar (tabla abajo) |
| `matar` / `atacar <objetivo>` | Iniciar combate |
| `huir` | Escapar de un combate perdido |
| `coger todo cuerpo` | Saquear un cadáver (oro y equipo) |
| `sacrificar <cuerpo/objeto>` | Ofrecerlo a tu dios por plata; las monedas que da ÷ 3 ≈ nivel del mob/objeto (truco para medir niveles). **Ojo:** es lento; solo compensa si buscas plata, no para farmear XP (verificado: en la Arena los cadáveres traen «Nada.» y el ingreso era por sacrificios de +3 a +12 plata) |
| `recall` | Volver al punto de inicio (Templo de Midgaard) |
| `backup` | Guardado manual de la ficha (desde nivel 3) |
| `abrir puerta` / `abrir <dirección>` | Abrir puertas. Con llave: `desbloquear <puerta/dirección>`. Alternativas: hechizo *Traspasar* (pociones transparentes) o habilidad *forzar* (sin mobs cerca) |

### Tabla de `considerar` (diferencia de nivel del mob vs tú)
| Mensaje | Diferencia |
|---|---|
| Puedes matar a X solo con tu mirada | −10 |
| X no es digno de tu esfuerzo | −9 a −5 |
| X parece un combate fácil | −4 a −2 |
| ¡Un adversario perfecto! | −1 a +1 |
| X dice «¿Te crees con suerte, enano?» | +2 a +4 |
| X te mira y se parte de risa | +5 a +9 |
| Serías un bonito cadáver adornando la calle | +10 o más |

**Regla práctica:** atacar solo lo que salga fácil o perfecto. Nada de +5 o más.

### Ficha, entrenamiento y prácticas
| Comando | Para qué |
|---|---|
| `estado` / `score` | Ver stats, XP, alineación, protecciones |
| `info` | Ver con cuántos puntos de creación se hizo el pj y sus grupos de hechizos |
| `entrenar fue/int/sab/des/con/hp/mana` | Gastar una sesión de entrenamiento en un atributo (mensaje verificado: «Tu constitucion se incrementa!») |
| `practicar <habilidad/arma>` | Perfeccionar una habilidad con el maestro (sube con el uso; espada llega al 95% practicando, verificado) |
| `gain lista` / `gain <grupo o habilidad>` / `gain puntos` | Comprar grupos de hechizos o habilidades en tu cofradía. Precio en entrenamientos (10 prácticas = 1 entrenamiento) |

**Prioridad de entrenamiento (guía, verificada en la práctica):** primero **Constitución** al máximo, luego **Inteligencia**, luego Sabiduría. Motivo: CON alta = más HP por nivel; INT alta = más maná por nivel; SAB 15/18/22/25 = 2/3/4/5 prácticas por nivel. En humano ranger CON siguió subiendo tras nivel 5 (16→17, verificado): no asumas tope sin que el MUD lo rechace.
**Regla sagrada:** los entrenamientos NO se gastan en `gain` de habilidades (te dejan con menos HP para siempre, incorregible). Las habilidades se compran con **prácticas**. `gain puntos` (rebajar XP/nivel) también es mala compra: cobra 2 entrenamientos por cada 100 XP.

**Dónde entrenar/practicar:** en la Escuela del Mud está la **habitación de Entrenamiento de Furey** (el adepto pide decir QUIERO ENTRENAR; el comando `entrenar <stat>` funciona ahí, verificado) y el maestro de prácticas (sacerdote de Circe). La Escuela **no es alcanzable a pie desde la Arena**: toca salir con `recall` a Midgaard y volver a entrar (verificado). Nivel 6+: según la guía, tu cofradía en Midgaard o el marinero en «Un Almacén Abandonado» (norte de Midgaard).

**Lista de prácticas de un ranger con espada (verificada en el maestro):** curar leve 1%, aporreo incesante 1%, bastones 1%, espada 95%, patada 1%, pergaminos 1%, regresar 50%, varitas 1%.

### Economía y tiendas
| Comando | Para qué |
|---|---|
| `lista` | Ver qué vende una tienda y precios |
| `comprar <objeto>` / `comprar <cant>*<objeto>` | Comprar (ej. `comprar 15*pan`) |
| `valorar <objeto>` → `vender <objeto>` | Cotizar y vender lo que no uses |
| Banco: depositar oro | El oro pesa; deposítalo para cargar más cosas. Capacidad de carga = nivel + DES (nº objetos) y FUE (peso). Los contenedores (mochilas, rocas) reducen peso, no cantidad de objetos |

**Compras útiles para novato (tiendas de Midgaard, según la guía):** poción amarilla (ver invisible), poción gris (invisible, evita mobs agresivos débiles), poción transparente (Traspasar puertas sin llave), pergamino de identificar (ver stats de objetos), poción curar ceguera, poción de negación nv10 (quita hechizos). Habilidad *regatear* = descuentos. Ojo: a los tenderos les enfada que un ladrón intente robarles.
**Verificado:** la Tienda de la Escuela (adepto de Fryar) vende «una barra de pan» por **9 plata**.

### Hambre, sed y curación
- Nadie muere de hambre/sed, pero sin comer/beber recuperas HP/maná/mov mucho más lento (el aviso en la ficha es «Estás HAMBRIENTO», verificado).
- Comida: partes de cadáveres de mobs (evitar vísceras/tripas, pueden estar envenenadas) o panadería de Midgaard (`comprar pan` → `comer pan`). **Verificado:** comer la barra de pan de la Escuela responde «Nyam, nyam... Por ahora no tienes mas hambre.»
- Bebida: `beber <recipiente>` («Glup, glup...», verificado) / llenar con `llenar <recipiente> fuente`. Fuente de limonada en la Plaza de los Dioses (5 nortes desde recall): quita hambre y sed.
- **Curandero de Midgaard** (`recall` → norte → `curar` para ver precios): leve 10 oro, serio 15, crítico 25, sanar 50, todo hp 100, mana 10, todo mana 80, refrescar (mov) 5, deslumbrar 20, veneno 25, enfermo 15, maldecir 50. Se sana con `curar <hechizo>`.
- **Escuela (niveles bajos, verificado):** la **adepta de Gominola** en las Jaulas cura al descansar ahí (dejó a un nv5 en HP lleno, 63/63). El curandero a veces cura/protege gratis a niveles ≤10–20 que entran en su sala (no abusar entrando/saliendo).

### Comunicación
| Comando | Para qué |
|---|---|
| `decir <texto>` | Hablar en tu sala (no se puede desactivar) |
| `preguntar <texto>` | Canal de preguntas global. **Hasta nivel 2 es el ÚNICO canal público permitido**; desde nivel 3 se abren todos |
| `contar <nombre> <texto>` / `tell` | Mensaje privado. Responder con `responder <texto>` |
| `exclamar <texto>` | Grito solo en tu área (admite colores) |
| `gritar`, `declamar`, `chillar`, etc. | Canales globales; se activan/desactivan escribiendo el nombre del canal. Ver estado con `canal` |
| `silencio` | Apaga todos los canales públicos (menos `decir`) |
| `afonico` | Bloquea que te lleguen privados |
| `ignorar <nombre>` | Dejar de oír a alguien (no funciona con inmortales) |
| `social` / `<social> [objetivo]` / `gocial` | Sociales/emociones (ej. `reir`, `rofl gandalf`); `gocial` lo ve todo el mundo |
| `emote <texto>` | Emote personalizado en tu sala |

Nada de spam en canales: el abuso se castiga quitando los canales (regla 5) y la comunidad ignora.

### Presentación del personaje
| Comando | Para qué |
|---|---|
| `titulo <texto>` | Cambiar tu título (lo que va tras tu nombre; respuesta verificada: «Título cambiado.»). Colores con `{<código>` … `{x` (ej. `{R` rojo intenso). **Recuerda:** al subir de nivel el MUD lo sustituye solo por el título de clase |
| `descripcion <texto>` / `descripcion + <texto>` / `descripcion -` | Tu descripción al ser mirado (admite colores y ASCII) |
| `prompt <código>` | Personalizar el prompt (`ayuda prompt`) |
| `color` / `breve` | Activar/desactivar color y descripciones breves (menos texto en pantalla) |

### Configuración automática (`auto` para verla)
Se activa/desactiva cada opción escribiendo su nombre (ej. `autosacrificio`). **Verificado en la práctica:** AutoOro viene ACTIVO (recoges monedas solo), AutoRobo y AutoSacrificio pueden venir INACTIVOS según el pj. `nosummon` = inmunidad a que te teletransporten. `noseguir` = rechazar seguidores.

## 6. Ruta de leveleo inicial (Escuela y Arena, verificada)

1. **Naces nivel 1 en la Escuela del Mud.** La Azafata de Petria da la bienvenida en la Entrada (sugiere teclear `DECIR SOY NUEVO`). Lee todos los carteles.
2. Entrena en la **habitación de Entrenamiento de Furey** y practica tu arma con el maestro (sacerdote de Circe). Prioridad: CON → INT → SAB; practica tu arma principal (llega al 95%).
3. **Jaulas:** primeros mobs encerrados; la adepta de Gominola cura en esa zona al descansar.
4. **Arena** (a través de la puerta este de la Escuela; puede hacer falta llave fresca de la gran criatura): farmeo de conejos, caracoles, zorros, lagartos y jabalíes. XP típica verificada por presa según nivel: 50–250 XP, con tope de 250 por mob. El **jabalí da la XP más alta (~190–250) pero pega muy duro**: solo con HP alto. Los cadáveres de la Arena traen «Nada.» de loot: el ingreso ahí es monedas sueltas, no equipo.
5. **El personaje no se guarda hasta nivel 3.** Al llegar, `backup`.
6. Al nivel 2 se desbloquea `quest novato` (tutorial guiado; el Gato aparece al nivel 4 pidiendo comandos `Score`/`raza`). Los quests del **dios Probador** se abren a nivel 5 según la guía (ver §7), aunque el propio juego asigna encargos de dioses al subir (verificado: Cronos encargó su reloj a un nv5 recién subido).
7. Perdido del todo: `recall` y de vuelta a empezar ruta. Dudas: canal `preguntar`.

## 7. Quests y el dios Probador

- **Quest de novato (verificado):** al subir a nivel 2 el dios Probador asigna un encargo de tutorial (ej.: recuperar un objeto robado en la Mazmorra de la Escuela y devolvérselo en Midgaard). La **Mazmorra de la Escuela** tiene mobs agresivos (oso/lobo salen +2 a +4 para un nv3) y el cartel de la Arena advierte que no hay salida fácil: no entrar por debajo del nivel recomendado. El propio dios avisa que si no lo completas, el tutorial continúa al nivel siguiente.
- Los quests «grandes» los da el **dios Probador** desde nivel 5 (según la guía): dan dinero y **cupones** canjeables por equipo del Probador o por **prácticas** (la moneda para `gain` de habilidades).
- Consultar tiempo restante o espera con `prueba tiempo`. **El quest en curso NO se guarda si abandonas**: se pierde y toca esperar para pedir otro.
- Los premios del Probador duran 500 horas reales. Los equipos de quest/legendarios que encuentres tirados: **no tocarlos** si impiden terminar un quest ajeno (regla 15); si recoges uno por error, guarda registro.
- Los dioses también encargan quests sueltos al subir de nivel (verificado: Cronos y su «reloj personalizado» en el Cuartel General, con pasos de llaves de madera/latón). Quedan anotados; perseguirlos o no es decisión estratégica del jugador.

## 8. Áreas por nivel y rutas desde `recall` (web de mapas)

Paths en formato `.direcciones` desde el punto de `recall`. Peligro ☠︎︎ = bajo, más calaveras = más riesgo.

| Niveles | Área | Path desde recall |
|---|---|---|
| Todos | Midgaard (ciudad inicio) | — |
| 1–5 | Escuela del Mud | `.u` |
| 1–5 | Guardería Enana | `.u,e` |
| 1–5 | Yad | `.u,w,d` |
| 1–20 | Llanuras del norte | `.2s,3e,4n,2w,3n` |
| 5–10 | Bosque de Haon Dor | `.2s,5w` |
| 5–10 | Bosque de Miden'nir | `.2s,3e,8s,2w,2s` |
| 5–10 | Cementerio | `.2s,3e,7s,w,s` |
| 5–15 | Moria | `.2s,6e,3n` |
| 5–15 | Fábrica de Mobs | `.2s,3w,3s,e` |
| 5–20 | Aldea gnoma | `.2s,8e,s` |
| 5–20 | Valle de los Elfos | `.2s,3e,4n,2w,3n,2e,n,e,n` |
| 5–20 | Arenas del Desierto | `.2s,5e` |
| 5–20 | Torre Wyvern | `.2s,6e,4s,2e,s,2e,d,e` |
| 5–25 | Ruinas de Thalos | `.2s,6e,4s,3w` |
| 5–30 | Las Alcantarillas | `.4s,d` |
| 8–10 | Academia de Escuderos | `.u,2o` |
| 10–20 | Fortaleza Goblin | `.6s,2e,3s,2w,7s,2e,5s` |
| 10–25 | Reino Enano | `.2s,6e,3n,e` |
| 15–25 | La Capilla | `.2s,3e,7s,w,6s` |
| 25–50 | El Infierno* | `.4s,d,w,d,w,n,3d,s,w,d,w` |

\* **Infierno (desde nv25):** los dos guardianes de la entrada son autoataque, desarman y pegan a quien tenga menos nivel. Truco de la guía: guarda las armas antes de pasarlos y **huye rápido** a las salas siguientes. De las mejores zonas de leveleo 25+.

> La tabla completa (85+ áreas hasta nivel 111) está en https://www.petriamud.com/mapas/ — consultar ahí antes de explorar una zona nueva.

## 9. Clanes y PK (teoría de la guía)

- Un clan te convierte en **PK**: puedes matar jugadores y ellos a ti. Es «otro juego»: competitividad total, habrá quien te campee día y noche.
- La guía **desaconseja clanearse antes de haber jugado hasta nivel 111** con un personaje y conocer el Mud.
- Si te matan en PK, tu cadáver va a la morgue de tu clan.
- **Sin clan está prohibido interferir en peleas PK**: nada de curar combatientes, darles pociones, coger armas caídas o summonear a los contrincantes. Sanción ejemplar.
- Habilidad *ocultarse* al 100% sirve en PK para pasar desapercibido (sin moverte ni actuar); aun así un hechizo de área o *bendita niebla* te revela.

## 10. Reglas del juego (resumen — el desconocimiento no exime)

1. Los dioses ayudan solo cuando lo consideran necesario.
2. **Prohibido multiplaying**: más de un personaje tuyo conectado a la vez (aunque esté AFK) y cualquier ayuda entre tus propios personajes.
3. Bug encontrado = reportarlo a los imps; explotarlo se castiga.
4. Nada de abusar de canales globales (GRITAR, etc.): te quitan los canales, puede ser permanente.
5. Prohibido atacar de cualquier forma a jugadores **no PK**. Tampoco atacar el mob que está matando otro (salvo mismo grupo).
6. Nombres ofensivos/ininteligibles/de sistema: te pueden obligar a cambiarlo.
7. Si entras a un clan, obligación de conocer las Leyes de Clanes.
8. Desobedecer a un Implementador en temas del Mud = borrado del personaje.
9. **Spam prohibido**: repetir comandos sin parar implica revisión de tus acciones. → Jugar a ritmo humano, esperando respuesta entre comandos.
10. Insultar fuera de rol (y en PK: nada homófobo/racista/familiar, ni amenazas fuera del juego ni datos personales) se castiga.
11. Triggers: crearlos responsablemente, que no te metan en líos.
12. No molestar a jugadores sin clan: ni matarles sus mobs, ni instigarlos a clanearse, ni summon sin consentimiento.
13. Objetos legendarios o de quest que bloqueen un quest ajeno: dejarlos donde están.
14. Reportes con log a: nimrod@petriamud.com

---

*Fuentes: guía de principiantes oficial de Petria, web de mapas oficial y web de reglas oficial (consultadas el 2026-10-02), más lo verificado jugando con Elelem (ver `ELELEM.md`).*
