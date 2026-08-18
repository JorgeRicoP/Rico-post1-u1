# Análisis 3 — Petición POST Simulada con Postman

## Peticion enviada 201 Created
### Codigo de estado esperado
201 Created

### Body
{
    "title": "Laboratorio Programacion Web",
    "body": "Analisis de peticiones HTTP con Postman.",
    "userId": 1,
    "id": 101
}

### Headers
:status     201
date    Tue, 18 Aug 2026 03:44:41 GMT
content-type    application/json; charset=utf-8
content-length  127
location    https://jsonplaceholder.typicode.com/posts/101
access-control-allow-credentials    true
access-control-expose-headers   Location
cache-control   no-cache
etag    W/"7f-+oN5bcd5gPS3m4JG6wRHEiiFBkA"
expires     -1
nel     {"report_to":"heroku-nel","response_headers":["Via"],"max_age":3600,"success_fraction":0.01,"failure_fraction":0.1}
pragma  no-cache
report-to   {"group":"heroku-nel","endpoints":[{"url":"https://nel.heroku.com/reports?s=4UIP2vV1ke1V1%2FDIZvaS1Za6y0GA7RlN7jHa6UlFjv4%3D\u0026sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d\u0026ts=1787024681"}],"max_age":3600}
reporting-endpoints     heroku-nel="https://nel.heroku.com/reports?s=4UIP2vV1ke1V1%2FDIZvaS1Za6y0GA7RlN7jHa6UlFjv4%3D&sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d&ts=1787024681"
server  cloudflare
vary    Origin, X-HTTP-Method-Override, Accept-Encoding
via     2.0 heroku-router
x-content-type-options  nosniff
x-powered-by    Express
x-ratelimit-limit   1000
x-ratelimit-remaining   999
x-ratelimit-reset   1787024716
cf-cache-status     DYNAMIC
cf-ray  a2cdebe0cc5eb2bc-MIA
alt-svc     h3=":443"; ma=86400

### Resultados de los tests
(PASSED) Status 201 Created
(PASSED) Respuesta incluye id asignado

### Diferencias entre GET y POST
| Aspecto | GET | POST |
|---|---|---|
| Propósito | Solicitar/leer un recurso existente | Crear un nuevo recurso en el servidor |
| Cuerpo (body) | No envía body | Envía un body (JSON) con los datos del nuevo recurso |
| Código de estado típico | 200 OK / 304 Not Modified | 201 Created |
| Idempotencia | Sí (repetirla no cambia el estado del servidor) | No (cada envío crea un nuevo recurso) |
| Cacheable | Sí, generalmente | No, generalmente |
| Datos visibles | Pueden ir en la URL (query params) | Van en el cuerpo, no en la URL |

### Conclusion
Para concluir, mientras que las peticiones GET analizadas anteriormente se usaron para leer información (una página HTML, un ícono, un post existente), esta petición POST se usó para crear un nuevo recurso en el servidor. Esto se refleja tanto en el código de estado devuelto (201 en vez de 200/304/404) como en la necesidad de enviar un Content-Type y un cuerpo JSON, elementos ausentes en las peticiones GET previas.