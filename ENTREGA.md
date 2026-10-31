# Entrega · Duelo de herramientas

**Equipo:** ______cypress________________  
**Integrantes:** ________julian ramirez - juan jose gutierrez
 
**Repositorio:** ___https://github.com/juangutierrezlc-ai/laboratorio_verificacion_automatizacionV2/blob/main/kits/cypress/cypress/e2e/duelo.cy.js___________________  
**Herramienta que nos tocó:** ☐ Selenium + Mocha &nbsp; x Cypress &nbsp; ☐ Playwright + Cucumber  
**Escenario que nos tocó:** ______________________

> Completa este archivo a medida que avanzas (cada sección dice en qué parte de la guía se llena).
> Lo que se mide con números lo guarda el medidor en `medidas.json`; aquí va lo que un número no dice.
> Escribe con tus palabras: las respuestas copiadas de la guía, de otro equipo o de un asistente sin pasar por tu criterio no cuentan.

Archivos que entregan, todos en el repositorio y con `git push`:

| Archivo | Quién lo escribe | Parte |
|---|---|---|
| `ENTREGA.md` (este) | ustedes | 1 a 6 |
| `autoinforme.json` | ustedes (minutos y diagnóstico) | 2 a 4 |
| `medidas.json` y `medidas-control.json` | los genera el medidor (`npm run medir`) | 4 |
| `MATRIZ.md` | ustedes | 5 |
| `ADR.md` | ustedes | 6 |
| Las pruebas de su kit (las tres historias) | ustedes | 1 a 3 |

---

## 1. Qué hace la herramienta por nosotros (Parte 1)

Lean el ejemplo resuelto (US-01 CA1) en su kit, **línea por línea**, y los archivos de `soporte` o de configuración
que vienen con él. Para cada tarea que alguien debe cumplir en una prueba de interfaz, digan **quién la hace**:
*la herramienta sola*, *una librería que hubo que sumar* (¿cuál?) o *código nuestro*. Escriban el archivo y la línea.

| Tarea | ¿Quién la hace? | ¿Dónde lo vemos? (archivo y línea) |
|---|---|---|
| Abrir el navegador y cerrarlo al terminar | | |
| Esperar a que el elemento exista o se pueda usar | | |
| Reintentar una comprobación que todavía no se cumple | | |
| Ejecutar las pruebas, contarlas y decir cuántas pasaron | | |
| Comprobar un valor y mostrar «esperado» y «recibido» | | |
| Leer el texto de un `alert()` del navegador *(lo descubren en la Parte 2)* | | |
| Dejar evidencia (captura, video o traza) cuando una prueba falla | | |

**Con esta tabla:** ¿la herramienta que nos tocó es una *librería*, un *framework*, o una librería con piezas que
tuvimos que armar nosotros? Respondan en dos frases con la idea «la librería la llamas tú; el framework te llama a ti».

> _Respuesta: cypress es un framework. minetras que una libreria la llamas tu como programador invocando sus funciones el desarrollo del codigo cuando necestas resolver un problema en especifico , cypreess toma el control total en un entorno de ejecucion, del navegador y del ciclo de vida de los test, encargose de agregar en su propia estrutura en tu codigo o dentro de tu codigo.

en cypress, la herrmienta sola se encarga de manera automatica de abrir y cerra el nevegadro y esperar a que los elementos existan, reintentar las comprobaciones pendietes, ejecutar y contabilizar los resultados de los test y registrar la evidencia en caso de fallas; por otra parte , la verificacion de valores mostrando <<esperando>> y <<recibido>> la realiza una libreria integrada (chai) en las linear de afirmacion dentro del archivo de prueba minetras que el leer el texto de un alert() del navegador requiere de codigo nuestro mediante la escucha del evento dentro del scrip de prueba.

## 2. Bitácora de las historias (Partes 2 y 3)

Una columna por historia. «Minutos» son los mismos que anotan en `autoinforme.json`: desde que empiezan a escribir
hasta que ven la prueba en verde.

