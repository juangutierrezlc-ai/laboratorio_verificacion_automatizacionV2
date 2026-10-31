Matriz de decisión

Equipo: Cypress · Julián Ramírez Espinosa, Juan José Gutiérrez
Escenario: E6 · Entidad Pública (contrato de diez años, cambia de proveedor entre licitaciones, auditoría anual, sin servicios de pago ni nube)

Las tres opciones son las mismas de la presentación: Selenium (con Mocha en este duelo), Cypress y Playwright. La pregunta de si hace falta una capa BDD (Cucumber) por encima va aparte, en el ADR.md.

Cómo se llena (en este orden)
Pesos. Repartan 100 puntos entre los ocho criterios según lo que el escenario necesita. Un criterio puede valer 0 si no importa. Escriban en una frase por qué pesa lo que pesa: esa frase se califica.
Puntajes de 1 a 5 por herramienta y criterio (5 = lo cubre muy bien). Cada puntaje lleva evidencia, con una etiqueta:
[tablero] un dato de la clase (diga cuál: «Cypress, 10/10 corridas, mediana 1,8× el control»).
[doc] documentación oficial (pongan el enlace y lo que dice).
[exp] lo que vivió el equipo en el laboratorio (qué pasó, en qué parte).
Un puntaje sin evidencia no cuenta. Una opinión sin dato se marca como opinión: [opinión].
Total = Σ (peso × puntaje) ÷ 100. El máximo es 5,00.
Prueba de sensibilidad. Suban 10 puntos al peso del criterio del que más dudaron (bajándoselos a otro). ¿Cambió el ganador? Anótenlo abajo: si cambia con 10 puntos, la decisión es frágil y el ADR debe decirlo.

De dónde sale la evidencia de cada criterio
#	Criterio	La pregunta	En el duelo se mide…	Para el resto, busquen…
1	Encaje	¿Calza con el lenguaje, las habilidades y los procesos del equipo del escenario?	[exp] minutos hasta el verde y obstáculos (ENTREGA.md §2)	[doc] lenguajes que soporta
2	Cobertura	¿Cubre los navegadores, móviles y APIs que el escenario necesita?	— (no se mide aquí)	[doc] navegadores y plataformas soportados
3	Estabilidad	¿Espera sola o las esperas se programan a mano? ¿Falló alguna corrida?	[tablero] corridas completas / corridas	[exp] esperas que tuvimos que escribir
4	Diagnóstico	Cuando falla, ¿se ve por qué?	[tablero] puntos de diagnóstico (0 a 5)	
5	Velocidad	¿Cuánto tarda, descontando la máquina?	[tablero] mediana y «veces el control»	[doc] paralelismo
6	Integración	¿Se lleva bien con CI, informes y Jira?	[exp] qué informe dejó y en qué formato	[doc] guías de integración continua
7	Comunidad y futuro	¿Quién la mantiene y hasta cuándo?	[tablero] días desde la última publicación	[doc] repositorio, frecuencia de versiones, quién la respalda
8	Costo total	Licencias + aprender + mantener	[tablero] líneas de código · [exp] minutos	[doc] licencia y servicios de pago

