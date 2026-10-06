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

- **Deslumbramiento de mobs (verificado 2026-10-06 en la Aldea gnoma):** el científico puede cegar con un hechizo de deslumbramiento; la ceguera dura más de un minuto y bloquea localizar/atacar mobs («no está por aquí»). Mitigación: dejar al cegador para el final del circuito o curarse con `conjurar curar deslumbrar` (cura propia verificada: restaura la vista).

## 4. Conceptos base

- **Mob:** todo ser controlado por el servidor (fidos, guardias, el dios Probador, etc.). Se sube de nivel matándolos.
- **HP / Maná / Mov:** vida, energía mágica para conjuros (ver costo con `hechizos`) y puntos de movimiento. Con Mov en 0 no puedes caminar ni esquivar bien. Montaña cansa más que ciudad; `volar` ahorra movimiento.
- **Recuperarse:** `descansar` (más lento) o `dormir` (más rápido), curandero, o habilidades *rápida curación* (HP) y *meditación* (maná). No estar afectado por `acelerar` al curarse.
- **Prompt:** línea siempre visible con tus valores, ej. `<20/20hp 100/100m 100/100mv 2100xp>`. Personalizable con `prompt` (ver `ayuda prompt`).
- **Tu ficha:** `estado` o `score`. **Tus conjuros/habilidades:** `hechizos` / habilidades según la guía; lo que te afecta y su duración se consulta en la misma ficha.
- **Hitroll:** probabilidad de acertar golpes físicos (se compara contra la armadura/AC del rival). **Damroll:** daño extra por golpe acertado. Mantener ambos lo más alto posible.
- **Alineación:** de angelical (+1000) a satánico (−1000) según a quién mates. Afecta qué equipo puedes usar (flags anti-good/anti-evil → «zap» si no cumples) y hechizos como *rayo de sinceridad/corrupción*. Se detecta con *detectar bondad/maldad* (aura dorada = bueno, roja = malo, sin aura = neutral).
- **Experiencia máxima por mob:** 250 XP. Influye la diferencia de nivel y la alineación (misma moral = menos XP).
- **Decaimiento de XP por nivel:** el mismo mob paga cada vez menos conforme subes (científico Gnomo verificado: 87 XP a nivel 9 → 42–67 a nivel 11 → 13–19 a nivel 12). Cada zona rinde unos 2–3 niveles y luego toca cambiar, aunque siga siendo «segura».

- **Repoblación de zonas:** una zona NO repuebla mientras haya un jugador dentro, aunque esperes (verificado: 20 min dentro de la Aldea sin una reaparición). Al salir y dejarla vacía ~15 min, la ronda completa reaparece (verificado en la Aldea Gnoma). Patrón correcto: farmear la ronda, salir a otra zona/ciudad un cuarto de hora y volver.- **Guardar el personaje:** un pj nuevo **no se guarda hasta nivel 3** (verificado). Desde ahí se guarda solo; aun así `backup` manual da el mensaje «Perfecto, has hecho un BACKUP de tu ficha» (verificado).
- **Subida de nivel (verificado):** mensaje «¡¡¡ HAS SUBIDO UN NIVEL !!!» + ganancias de HP/maná/mov y **prácticas** (verificado: 2 al pasar a 12 y 3 al pasar a 13; varía con los atributos). En algunos niveles se desbloquean conjuros nuevos para practicar (verificado en ranger a nivel 13: *piel de corteza* y *espíritu animal*). Al subir, el título visible pasa automáticamente al **título de clase** (ej. ranger → «El Acechador»): hay que reaplicar el título personal con `titulo` tras cada subida.
- **Morir:** no pierdes nivel; pierdes 2/3 de la XP ganada desde el último nivel. Tu equipo queda en el cadáver, que va a la Cámara de Cadáveres (laberinto bajando desde el curandero); **si no lo recoges pronto, lo pierdes**: el cadáver puede desaparecer rápido (verificado dos veces: al llegar ya no estaba). Hasta nivel 5 según la guía, si abandonaste sin recoger: `equipmin` te da luz, escudo y arma básicos — **verificado: sigue funcionando en niveles 6–10, pero a nivel 12 ya no equipa nada**.

## 5. Comandos esenciales

### Exploración y combate
| Comando | Para qué |
|---|---|
| `mirar` | Ver descripción completa de la sala (con `breve` activado ves la corta al moverte) |
| `norte/sur/este/oeste/arriba/abajo` (y diagonales) | Moverse. También rutas rápidas con paths tipo `.2s,3e` desde `recall` (ver §8) |
| `otear` / `otear <dirección>` | Ver mobs cercanos (hasta 3 salas en esa dirección) |
| `considerar <objetivo>` | Medir nivel del mob antes de atacar (tabla abajo) |
| `matar` / `atacar <objetivo>` | Iniciar combate |
| `huir` | Escapar de un combate perdido. **Cuesta XP** (verificado: 10 XP a nivel bajo y 25 XP a nivel 13 con `recall` en combate): úsalo para vivir, no como rutina |
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