| | US-04 CA2 (7 mochilas, stock 6) | US-09 CA1 (DESC10) |
|---|---|---|
| Minutos hasta el verde | | |
| Primer intento que **no** funcionó: qué escribimos y qué dijo la herramienta | | |
| Mensaje de error que nos ayudó (o que nos confundió) | | |
| Qué tuvimos que buscar en la documentación (enlace) | | |
| Qué haría distinto un equipo con más experiencia en esta herramienta | | |

**Lo más distinto frente a US-01 CA1** (el ejemplo resuelto): ¿qué cambió al leer un `alert()`, al elegir *dentro de
una tarjeta* y al leer un valor del carrito? Piensen en esperas, selectores y en cómo leyeron el resultado.

> _Respuesta:
US-01 CA1 es una sola línea: cy.get('h3').should('have.length', 8), con un selector global y una comprobación que reintenta sola. En CA2 cambiaron tres cosas. El alert(): Cypress lo acepta solo, pero no lo muestra en la prueba, así que para leer su texto hubo que escuchar el evento window:alert con un stub antes del clic. Es lo único que tuvimos que preparar por adelantado. El selector: ya no sirve buscar en toda la página, porque hay ocho botones «Agregar»; hubo que ubicar la tarjeta por su título y buscar con .within() dentro de ella. En CA3 el reto fue leer un valor que aparece después: la fila «Descuento» no existe hasta aplicar el código, pero no tuvimos que escribir esperas, porque cy.contains('dt', /^Descuento/) y should reintentan hasta que aparece. Leímos el resultado en el <dd> hermano con .siblings('dd'). En resumen: las esperas las siguió haciendo la herramienta, y lo que más cambió fueron los selectores (de global a «dentro de una tarjeta» y «hermano de una etiqueta») y la forma de leer un aviso que no está en la página.

## 3. Lo que medimos (Parte 4)

Pega el resumen que imprimió `npm run medir` en tu kit y en el control (Playwright Test):

```text
Midiendo: Cypress · 10 corridas · carpeta kits\cypress

  corrida 1/10   16.6 s  ✓ pasan las 3
  corrida 2/10   17.8 s  ✓ pasan las 3
  corrida 3/10   17.7 s  ✓ pasan las 3
  corrida 4/10   18.2 s  ✓ pasan las 3
  corrida 5/10     18 s  ✓ pasan las 3
  corrida 6/10   18.2 s  ✓ pasan las 3
  corrida 7/10   18.8 s  ✓ pasan las 3
  corrida 8/10   19.1 s  ✓ pasan las 3
  corrida 9/10   19.8 s  ✓ pasan las 3
  corrida 10/10  17.9 s  ✓ pasan las 3

Resumen
  Velocidad ......... mediana 18.12 s  (mínimo 16.6 · máximo 19.78)
  Estabilidad ....... 10 de 10 corridas completas
  Código ............ 27 líneas de pruebas + 11 de soporte = 38
  cypress............ 16.2.0 instalada · última publicación hace 2 días (v16.2.1)
  Autoinforme ....... minutos {"instalacion":20,"ca2":30,"ca3":11}, diagnóstico 4/5
```

```text
Midiendo: Playwright Test (control) · 10 corridas · carpeta control\playwright

  corrida 1/10      4 s  ✓ pasan las 3
  corrida 2/10    4.3 s  ✓ pasan las 3
  corrida 3/10    4.3 s  ✓ pasan las 3
  corrida 4/10    4.7 s  ✓ pasan las 3
  corrida 5/10    4.9 s  ✓ pasan las 3
  corrida 6/10      5 s  ✓ pasan las 3
  corrida 7/10    5.4 s  ✓ pasan las 3
  corrida 8/10    5.2 s  ✓ pasan las 3
  corrida 9/10      5 s  ✓ pasan las 3
  corrida 10/10   4.7 s  ✓ pasan las 3

Resumen
  Velocidad ......... mediana 4.83 s  (mínimo 4.03 · máximo 5.43)
  Estabilidad ....... 10 de 10 corridas completas
  Código ............ 34 líneas de pruebas + 14 de soporte = 48
  @playwright/test... 1.64.1 instalada · última publicación hace 16 días (v1.64.1)
```

