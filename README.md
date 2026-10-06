# CS_MARKET

Proyecto de Fin de Grado de 2º de DAW.

CS_MARKET es una aplicación web para consultar el mercado de skins de Counter-Strike 2:

- **Precio en tiempo real** de cada skin, obtenido de APIs públicas de mercado.
- **Pico máximo de precio** que ha alcanzado cada skin en venta.
- **Tendencia**: si el precio sube o baja.
- **Botón "Inspeccionar"**: conectando con la cuenta de juego, mostrar las skins con su float y su estado (desgaste).

## Documentación

| Archivo | Contenido |
|---|---|
| [docs/arquitectura.md](docs/arquitectura.md) | Piezas del sistema, fuentes de datos y cómo se unen |
| [docs/decisiones/](docs/decisiones/) | Una ficha por cada decisión importante, con el porqué |
| [docs/ideas.md](docs/ideas.md) | Ideas nuevas para implementar |
| [docs/dudas.md](docs/dudas.md) | Preguntas abiertas sobre cómo implementar cada cosa |
| [CHANGELOG.md](CHANGELOG.md) | Cambios importantes, fechados |

## Tecnologías

- Backend: Java con servlets (Java EE 8, `javax.servlet`, sobre Tomcat 9) y JDBC. Ver [decisión 0002](docs/decisiones/0002-backend-servlets.md).
- Frontend: HTML, CSS y JavaScript.
- Base de datos: _pendiente de decidir_.

## Instalación

_Pendiente._ Se completará cuando exista el primer código ejecutable (versión de Java, Tomcat, base de datos y cómo configurarla).

## Ejecución

_Pendiente._
