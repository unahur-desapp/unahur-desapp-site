## Qué contiene
1. Catálogo de funcionalidades (43 items) organizado por los mismos ejes del enunciado (A: cuadros, B: reglas, C: ranking, D: identidades, G: gobernanza, X: transversales). Cada una con ID, prioridad P0/P1/P2, cita textual del enunciado que la origina y criterios de aceptación observables.

2. Mapa de páginas (25 pantallas) en tres zonas: pública (8), jugador (7), admin (10).

3. Esquema de API bajo /api/v1, agrupado en 9 recursos, con convenciones transversales (errores, paginación, concurrencia optimista, idempotencia).

4. Matriz de trazabilidad funcionalidad → página → endpoint, para verificar que no queda nada del enunciado sin soporte.

## Decisiones de diseño que quiero destacar
Competidor como abstracción central. El motor de cuadros trabaja con Competidores (un Jugador en singles, un Equipo en dobles), nunca con Jugadores directamente. Es lo que hace que el bracket sea uno solo para todas las modalidades, y es justamente la relación que el enunciado pide defender en la entrega #1.

Un único endpoint de transiciones de torneo (POST /tournaments/:id/transitions) en vez de /open, /close, /start… Concentra la máquina de estados en un punto, hace trivial auditarla y evita que el frontend invente caminos. Respuesta directa al criterio de evaluación #2.

No existe PUT /matches/:id/result. La ausencia del verbo de edición es lo que materializa en la API la inmutabilidad exigida. Corregir un error va por POST /matches/:id/rectifications, auditado.

El ganador nunca lo manda el cliente: lo deriva el backend del score. Y hay un endpoint dry-run (/result/validate) para que la UI valide en vivo sin duplicar las reglas de tenis en el frontend.

Concurrencia (§3.1): el cierre de torneo no recalcula en línea, encola un job; orden total (fechaFin, categoría, id), lock por modalidad, atribución idempotente por (tournamentId, playerId). El ranking es una proyección reconstruible desde cero → verificable por test.

Mobile: se descarta el árbol. Un bracket de 32 no entra en un viewport móvil, así que abajo de 768px va selector de ronda + lista vertical de cards. Por eso agregué GET /draw/rounds/:round.

## Dos cosas que conviene resolver antes de seguir
S-7 (riesgo alto): "el tenis se juega solo, en parejas o en equipos mixtos" admite dos lecturas. Asumí dobles mixtos (pareja hombre+mujer), que es lo que el enunciado describe literalmente después. Si en realidad piden competencia por equipos tipo Copa Davis, cambia la abstracción de Competidor y con ella el ERD. Vale despejarlo con la cátedra.

El criterio #1 dice explícitamente que la primera entrega es modelado, no código. Lo dejé anotado en el §0: este documento es insumo para el ERD, y conviene validar el modelo antes de escribir nada en /backend y /frontend (hoy vacíos).

Marqué como supuestos explícitos los criterios de puntaje para retired y walkover (S-2, S-3) porque el enunciado los plantea como pregunta abierta — son decisión del equipo y hay que poder defenderlas.

Si querés, el próximo paso natural es el ERD + modelo de objetos, o publicar esto como página compartible para el resto del equipo.