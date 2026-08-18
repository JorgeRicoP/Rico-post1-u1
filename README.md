# Post-contenido — Unidad 1: Fundamentos de la Web

## Descripción
Repositorio del laboratorio de la Unidad 1 de Programación Web —
Séptimo Semestre. Contiene dos partes: configuración del entorno
de desarrollo (parte-1-entorno/) y análisis de peticiones HTTP con
Chrome DevTools y Postman (parte-2-analisis-http/).

## Parte 1 — Entorno de desarrollo
Página HTML básica inspeccionada con Chrome DevTools. Ver
parte-1-entorno/.

## Parte 2 — Análisis de peticiones HTTP
| # | Tipo | URL | Código |
|---|------|-----|--------|
| 1 | GET HTML | https://example.com | 200 OK |
| 2 | GET JSON (exitoso) | /posts/1 | 200 OK |
| 3 | GET JSON (fallido) | /posts/999 | 404 Not Found |
| 4 | POST JSON | /posts | 201 Created |

Ver parte-2-analisis-http/analisis/.

## Herramientas utilizadas
- VS Code, Git, GitHub
- Google Chrome + DevTools (panel Network)
- Postman (petición POST con tests)

## Conclusiones
Este laboratorio permitió comprender de forma práctica cómo funciona la comunicación cliente-servidor en la web, desde la configuración básica del entorno de desarrollo hasta el análisis detallado de peticiones HTTP reales. Se identificaron las diferencias clave entre los métodos GET y POST, así como el significado de los códigos de estado (200, 304, 404, 201) y su relación directa con el comportamiento esperado de una API REST. El uso de Chrome DevTools permitió observar de primera mano headers de caché, CDN (Cloudflare) y tiempos de carga, mientras que Postman facilitó la simulación de peticiones POST y la automatización de pruebas mediante scripts. En conjunto, estas herramientas reforzaron la importancia de los headers HTTP tanto para el rendimiento (cacheo, compresión) como para la seguridad y el control de acceso (rate limiting, CORS). Finalmente, el flujo de trabajo con Git y GitHub reforzó buenas prácticas de control de versiones, documentando cada análisis con commits descriptivos y organizados por partes del laboratorio.