- **«No es digno de tu esfuerzo» aún da XP:** un mob muy por debajo de tu nivel rinde poco, pero no cero (verificado a nivel 12: 17–19 XP). Sirven como relleno cuando no hay nada mejor; no los descartes por el aviso.

- **Resolución de nombres genéricos:** `matar <nombre>` puede enganchar al mob peligroso de nombre parecido que haya cerca, no al débil que querías (verificado: `matar goblin` en la Fortaleza resolvió al teniente goblin y entraron dos enemigos). Con `considerar` y nombres completos siempre que se pueda.

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

## 11. Mapas verificados (salas, conexiones y mobs)

Solo el área: salas, conexiones, mobs y peligros propios de cada zona. Verificado en juego (2026-10-02 → 2026-10-04). Los números `#xxxx` son la sala cuando se conoce.

## Midgaard (ciudad base)

- **Templo de Mota #3001** — punto de llegada del `recall`. Seguro.
  - Altar del Templo #3054: curandero. Debajo: **Salón de Cadáveres** (aquí aparecen los cadáveres al morir).
- #3001 → **S** → Plaza del Templo → **S** → **Plaza del Mercado**.
  - Plaza del Mercado → **O** → Calle Mayor (oeste) → **N** → La Panadería #3009 (panadero, protegido).
  - Plaza del Mercado → **E** → Calle Mayor → **E** → Calle Mayor (Tienda General) → **E** → Interior del Portón Este → **E** → Exterior del Portón Este → **E** → Una Entrada a la Ciudad → **E** → Un Cruce de Carreteras → **E** → La Carretera del Este → **E** → Por la Carretera del Este → **E** → Un Puesto de Guardia (tuareg).
- La Armería #3011 (cierra de noche).
- **Plaza del Rastrillo** (al O del Vertedero): fuente de agua.
- **La Sala de entrenamientos de los Rangers #3396**: Elladam, entrenador de Rangers.
- El Vertedero: vacío en dos visitas (2026-10-03/04).

## Aldea gnoma (farmeo niveles 9-11)

Entrada: desde Un Puesto de Guardia → **S** → La Entrada a la Aldea Gnoma **#1501** → **E** → Un Polvoriento Sendero **#1502** → **E** → Un Camino en la Aldea **#1503** → **N** → Un Camino en la Aldea **#1505** (hombre Gnomo); **#1503** → **E** → Un Sendero **#1504** → **S** → Casa **#1513** (científico); **#1505** → **S** → Un Camino en la Aldea **#1507** → **O** → Una Tienda Gnoma (científico) → **S** → #1508 → **O** → Una Tienda Gnoma (científico). (`areas2`: `3s8es` desde el Templo.)

- La Casa **oeste de #1505** guarda **2 hombres juntos: no entrar** (grupo).
- El científico puede cegar (deslumbrar). XP a nivel 10–11: científico 29–67, hombre 20–49; a niveles 9–10 el científico daba 82–102.
- **Una Pequeña Cabaña #1519** — **guardia Gnomo solo**: 60–110 XP a nivel 9; **17–18 XP a nivel 13**.
- **El Sendero en Desuso** — linda con «La Entrada a las Minas» y «El Claro» (sin explorar).
- **Fortaleza** — 2 guardias juntos: peligro, no entrar en pelea ahí.
- **Jefe Gnomo** — intocable, no atacable.
- Portón de Vapor (este): bloqueado, «Solo se permite el ingreso a gnomos».
- Protegidos (no atacables): mujer, niño, archivista, alquimista, tabernero Gnomo.

## Cementerio (agotado al nivel 9: 19 XP/mob)

Ruta: recall → #3001 → `.2s,3e,7s,w,s` → entrada **#3600** (segura).

