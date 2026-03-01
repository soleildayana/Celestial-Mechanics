# Copilot Instructions for Celestial-Mechanics

## Contexto del proyecto
- Este repositorio es **notebook-first**: el trabajo principal está en `Movimientos_Sol_Tierra_Luna.ipynb` y `n_bodies_num.ipynb`.
- El objetivo es calcular/visualizar dinámica gravitacional (2 y N cuerpos) usando efemérides de JPL Horizons vía `pymcel`.
- No hay paquetes Python modulares ni suite de tests; prioriza cambios pequeños y verificables por celda.
- Temas centrales del contenido: **Astronomía** y **Física**.

## Arquitectura y flujo de datos
- Patrón central: `tabla, jd, X = pc.consulta_horizons(id=..., location='@SSB', epochs=...)`.
- `X` se interpreta como estado cartesiano: `X[0:3]` posición, `X[3:6]` velocidad.
- Las fuerzas/aceleraciones se calculan con vectores relativos (`r2 - r1`) y norma `np.linalg.norm(...)`.
- Constantes físicas provienen de `pc.constantes` (por ejemplo `G`, `M_sun`, `M_earth`, `mu_sun`).

## Convenciones específicas del código
- Declara variables de forma explícita; si son análogas, agrúpalas en una misma línea (ejemplo: `a, b, c = 1, 2, 3`).
- Unidades usadas en notebooks: posiciones en `km`, velocidades en `km/s`; mantén coherencia en todas las celdas nuevas.
- IDs NAIF ya usados en el repo: Sol `10`, Tierra `399`, Luna `301`, Júpiter `599`.
- Se trabaja respecto al baricentro del sistema solar (`location='@SSB'`) salvo que el notebook indique explícitamente otra cosa.
- Si agregas funciones, sigue el estilo ya usado (`fuerza_gravitacional`, `aceleraciones_n_cuerpos`): firma simple y `numpy` vectorial.

## Estilo de explicación y presentación
- Prioriza explicaciones teóricas rigurosas: explica el **por qué** de cada paso además del **qué**.
- Mantén redacción clara y concisa; evita relleno y repeticiones.
- Organiza el contenido en secciones y subsecciones con títulos descriptivos.
- Mantén higiene del código y uso eficiente del espacio (sin bloques redundantes).

## Visualización
- Usa `plotly` para visualizaciones interactivas siempre que sea viable.
- Para gráficas de astronomía/física, prefiere fondos oscuros y estética tipo espacial.
- Conserva ejes y unidades físicas explícitas en títulos/etiquetas (por ejemplo `X (km)`, `km/s^2`).

## Flujo recomendado para agentes
- Al editar notebooks, **no** reescribas celdas completas si no es necesario; modifica solo la celda objetivo.
- Ejecuta celdas en orden top-down cuando un cambio afecte variables compartidas (`r_S`, `r_T`, `mu`, etc.).
- Si una celda instala paquetes con `!pip install`, considera reiniciar kernel antes de validar imports.
- Mantén los resultados reproducibles: evita fechas dinámicas (`datetime.now()`) cuando el análisis requiera comparación estable.

## Dependencias e integración
- Dependencias declaradas en `req.txt`: `plotly`, `numpy`, `pandas`, `matplotlib.pyplot`, `spiceypy`.
- Dependencias usadas en notebooks: `pymcel`, `numpy`, `matplotlib`, `spiceypy`, `plotly`.
- `pymcel` integra consultas a Horizons; cualquier refactor debe preservar ese punto de integración.

## Qué evitar en este repo
- No introducir estructura de app (APIs, carpetas backend/frontend) sin petición explícita: el proyecto es académico y exploratorio.
- No cambiar convenciones físicas/unidades de forma silenciosa.
- No eliminar narrativa Markdown de los notebooks: documenta el razonamiento físico junto con el código.

## Ejemplos de referencia en este repositorio
- Fuerza de 2 cuerpos y vector relativo: `Movimientos_Sol_Tierra_Luna.ipynb`.
- Generalización a N cuerpos (`aceleraciones_n_cuerpos`): `Movimientos_Sol_Tierra_Luna.ipynb`.
- Consulta de estados para Sol/Júpiter y extrapolación básica: `n_bodies_num.ipynb`.

