Documento creado en doc/analisis-inicial.md. 

Resumen:
- 8 funcionalidades (F1–F8), cada una vinculada a citas literales del enunciado: ciclo de vida de torneos, motor de cuadros, máquina de estados de partido, ranking tipo ATP (con concurrencia), identidades/modalidades/elegibilidad, inscripciones, gobernanza y estadísticas históricas.
- Mapa de páginas en 3 niveles: públicas (/, /torneos/:id/cuadro, /ranking…), área de jugador (/panel/inscripciones, /panel/carrera…) y administración (/admin/torneos/:id/cuadro, /admin/ranking…).
- Esquema de endpoints REST (~30 rutas bajo /api/v1) organizados por recurso (auth/users, teams, tournaments/enrollments, bracket/matches, categories/ranking), con acceso admin vs jugador y acciones de dominio tipo POST /tournaments/:id/bracket.
  
Incluí una sección de próximos pasos alineada a los criterios de evaluación (DER/Modelo de objetos, state machine, pseudocódigo de ranking, informe de IA). ¿Querés que avance con el modelo de datos (ERD/MER) o directamente con el esqueleto del backend?