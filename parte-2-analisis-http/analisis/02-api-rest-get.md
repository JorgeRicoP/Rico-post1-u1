# Análisis 2: Petición GET a API REST Pública con DevTools

## Información general
Request URL - https://jsonplaceholder.typicode.com/favicon.ico
Request Method - GET
Status Code - 200 OK (from disk cache)
Remote Address - 104.21.59.19:443
Referrer Policy - strict-origin-when-cross-origin

## Response headers
access-control-allow-credentials - true
age - 5519
alt-svc - h3=":443"; ma=86400
cache-control - public, max-age=43200
cf-cache-status - HIT
cf-ray - a2cdb1511fb39be2-MIA
content-encoding - zstd
content-type - image/x-icon
date - Tue, 18 Aug 2026 03:04:42 GMT
etag - W/"13e-19cf3f0c300"
last-modified - Sun, 15 Mar 2026 23:59:28 GMT
nel - {"report_to":"heroku-nel","response_headers":["Via"],"max_age":3600,"success_fraction":0.01,"failure_fraction":0.1}
report-to - {"group":"heroku-nel","endpoints":[{"url":"https://nel.heroku.com/reports?s=T1Z%2FcWIPLawjp2b3oq5%2B8Ts2sn%2BoBzo6yhS1XAfub5E%3D\u0026sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d\u0026ts=1781864829"}],"max_age":3600}

reporting-endpoints - heroku-nel="https://nel.heroku.com/reports?s=T1Z%2FcWIPLawjp2b3oq5%2B8Ts2sn%2BoBzo6yhS1XAfub5E%3D&sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d&ts=1781864829"
server - cloudflare
vary - Origin, Accept-Encoding
via - 2.0 heroku-router
x-powered-by - Express
x-ratelimit-limit - 1000
x-ratelimit-remaining - 999
x-ratelimit-reset - 1781864833

## Request Headers
referer - https://jsonplaceholder.typicode.com/posts/1
sec-ch-ua - "Not=A?Brand";v="99", "Google Chrome";v="151", "Chromium";v="151"
sec-ch-ua-mobile - ?0
sec-ch-ua-platform - "Windows"
user-agent - Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36

## Tiempos de carga
Queued at 137.62 ms
Started at 163.71 ms
Resource Scheduling - Queueing duration 26.09 ms
Connection Start - Stalled duration 1.11 ms
Request Sent duration 0 
Waiting for server response duration 0.17 ms
Content Download duration 3.41 ms
total 30.78 ms

## Conclusion
Esta petición GET al favicon de jsonplaceholder.typicode.com devolvió un 200 OK "from disk cache", lo que significa que el navegador ni siquiera consultó al servidor: usó directamente la copia local guardada gracias al header cache-control: public, max-age=43200 (válido por 12 horas). El backend corre sobre Heroku (via: 2.0 heroku-router, x-powered-by: Express) mientras que Cloudflare actúa como CDN/proxy frente a él, y también se ve un cf-cache-status: HIT, indicando doble capa de cacheo (CDN + navegador). Se observa además un sistema de rate limiting activo (x-ratelimit-limit: 1000, remaining: 999) y de reporte de errores de red (NEL) apuntando a Heroku, típico de APIs que monitorean su disponibilidad. El tiempo total fue de solo 30.78 ms, y al venir del caché de disco, prácticamente todo el tiempo se fue en la cola de programación del recurso (26.09 ms) y no en red real. En conjunto, refleja una API pública con buenas prácticas de cacheo, límites de uso controlados y observabilidad activa.

## HTTP vs API REST
Aunque ambas peticiones usan el mismo protocolo (HTTPS) y comparten Cloudflare como capa de CDN, cumplen propósitos distintos: la primera solicita un documento HTML (navegación de página completa, sec-fetch-dest: document), mientras que la segunda solicita un recurso estático binario (un ícono) consumido dentro del contexto de una API REST. La petición a la API expone headers característicos de servicios backend —como x-ratelimit-*, x-powered-by: Express y nel/report-to para monitoreo— que no aparecen en la petición HTML tradicional, evidenciando una arquitectura orientada a servicios con control de consumo y trazabilidad. En cuanto a caché, la petición HTML usó revalidación condicional (304 Not Modified, vía if-modified-since), mientras que la de la API evitó incluso esa validación al servir directamente desde el caché de disco del navegador (200 "from disk cache"), lo cual la hizo aún más rápida (30.78 ms vs 120.46 ms). Por último, la petición HTML incluye headers de navegación de usuario (sec-fetch-user, sec-fetch-mode: navigate) ausentes en la de la API, ya que esta última fue disparada por el propio navegador al renderizar un recurso embebido, no por una acción directa del usuario.

