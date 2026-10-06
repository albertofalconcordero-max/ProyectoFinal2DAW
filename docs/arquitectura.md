# Arquitectura

> Documento vivo. Lo marcado como _pendiente_ aún no está decidido.

## Visión general

```
Navegador (HTML/CSS/JS)
        │  peticiones HTTP, respuestas JSON
        ▼
Servlets en Tomcat ──JDBC──► Base de datos (histórico de precios)
        ▲
        │  tarea programada cada X minutos
APIs externas (CSGO-API, Skinport)
```

1. Una **tarea programada** dentro del backend consulta Skinport cada cierto tiempo y guarda cada precio en la base de datos. Así se va construyendo el histórico propio, del que salen el pico máximo y la tendencia.
2. Los **servlets** exponen endpoints que devuelven JSON al frontend.
3. El **frontend** muestra el catálogo, los precios, el pico máximo y el botón "Inspeccionar".

## Fuentes de datos

| Para qué | URL | Notas |
|---|---|---|
| Catálogo de skins (nombre, imagen, rareza) | `https://raw.githubusercontent.com/ByMykel/CSGO-API/main/public/api/en/skins_not_grouped.json` | JSON estático en GitHub |
| Precio actual | `https://api.skinport.com/v1/items?app_id=730&currency=EUR` | Requiere cabecera `Accept-Encoding: br` |
| Si sube o baja | `https://api.skinport.com/v1/sales/history?app_id=730&currency=EUR` | Requiere cabecera `Accept-Encoding: br` |

Las tres se unen por el campo **`market_hash_name`**.

`app_id=730` es el identificador de CS2 en Steam y `currency=EUR` fija la moneda en euros.

Ver [decisión 0001](decisiones/0001-fuentes-de-datos.md).

## Estructura del proyecto

Proyecto web de NetBeans. Los paquetes Java van directamente bajo `src/java`. Los nombres de clase son orientativos.

```
src/java/
├── controlador/   servlets: reciben la petición y devuelven JSON
│   ├── SkinServlet.java            buscador y ficha de una skin
│   ├── LoginSteamServlet.java      redirige a Steam
│   ├── RetornoSteamServlet.java    recibe la respuesta de Steam
│   └── InventarioServlet.java      "Mi inventario" con precios
├── servicio/      lógica y llamadas a las APIs externas
│   ├── ServicioCatalogo.java       CSGO-API
│   ├── ServicioSkinport.java       precios e historial de ventas
│   ├── ServicioSteam.java          login e inventario
│   └── ActualizadorPrecios.java    la tarea que guarda precios cada X min
├── dao/           acceso a la base de datos con JDBC
│   ├── Conexion.java
│   ├── SkinDAO.java
│   ├── PrecioDAO.java
│   └── UsuarioDAO.java
├── modelo/        clases de datos: Skin, Precio, Usuario
├── listener/      ArranqueListener: arranca la tarea al iniciar Tomcat
├── filtro/        LoginFiltro: protege lo que exige login (más adelante)
└── util/          ayudas comunes, como descomprimir Brotli o el JSON

web/               todo lo que descarga el navegador
├── index.html
├── css/
├── js/
├── img/
└── WEB-INF/web.xml   no accesible desde el navegador
```

Recorrido de una petición: `web/js` → `controlador` → `servicio` → `dao` → base de datos. Las clases de `modelo` son los objetos que viajan entre capas.

Las llamadas a las APIs externas (Skinport, CSGO-API, Steam) se hacen siempre desde Java, en `servicio`, nunca desde el JavaScript del navegador: la tarea programada tiene que guardar precios aunque nadie tenga la web abierta, el listado de Skinport es muy grande, Skinport limita el número de peticiones y el login con Steam hay que verificarlo en el servidor.

## Componentes

### Catálogo
Carga el JSON de CSGO-API y lo cruza con los precios por `market_hash_name`.

### Precios e histórico
- Precio actual: endpoint `/v1/items` de Skinport.
- Tendencia: endpoint `/v1/sales/history` de Skinport.
- Pico máximo: _pendiente_ (ver [dudas](dudas.md)).
- Frecuencia de la tarea programada: _pendiente_.

### Inspeccionar (float y estado)
Conexión con la cuenta de juego para leer el inventario y obtener el float de cada skin. _Pendiente de investigar_ (ver [dudas](dudas.md)).

### Base de datos
Motor y modelo de tablas: _pendientes_.
