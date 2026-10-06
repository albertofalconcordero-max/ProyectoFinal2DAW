# Dudas abiertas

Preguntas sobre cómo implementar cada cosa. Cuando una se resuelve, se apunta la respuesta y, si es importante, se crea una decisión en `decisiones/`.

## Abiertas

### ¿Cómo obtener el pico máximo histórico de cada skin?
Skinport da el precio actual y un resumen de ventas recientes, no el máximo de toda la historia. Opción que se baraja: guardar el precio en cada consulta de la tarea programada y calcular el máximo sobre nuestra base de datos. Así el pico cuenta solo desde que empezamos a guardar. ¿Hay alguna fuente con histórico más largo?

### ¿Cómo obtener el float y el estado de cada skin?
El float no aparece en el catálogo ni en Skinport. Hay que investigar cómo se lee a partir del enlace de inspección de cada objeto y qué servicio o API lo permite.

### ¿Cómo conectar la web con la cuenta de juego?
Qué método de inicio de sesión usar para leer el inventario del usuario y qué permisos hacen falta.

### ¿Cómo descomprimir Brotli (`Accept-Encoding: br`) en Java?
Java no trae Brotli de serie. Hay que elegir librería.

### ¿Cada cuánto consultar Skinport?
Depende de los límites de peticiones de su API y de lo "en tiempo real" que queramos que sea.

### ¿Qué base de datos usar?
Motor y diseño de tablas para catálogo e histórico de precios.

### ¿Gson o Jackson para el JSON?

## Resueltas

| Duda | Respuesta | Fecha |
|---|---|---|
| ¿Servlets o Spring Boot? | Servlets. Ver decisión 0002 | 2026-10-06 |