# Análisis: Peticion GET a recurso inexistente

## Informacion general
Request URL
https://jsonplaceholder.typicode.com/posts/999
Request Method
GET
Status Code
404 Not Found
Remote Address
104.21.59.19:443
Referrer Policy
strict-origin-when-cross-origin

## Response headers
access-control-allow-credentials    true
age     17109
alt-svc     h3=":443"; ma=86400
cache-control   max-age=43200
cf-cache-status     HIT
cf-ray  a2cdd167af1e3442-MIA
content-length  2
content-type    application/json; charset=utf-8
date    Tue, 18 Aug 2026 03:26:36 GMT
etag    W/"2-vyGp6PvFo4RvsFtPoIWeCReyIC8"
expires     -1
nel     {"report_to":"heroku-nel","response_headers":["Via"],"max_age":3600,"success_fraction":0.01,"failure_fraction":0.1}
pragma  no-cache
report-to   {"group":"heroku-nel","endpoints":[{"url":"https://nel.heroku.com/reports?s=v4mhNiMtX4kH79NDvzVdEmSIVvGxCdIQ8pKxrkSwNsw%3D\u0026sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d\u0026ts=1787006486"}],"max_age":3600}
reporting-endpoints     heroku-nel="https://nel.heroku.com/reports?s=v4mhNiMtX4kH79NDvzVdEmSIVvGxCdIQ8pKxrkSwNsw%3D&sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d&ts=1787006486"
server  cloudflare
server-timing   cfCacheStatus;desc="HIT"
server-timing   cfEdge;dur=5,cfOrigin;dur=0
vary    Origin, Accept-Encoding
via     2.0 heroku-router
x-content-type-options  nosniff
x-powered-by    Express
x-ratelimit-limit   1000
x-ratelimit-remaining   999
x-ratelimit-reset   1787006536

## Request Headers
:authority  jsonplaceholder.typicode.com
:method     GET
:path   /posts/999
:scheme     https
accept  text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
accept-encoding     gzip, deflate, br, zstd
accept-language     es-US,es-419;q=0.9,es;q=0.8
priority    u=0, i
sec-ch-ua   "Not=A?Brand";v="99", "Google Chrome";v="151", "Chromium";v="151"
sec-ch-ua-mobile    ?0
sec-ch-ua-platform  "Windows"
sec-fetch-dest  document
sec-fetch-mode  navigate
sec-fetch-site  none
sec-fetch-user  ?1
upgrade-insecure-requests   1
user-agent  Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36

## Conclusion
Esta petición GET al recurso /posts/999 devolvió un 404 Not Found, indicando que el post con ese ID no existe en la API, aunque el servidor respondió correctamente con un cuerpo JSON válido (content-type: application/json) de apenas 2 bytes (probablemente {}), en lugar de fallar silenciosamente. Curiosamente, la respuesta muestra cf-cache-status: HIT con un age de 17109 segundos (~4.75 horas), lo que revela que Cloudflare también cachea respuestas de error 404, ya que estas cuentan como respuestas válidas y estables desde la perspectiva del CDN. Se observan además headers de seguridad y control como x-content-type-options: nosniff (previene sniffing de MIME) y pragma: no-cache junto a expires: -1, una combinación algo contradictoria con el cache-control: max-age=43200, típica de configuraciones heredadas en Express/Heroku. El rate limiting sigue activo y sin consumirse apenas (x-ratelimit-remaining: 999), y los headers de request corresponden a una navegación directa del navegador (sec-fetch-mode: navigate, sec-fetch-user: ?1), es decir, la URL fue visitada directamente en la barra de direcciones, no llamada vía JavaScript/fetch. En general, este caso ejemplifica cómo una API REST bien diseñada maneja recursos inexistentes: responde con el código de estado semánticamente correcto (404) en vez de un 200 con contenido vacío, manteniendo consistencia y previsibilidad para los consumidores del servicio.