# Análisis 1: Petición GET - example.com

## Información general
Request URL - https://example.com/
Request Method - GET
Status Code - 304 Not Modified
Remote Address - 172.66.147.243:443
Referrer Policy - strict-origin-when-cross-origin

## Response headers
age - 6173
allow - GET, HEAD
cf-cache-status - HIT
cf-ray - a2cd8b030a00a4eb-MIA
date - Tue, 18 Aug 2026 02:38:33 GMT
etag - "6a7cd47d-22f"
last-modified - Wed, 12 Aug 2026 20:15:57 GMT
server - cloudflare

## Request Headers
:authority - example.com (dominio al que se dirige la peticion)
:method - GET (metodo http usado, se esta solicitando obtener un recurso)
:path - / (la ruta del recurso solicitado del dominio)
:scheme - https (el protocolo usado para la conexion)
accept - text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7 (indica los tipos de contenido y el navegador puede procesar y en que orden de preferencia)
accept-encoding - gzip, deflate, br, zstd (indica algoritmos de comprension soporta el navegador para reducir el tamaño de la respuesta)
accept-language - es-US,es-419;q=0.9,es;q=0.8 (indica el o los idiomas preferidos del usuario para el contenido de respuesta)
cache-control - max-age=0 (le dice al servidor que revalide el contenido en cache antes de usarlo)
if-modified-since - Wed, 12 Aug 2026 20:15:57 GMT (pide al servidor que solo envie el recurso si fue modificado despues de la fecha indicada)
priority - u=0, i (indica la prioridad de esta peticion respecto a otras, usado para optimizar cargas)
sec-ch-ua - "Not=A?Brand";v="99", "Google Chrome";v="151", "Chromium";v="151" (client hint que informa la marca y version del navegador)
sec-ch-ua-mobile - ?0 (indica si el dispositivo es movil, 0 es no y 1 es si)
sec-ch-ua-platform - "Windows" (indica el SO del cliente)
sec-fetch-dest - document (indica el destino de la peticion; aqui significa que se esta cargando un documento HTML completo)
sec-fetch-mode - navigate (indica que la peticion corresponde a una navegacion)
sec-fetch-site - none (indica la relacion entre el origen que la peticion y el destino)
sec-fetch-user - ?1 (indica que la peticion fue activada por una accion real del usuario, no por un script)
upgrade-insecure-requests - 1 (le dice al servidor que el navegador prefiere recibir la respuesta en https si hay una version insegura disponible)
user-agent - Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36 (identifica el navegador, motor de renderizado y SO del cliente que hace la peticion)

## Tiempos de carga
Queued at 0 ɥs
Started at 3.85 ms
Connection Start - Stalled duration 2.68 ms
Request Sent duration 0.16 ms
Waiting for server response duration 112.47 ms
Content Download duration 1.30 ms
total 120.46 ms

## Conclusion
Esta peticion GET a example.com resulto en un 304 Not Modified, lo que indica que el navegador ya tenía el recurso en cache y el servidor confirmo que no hubo cambios desde la ultima descarga (coincide el if-modified-since con el last-modified), evitando asi transferir contenido innecesario. La respuesta fue servida por Cloudflare (server: cloudflare) directamente desde su cache de borde (cf-cache-status: HIT), lo cual explica por que el age es de 6173 segundos, es decir, el recurso lleva más de 1 hora y 42 minutos almacenado en ese nodo. El tiempo total de carga fue de apenas 120.46 ms, con el mayor peso concentrado en la espera de respuesta del servidor (112.47 ms), mientras que la conexion y la descarga de contenido fueron practicamente instantaneas. En general, esto refleja un comportamiento optimo: uso eficiente de cache tanto en cliente como en CDN, baja latencia y una peticion liviana al no requerir reenvio del cuerpo del recurso.