Mediana de nuestro kit: 18,12 s · Mediana del control en nuestra máquina: 4,83 s · Veces el control (kit ÷ control): 3,75×
Corridas completas de nuestro kit: 10 de 10
Líneas de código (pruebas + soporte): 38
Puntos de diagnóstico (de 5): 4

**El fallo a propósito.** ¿Qué rompieron y cómo? Pega las primeras 10 líneas de lo que dijo la herramienta y señala
qué ayudaba a encontrar la causa y qué faltaba.

Cambiamos el 8 por 9 en:
cypress/e2e/duelo.cy.js: cy.get('h3').should('have.length', 9); y corrimos npm test.

```text
  Duelo · tres criterios de aceptación
    1) US-01 CA1: el catálogo muestra 8 productos
    √ US-04 CA2: no deja agregar 7 mochilas de una vez (stock 6) y avisa (95ms)
    √ US-09 CA1: DESC10 descuenta el 10 % del subtotal (35ms)

  2 passing (5s)
  1 failing

  1) Duelo · tres criterios de aceptación
       US-01 CA1: el catálogo muestra 8 productos:
     AssertionError: Timed out retrying after 4000ms: Not enough elements found. Found '8', expected '9'.
```

**Las cinco preguntas del diagnóstico** (se contestan **con el kit tal como llegó**, y el «sí» o «no» va en `autoinforme.json`).
En la última columna digan *de dónde vino* cada evidencia: de la **herramienta** (sola), de la **configuración del kit** o de
**código nuestro**.

Qué ayudaba: el nombre de la prueba que falló, el tipo de comprobación (cantidad de elementos), el valor encontrado (8) y el esperado (9), la línea duelo.cy.js:13:17 y una captura guardada en cypress/screenshots/. También dice que reintentó durante 4 segundos, así que no fue un problema de esperar poco.

Qué faltaba: el mensaje no repite el selector (h3), aunque se encuentra yendo a la línea 13. No quedó video (Video: false) ni una traza para repasar los pasos sin volver a correr la prueba.

Las cinco preguntas del diagnóstico (se contestan con el kit tal como llegó, y el «sí» o «no» va en autoinforme.json). En la última columna digan de dónde vino cada evidencia: de la herramienta (sola), de la configuración del kit o de código nuestro.

| Pregunta (campo en `autoinforme.json`) | ¿Sí o no? | ¿De dónde vino? |
|---|:---:|---|
| ¿El mensaje dice **qué** falló (el elemento o la comprobación), sin que haya que adivinar? (`diceQueFallo`) | | |
| ¿Muestra el valor **esperado** y el **recibido**? (`esperadoYRecibido`) | | |
| ¿Señala la **línea de nuestra prueba** donde falló? (`lineaDeLaPrueba`) | | |
| ¿Quedó una **captura de pantalla** (o un video) de la falla en el disco? (`capturaOVideo`) | | |
| ¿Quedó una **traza o un informe** para repasar la falla paso a paso sin volver a correrla? (`trazaOInforme`) | | |

-	Herramienta: AssertionError … Not enough elements found y el nombre de la prueba.

-	Herramienta: Found '8', expected '9' y el diff -8 / +9.

-	Herramienta: duelo.cy.js:13:17 en el stack.

-	[Herramienta / Configuración del kit: revisar cypress.config.js. Si no define screenshotOnRunFailure, es la herramienta sola]. Solo captura, sin video.

-	En cypress run no se genera traza ni informe; la repetición paso a paso (Test Replay) está en Cypress Cloud. 



**Tres cosas que nuestra medición NO demuestra** (pistas: cuántas pruebas, cuántas corridas, cuántas máquinas,
qué mide el tiempo, qué cuenta una «línea de código»):

1.Cómo se comporta con muchas pruebas: medimos 3 pruebas sobre una tienda pequeña, no 300. Con más pruebas importan el paralelismo y la organización del código, y eso no se vio.