- **Capilla #3405** (Santuario): segura.
- Mobs: esqueleto polvoriento, zombie putrefacto, ghoul pálido (tumba #3617); de noche, «ojos diabólicos».
- **Peligro:** #3601 con dos esqueletos; también aparecen pares en #3640.
- Propiedad de la zona: `recall`/`regresar` no funcionan dentro; la salida es a pie.

## Guardería Enana (agotada al nivel 7)

- **Recepción #6601** — segura. Propiedad de la zona: `recall` no funciona dentro.
- #6601 → **S** → #6602 → **O** → #6603 (niñera + osito + enano) → **S** → #6605 → **E** → #6604.
- **#6610 Patio de Juegos: no entrar.**
- Mobs: soldado de juguete, enano joven, muñeca, osito de peluche.
- **La vieja niñera** asiste en las peleas de su sala: no pelear con ella presente. El feo oso de peluche vaga entre salas.

## Zonas peligrosas o descartadas (verificado)

- **Miden'nir** — goblin/teniente: aggro, desarma y derriba; mató a Elelem (nivel ~12+).
- **Fábrica de Mobs** — viscosidad tóxica: muerte por desgaste con equipo bajo.
- **Gigante Entrenador** — mata al entrar.
- **Escuela** — inaccesible desde el reload de Sammer (antes: Jaulas, adepta de Gominola).
- **Haon Dor** — conejos en pareja (24 XP); **alcantarillas** — gran rata; **El Vertedero** — vacío.

## Las Minas (junto a la Aldea gnoma) — medidas 2026-10-05

- Entrada por el Sendero en Desuso → «La Entrada a las Minas» → «Un Pozo Minero». Salas iluminadas.
- Mob medido: minero Hobgoblin single = **5 XP a nivel 12** — inviable. Cerca quedan «Barracas» y «Armería» hobgoblin (sin medir).
- «La Armería Hobgoblin»: vacía de mobs (solo armas tiradas). «Las Barracas de los Hobgoblins»: DOS soldados Hobgoblin juntos — grupo, no medibles como singles.

## Llanuras del Norte (probada 2026-10-06, nivel 13)

- Ruta desde `recall`: `.2s,3e,4n,2w,3n`. Camino, colina y praderas de entrada **sin mobs**; fauna suelta escasa (loba sola en el sendero).
- **La loba paga 0 XP a nivel 13**: la entrada de la zona no compensa para levear a este nivel.
- Al norte del sendero hay un mirador que bordea la entrada del **Valle de los Elfos** (otra zona).

## Valle de los Elfos (probada 2026-10-06, nivel 13)

- Ruta desde `recall`: `.2s,3e,4n,2w,3n,2e,n,e,n` y luego abajo; comparte el arranque con las Llanuras del Norte.
- Mobs medidos a nivel 13: elfo = **6 XP**, chucho (perro) = **0 XP**; `considerar` los marca «no es digno de tu esfuerzo». No compensa a nivel 13.

## Fortaleza Goblin (descartada 2026-10-06, nivel 13)

- Ruta desde `recall`: `.6s,2e,3s,2w,7s,2e,5s`. A la entrada hay **dos tenientes goblin juntos** (grupo).
- En el túnel, un «goblin» solitario engaña: `matar goblin` resolvió al **teniente** y entraron dos enemigos, con intentos de desarme y zancadilla y daño sostenido. Teniente = **+20 XP a nivel 13**, pero la zona no permite singles seguros: **descartada para farmear**.

## Bosque Sagrado (entrada no localizada, 2026-10-06)

- `areas2` lo lista 5–20 con ruta `3s8en`, pero no se encontró entrada practicable: el callejón es sin salida (muro cerrado) y el Santuario del Portal Druídico denegó la entrada. Pendiente de otra vía.

## Aldea Abandonada (entrada no localizada, 2026-10-06)

- `areas2` la lista 10–20 con ruta «3s, 13o, so» desde el templo. Siguiéndola se sale por el Portón Oeste al Linde del Bosque y a senderos del Bosque Iluminado/Denso, donde el suroeste no es salida válida: no se localizó la entrada ni mobs suyos en este tanteo.

## Torre Wyvern (exterior probado 2026-10-06, nivel 13)

- Ruta desde `recall`: `.2s,6e,4s,2e,s,2e,d,e` más avance extra. Caminos exteriores con tramperos, cazadores, guardabosques y centauros (también en pareja: no atacar grupos).
- Centauro single medido: **+14 XP a nivel 13** (como la Aldea Gnoma).
- Las **torres gemelas** están rodeadas por un foso que exige un **bote**. El barril del viejo almacén no sirve como bote. La tienda de los alrededores no responde como tienda (`lista` rechazado y las compras no descuentan plata): origen del bote sin resolver.

## Reino Enano (tránsito probado 2026-10-06)

- Tránsito por el Bosque Oscuro de los Enanos (valle → sendero oscuro → curva) hacia un arroyo y un bosque élfico, sin ningún enano single medible en el recorrido. La entrada con enanos queda sin localizar.
- Casa #1513: el científico es baja válida cuando está **solo** en la casa (sin la mujer ni el niño); si ellos están dentro, no se ataca. Con Tienda #1514 y Cabaña #1519, la ronda completa rinde ~42 XP a nivel 13.