| Criterio | Peso (%) | Selenium | Cypress | Playwright | ¿Por qué ese peso? · Evidencia de los puntajes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **1 · Encaje** | 5 | 5 | 2 | 4 | **Peso:** no se sabe qué lenguaje usará el siguiente proveedor; pesa poco, pero premia a la herramienta que acepte varios.<br>**Selenium:** [doc] Java, Python, C#, Ruby y JavaScript (https://www.selenium.dev/documentation/).<br>**Cypress:** [doc] solo JavaScript/TypeScript; [exp] 41 min para CA2 + CA3 (30 + 11), el mayor obstáculo fue leer el alert().<br>**Playwright:** [doc] JavaScript/TypeScript, Python, Java y .NET (https://playwright.dev/docs/languages). |
| **2 · Cobertura** | 15 | 5 | 3 | 3 | **Peso:** debe correr en Chrome, Edge y Firefox con versiones que fija TI, algunas en equipos antiguos.<br>**Selenium:** [doc] los fabricantes de cada navegador mantienen drivers que siguen el estándar W3C WebDriver (https://www.w3.org/TR/webdriver1/).<br>**Cypress:** [doc] Chrome, Edge y Firefox, pero oficialmente solo las últimas 3 versiones mayores: riesgo con versiones fijadas y equipos viejos (https://docs.cypress.io/app/references/launching-browsers).<br>**Playwright:** [doc] Chromium, Firefox y WebKit propios, más Chrome y Edge de marca; el Firefox es una compilación propia, no el Firefox que instala TI (https://playwright.dev/docs/browsers). |
| **3 · Estabilidad** | 15 | 3 | 5 | 5 | **Peso:** la auditoría anual revisa que las pruebas se repitan con el mismo resultado.<br>**Selenium:** [opinión] sin dato del tablero; [doc] la guía del duelo indica que en Selenium las esperas se escriben a mano (driver.wait, until.alertIsPresent).<br>**Cypress:** [tablero] 10/10 corridas completas; [exp] no escribimos esperas, los should reintentan solos.<br>**Playwright:** [exp] control en nuestra máquina, 10/10 corridas completas. |
| **4 · Diagnóstico** | 10 | 3 | 4 | 4 | **Peso:** un proveedor que llega en otra licitación debe entender las fallas sin haber escrito las pruebas.<br>**Selenium:** [opinión] sin dato del tablero; Mocha y assert muestran esperado/recibido y línea, pero no esperamos captura sin código adicional.<br>**Cypress:** [tablero] 4 de 5; [exp] mensaje, esperado/recibido, línea (duelo.cy.js:13:17) y captura sí; traza no.<br>**Playwright:** [opinión] provisional; no hicimos el fallo a propósito en el control y no hay equipo de Playwright en el tablero. |
| **5 · Velocidad** | 5 | 3 | 2 | 5 | **Peso:** no hay despliegues diarios ni un límite de minutos en el pipeline; unos segundos más no le cambian nada al cliente.<br>**Selenium:** [opinión] sin dato.<br>**Cypress:** [tablero] mediana 18,12 s = 3,75× el control (18,12 ÷ 4,83).<br>**Playwright:** [exp] control 4,83 s = 1,0× por definición. |
| **6 · Integración** | 10 | 3 | 3 | 4 | **Peso:** la auditoría necesita evidencia que se pueda guardar y entregar, generada sin nube.<br>**Selenium:** [opinión] el informe depende del ejecutor (Mocha); hay que armarlo.<br>**Cypress:** [exp] en el fallo a propósito solo quedó una captura .png, sin informe ni traza; la repetición paso a paso (Test Replay) está en Cypress Cloud (https://www.cypress.io/pricing).<br>**Playwright:** [doc] Playwright Test trae informes (HTML, JUnit, entre otros) sin servicios externos (https://playwright.dev/docs/test-reporters). |
| **7 · Comunidad y futuro** | 25 | 5 | 3 | 4 | **Peso:** es lo que le duele al cliente: que la herramienta deje de existir o cambie de licencia en cinco años, y la contratación favorece estándares abiertos sin un único fabricante.<br>**Selenium:** [doc] WebDriver es Recomendación del W3C desde 2018; Apache 2.0, titular sin ánimo de lucro (Software Freedom Conservancy) (https://selenium.dev/documentation/about/copyright).<br>**Cypress:** [tablero] 2 días desde la última publicación; [doc] licencia MIT, pero la mantiene una sola empresa cuyo negocio es Cypress Cloud (https://github.com/cypress-io/cypress).<br>**Playwright:** [exp] control: 16 días desde la última publicación; [doc] Apache 2.0, mantenida por Microsoft, un solo fabricante (https://github.com/microsoft/playwright). |
| **8 · Costo total** | 15 | 3 | 3 | 4 | **Peso:** no puede haber servicios de pago, y cada proveedor nuevo hereda y mantiene el código.<br>**Selenium:** [doc] Apache 2.0, gratis; [opinión] esperamos más código propio (esperas y evidencia a mano), sin dato de líneas.<br>**Cypress:** [tablero] 38 líneas, 41 min; [exp] instalación 20 min y ~600 MB; [doc] gratis, pero la traza depende de Cypress Cloud.<br>**Playwright:** [exp] control 48 líneas (34 de pruebas + 14 de soporte); [doc] Apache 2.0, gratis, sin servicio de pago necesario. |
| **Total ponderado (máx. 5,00)** | **100%** | **3,90** | **3,30** | **4,05** | — |





Cálculo:

Selenium: (5·5 + 15·5 + 15·3 + 10·3 + 5·3 + 10·3 + 25·5 + 15·3) ÷ 100 = 390 ÷ 100 = 3,90
Cypress: (5·2 + 15·3 + 15·5 + 10·4 + 5·2 + 10·3 + 25·3 + 15·3) ÷ 100 = 330 ÷ 100 = 3,30
Playwright: (5·4 + 15·3 + 15·5 + 10·4 + 5·5 + 10·4 + 25·4 + 15·4) ÷ 100 = 405 ÷ 100 = 4,05

Prueba de sensibilidad
Criterio que subimos 10 puntos: Cobertura (15 → 25), porque es del que más dudamos: no sabemos qué versiones antiguas de los navegadores tienen los funcionarios (se lo bajamos a: Estabilidad, 15 → 5).
¿Cambió el ganador? ☐ No ☒ Sí → ahora gana: Selenium (4,10 frente a 3,85 de Playwright y 3,10 de Cypress).
Lo que esto nos dice de nuestra decisión: es frágil. Playwright gana por solo 0,15 puntos, y basta mover 10 puntos hacia cobertura para que gane Selenium. Además, el puntaje de estabilidad de Selenium (3) es [opinión], porque no hay un equipo de Selenium en el tablero: si Selenium saca 10/10 corridas, su estabilidad sube a 5 y Selenium gana con 4,20. El ADR debe decir que la decisión se juega entre Selenium y Playwright, y que Cypress queda tercero en todos los casos que probamos.

Ganador de la matriz

Playwright con 4,05 puntos sobre 5,00 (Selenium muy cerca con 3,90; resultado provisional hasta tener datos de Selenium en el tablero).
¿Coincide con lo que habríamos elegido antes de medir? ☐ Sí x No → ¿qué cambió? [siento que pueden influir varios aspectos como la maquina donde se esta ejecutando las pruebas posiblemente tambien temas de conexion con el servidor y al internet.]