2.Que sea estable en general: 10 de 10 corridas en una sola máquina, en Chrome y contra una copia local de la tienda. Otros navegadores, otras máquinas o la red real podrían dar fallos que 10 corridas no muestran.

3.Cuánto cuesta mantenerla: 38 líneas y 41 minutos miden lo que costó escribir las primeras pruebas, no lo que cuesta cambiarlas cuando la interfaz cambia durante meses. Además, el tiempo medido es el de npm test completo (incluye abrir el navegador), no solo el de las pruebas.

## 4. Mirando el tablero (Parte 5)

Abran el tablero de la clase (el enlace lo da el docente) y respondan **con datos del tablero**, no con opiniones:

1. ¿Qué herramienta fue más rápida, medida en «veces el control»? ¿Y la más estable? ¿Hubo diferencias grandes **dentro** de una misma herramienta entre equipos? ¿A qué lo atribuyen?
2. ¿Qué herramienta dejó mejor diagnóstico y qué parte vino «de fábrica» o la tuvo que armar el equipo?
3. Un dato del tablero que les pareció raro. ¿Qué preguntarían a ese equipo antes de usarlo como evidencia?

> _Respuestas:_
Respuestas:

Estado del tablero al responder: 1 equipo (Cypress), 10 corridas medidas. Selenium + Mocha y Playwright + Cucumber tienen 0 equipos.

Velocidad: no se puede responder. Nuestro registro tiene el aviso “sin control”, así que no hay “veces el control” y la mediana de 18,1 s no se puede comparar con otra máquina. Estabilidad: Cypress tuvo 10/10 corridas completas, pero sin las otras dos herramientas no sabemos si es la más estable. Diferencias dentro de una herramienta: no se pueden ver, porque hay un solo equipo de Cypress.
Diagnóstico: Cypress tiene 4 de 5. Según nuestro fallo a propósito, las cuatro evidencias vinieron de la herramienta: el mensaje, el esperado/recibido (8 vs 9), la línea (duelo.cy.js:13:17) y la captura. La que faltó fue la traza: en cypress run no queda ninguna, y la repetición paso a paso depende de Cypress Cloud. No podemos decir cuál herramienta tuvo mejor diagnóstico sin los datos de Selenium y Playwright.
Dato raro: el nuestro. La columna “× control” aparece vacía (“—”) con el aviso “sin control” aunque corrimos el control. Antes de usarlo como evidencia, revisaríamos que medidas-control.json esté en la raíz del repositorio y que sus corridas hayan pasado las 3 pruebas. Además, “2 días del paquete” dice que Cypress se publicó hace poco, no que vaya a seguir disponible dentro de diez años, que es lo que le importa a nuestro cliente.

## 5. Matriz y decisión (Partes 5 y 6)

x `MATRIZ.md` completa (pesos que suman 100, puntajes con evidencia, total y prueba de sensibilidad)  
x `ADR.md` completo (una página, con consecuencias negativas y qué nos haría cambiar de opinión)  
x `medidas.json`, `medidas-control.json` y `autoinforme.json` en el repositorio, con `git push`

**Nuestra recomendación en una frase:**

> _…_

## 6. Reflexión

1. Antes de medir, ¿qué herramienta habríamos recomendado? ¿Cambió algo después de ver los datos de **todas** las herramientas? Si la que recomendamos no es la que nos tocó, ¿por qué? Si lo es, ¿qué habría pasado si nos hubiera tocado otra?
2. ¿Qué evidencia nos hizo falta y no pudimos medir en esta actividad (por ejemplo: 300 pruebas en lugar de 3, otros navegadores, un mes de mantenimiento)?
3. En una automatización real, ¿qué parte del esfuerzo creen que es **escribir** las primeras pruebas y qué parte es **mantenerlas**? ¿Qué parte de esto no capta nuestra actividad?
4. Si el cliente fuera la empresa donde quieren trabajar, ¿qué pesos cambiarían en la matriz?
5. Si usaron un asistente de IA: ¿en qué momentos ayudó y en cuáles hubo que corregirlo? ¿Cómo cambia eso lo que significan los minutos de `autoinforme.json`?
