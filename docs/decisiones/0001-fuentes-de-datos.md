# 0001. Fuentes de datos de skins y precios

- **Fecha:** 2026-10-06
- **Estado:** aceptada

## Contexto
La web necesita el catálogo de skins de CS2 (nombre, imagen y rareza), su precio actual y si sube o baja.

## Decisión
- Catálogo: CSGO-API de ByMykel (`skins_not_grouped.json`).
- Precio actual: Skinport `/v1/items` (`app_id=730`, `currency=EUR`).
- Tendencia: Skinport `/v1/sales/history` (`app_id=730`, `currency=EUR`).
- Las tres fuentes se unen por `market_hash_name`.
- Las peticiones a Skinport llevan la cabecera `Accept-Encoding: br`.

## Alternativas consideradas
_Sin documentar todavía._

## Consecuencias
- El backend tiene que saber descomprimir respuestas Brotli (`br`) de Skinport. _Pendiente_ elegir cómo hacerlo en Java (ver [dudas](../dudas.md)).
- Ninguna de estas fuentes da el pico máximo histórico directamente; habrá que construirlo guardando precios en nuestra base de datos.
- El float y el estado de cada skin no vienen en estas fuentes.
