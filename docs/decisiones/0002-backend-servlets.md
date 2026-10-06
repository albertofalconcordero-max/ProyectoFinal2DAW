# 0002. Backend con servlets (Java EE 8, `javax.servlet`, sobre Tomcat 9)

- **Fecha:** 2026-10-06
- **Estado:** aceptada

## Contexto
En el curso actual solo se han dado servlets. Spring Boot se vio por encima el año pasado en las prácticas, pero aún no se ha dado en clase.

## Decisión
- Backend en Java con **servlets** (Java EE 8, paquete `javax.servlet`) desplegados en **Tomcat 9** (9.0.53, el que usa el proyecto de NetBeans).
- Acceso a base de datos con **JDBC**.
- Una **tarea programada** que consulta Skinport periódicamente y guarda el histórico de precios.
- Frontend en **HTML, CSS y JavaScript**.

## Alternativas consideradas
- **Spring Boot:** menos código (`@RestController`, `@Scheduled`, JPA), pero no se ha dado todavía en clase.

## Consecuencias
- Cada endpoint es una clase que extiende `HttpServlet`.
- La conversión a JSON se hace con una librería (Gson o Jackson, _pendiente_ elegir).
- La tarea programada se puede montar con un `ScheduledExecutorService` arrancado desde un `ServletContextListener`.
- Más código a mano, pero demuestra cómo funciona todo por debajo.
- **Posible migración futura a Spring Boot** si se da durante este curso.
