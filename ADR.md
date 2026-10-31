# ADR-001 · Herramienta de pruebas de interfaz para «Entidad Pública (E6)»
Estado: Propuesta
Fecha: 2026-10-30
Equipo: Cypress · Julián Ramírez Espinosa, Juan José Gutiérrez

> Una página, como en la presentación: contexto, opciones, criterios, decisión y consecuencias. Se escribe para alguien
> que no estuvo en la clase y llega dentro de un año preguntando «¿por qué eligieron esto?». Borren estas líneas al entregar.

## Contexto

_(3 a 5 líneas: quién es el cliente, qué necesita y qué restricciones pesan. Hechos del escenario, sin adjetivos.)_
Una entidad del Estado contrata software para operarlo y mantenerlo durante diez años y cambia de proveedor entre licitaciones, así que las pruebas deben poder heredarlas otros equipos. Las reglas de contratación favorecen estándares abiertos y software sin dependencia de un único fabricante. No se permiten servicios de pago ni dependencia de la nube. Los navegadores son Chrome, Edge y Firefox, con versiones controladas por TI y algunos equipos antiguos. Una auditoría anual revisa que las pruebas se repitan con el mismo resultado.

## Opciones consideradas

Selenium (con Mocha), Cypress y Playwright. La matriz con pesos y puntajes está en [`MATRIZ.md`](MATRIZ.md).
Criterios que más pesaron en este escenario: _(los dos o tres con más peso)_.

Selenium (con Mocha), Cypress y Playwright. La matriz con pesos y puntajes está en MATRIZ.md. Criterios que más pesaron en este escenario: Comunidad y futuro (25), Cobertura (15), Estabilidad (15) y Costo total (15).

## Decisión

Recomendamos **__________** porque _(2 a 4 líneas que citen los criterios que más pesan y los datos del tablero que lo respaldan)_.

Recomendamos Playwright porque obtuvo el mayor total de la matriz (4,05 sobre 5,00, frente a 3,90 de Selenium y 3,30 de Cypress). En nuestra máquina, el control en Playwright Test pasó 10 de 10 corridas, con una mediana de 4,83 s; Cypress, en la misma máquina, tardó 3,75 veces eso (18,12 s). Además, tiene licencia Apache 2.0 y genera sus informes sin servicios en la nube, lo que cumple las restricciones del cliente. La recomendación es provisional y frágil: Selenium quedó a 0,15 puntos y gana si se da más peso a la cobertura o si su estabilidad medida resulta igual de buena.

## Consecuencias

- **Lo que ganamos:**
- **Lo que perdemos o se complica** _(al menos dos; una decisión sin consecuencias negativas no está completa)_:
- **Lo que tendremos que hacer** _(formación, migración, configuración, presupuesto…)_:

Lo que ganamos: pruebas que esperan solas a los elementos (menos esperas escritas a mano), informes locales para la auditoría sin pagar ningún servicio, y una herramienta que se puede usar en JavaScript, Python, Java o .NET, según el lenguaje del siguiente proveedor.

Lo que perdemos o se complica:

1.Dependemos de un solo fabricante (Microsoft). No es un estándar abierto como WebDriver del W3C, que es justo lo que le preocupa al cliente para los próximos diez años.

2.Playwright usa sus propias compilaciones de Firefox, no el Firefox que instala y controla TI; las pruebas no corren exactamente en el navegador de los funcionarios.

3.No sabemos cómo se comporta en los equipos antiguos de la entidad: no lo medimos.

Lo que tendremos que hacer: probar la suite en un equipo antiguo de la entidad con sus versiones de Chrome, Edge y Firefox; dejar documentados la versión de Playwright y la configuración para que el siguiente proveedor pueda repetir las pruebas; y formar al equipo que herede el proyecto.

## Qué nos haría cambiar de opinión

_(Dos o tres condiciones concretas y medibles: «si el equipo pasa a trabajar en Python», «si la suite supera las 300 pruebas y el tiempo de CI pasa de 10 minutos», «si el cliente exige Safari»…)_

1.Si un equipo de Selenium del tablero muestra 10 de 10 corridas completas: con ese dato Selenium sube a 4,20 y pasa a ser el ganador.

2.Si la entidad exige probar en la versión exacta de Firefox que instala TI, o en versiones de Chrome o Edge que Playwright ya no soporta.

3.Si Playwright cambia su licencia o Microsoft deja de publicar versiones durante más de 12 meses.

## ¿Con capa BDD (Cucumber) o sin ella?

_(3 líneas. Usen lo que midieron los equipos de Playwright + Cucumber frente al control (Playwright Test solo): líneas de código, tiempo, minutos de escritura. Y respondan: en este escenario, ¿quién leería los archivos `.feature`?)_

No tenemos datos de un equipo de Playwright + Cucumber en el tablero para compararlo con el control (48 líneas, 4,83 s), así que no podemos medir cuánto código o tiempo agrega la capa. En este escenario nadie escribe criterios en Dado / Cuando / Entonces y no hay analistas de negocio que vayan a leer los .feature; los lectores serían el proveedor siguiente y, en todo caso, el auditor. Por eso recomendamos sin Cucumber, salvo que el auditor pida leer las pruebas en lenguaje natural.

## Evidencia usada

- Tablero de la clase, consultado el ____-__-__ a las __:__ : _(qué datos usaron)_
- Documentación consultada: _(enlaces)_

Tablero de la clase, consultado el 2026-10-30 a las 21:20: Cypress, 3/3 pruebas, 10/10 corridas completas, mediana 18,1 s, 38 líneas, 41 minutos (CA2 + CA3), diagnóstico 4 de 5, 2 días desde la última publicación, aviso «sin control». Solo aparecía nuestro equipo. Control medido por nosotros (medidas-control.json): Playwright Test, 10/10 corridas, mediana 4,83 s, 48 líneas, 16 días desde la última publicación.

Documentación consultada:
-WebDriver, Recomendación W3C: https://www.w3.org/TR/webdriver1/
-Licencia de Selenium: https://selenium.dev/documentation/about/copyright
-Navegadores de Cypress: https://docs.cypress.io/app/references/launching-browsers
-Licencia de Cypress: https://github.com/cypress-io/cypress
-Precios de Cypress Cloud: https://www.cypress.io/pricing
-Navegadores de Playwright: https://playwright.dev/docs/browsers
-Lenguajes de Playwright: https://playwright.dev/docs/languages
-Informes de Playwright Test: https://playwright.dev/docs/test-reporters