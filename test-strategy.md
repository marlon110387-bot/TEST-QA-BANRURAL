
Estrategia de Pruebas - Juego "Adivina tu Número"

Objetivo

Verificar que el juego "Adivina tu número" funcione correctamente de acuerdo con los requisitos especificados por el banco financiero. Asegurar que la lógica del juego, la interfaz de usuario y los mensajes de feedback operen como se espera.

Alcance
•	Pruebas funcionales de la lógica del juego.
•	Validación de entradas del usuario.
•	Verificación de mensajes de error y éxito.
•	Comprobación del número de intentos.
•	Pruebas de usabilidad y interfaz de usuario.

Exclusiones
•	Pruebas de rendimiento o estrés.
•	Pruebas de seguridad.
•	Pruebas de compatibilidad con múltiples navegadores (a menos que se especifique).

Enfoque de Pruebas
•	Pruebas manuales para verificar el flujo del juego y los mensajes.
•	Pruebas de regresión después de las correcciones.

Tipos de Pruebas
1.	Pruebas de funcionalidad: Verificar que el juego genere un número aleatorio entre 1 y 100, que valide la entrada del usuario, que cuente los intentos correctamente y que muestre los mensajes apropiados.
2.	Pruebas de validación: Asegurar que solo se acepten números enteros y que se muestre una alerta para entradas no válidas.
3.	Pruebas de interfaz de usuario: Comprobar que los mensajes se muestren con los colores correctos (negro, verde, rojo).

Criterios de Entrada
•	El código fuente está disponible en el repositorio.
•	El entorno de prueba está configurado (navegador web, servidor local).

Criterios de Salida
•	Todos los casos de prueba han sido ejecutados.
•	Todos los bugs críticos han sido resueltos.
•	El juego cumple con todos los requisitos funcionales.

Herramientas
•	Navegador web (Chrome, Firefox, etc.) para pruebas manuales.
•	Herramientas de desarrollador del navegador para depuración.
•	Posiblemente Jest para pruebas unitarias de JavaScript (si se decide automatizar).

Roles y Responsabilidades
•	Tester: Ejecutar las pruebas, reportar bugs y verificar las correcciones.

Manejo de errores
•	Los errores o bugs se reportarán en un documento de seguimiento de bugs (en este caso en documento Test-Strategy en repositorio).

•	Cada error debe incluir steps to reproduce, expected result, actual result, y evidencia.

Casos de Prueba
CP01: Generación del número aleatorio
•	Descripción: Verificar que el número generado esté entre 1 y 100 y sea entero.
•	Pasos: Iniciar el juego y revisar el número generado (puede requerir depuración).
•	Resultado esperado: El número es un entero entre 1 y 100.
CP02: Entrada no entera
•	Descripción: Cuando el usuario ingresa un valor no entero, debe mostrar alerta y no contar el intento.
•	Pasos: Ingresar un valor no entero (ej. "abc", "12.5") y presionar el botón de adivinar.
•	Resultado esperado: Se muestra una alerta, y el contador de intentos no aumenta.
CP03: Entrada entera válida
•	Descripción: Cuando el usuario ingresa un entero, se procesa correctamente.
•	Pasos: Ingresar un número entero y presionar el botón.
•	Resultado esperado: El juego compara el número y muestra un mensaje (mayor o menor) o felicitaciones si adivina.
CP04: Número mayor
•	Descripción: Si el número ingresado es mayor al número a adivinar, muestra mensaje en negro: "Incorrecto! El número es mayor!".
•	Pasos: Ingresar un número mayor al número generado.
•	Resultado esperado: Mensaje en negro con el texto especificado.
CP05: Número menor
•	Descripción: Si el número ingresado es menor, muestra mensaje en negro: "Incorrecto! El número es menor!".
•	Pasos: Ingresar un número menor.
•	Resultado esperado: Mensaje en negro con el texto especificado.
CP06: Adivinanza antes de 10 intentos
•	Descripción: Si el usuario adivina antes de 10 intentos, muestra mensaje verde: "Felicitaciones! adivinaste el número!".
•	Pasos: Adivinar el número correcto en menos de 10 intentos.
•	Resultado esperado: Mensaje verde y fin del juego.
CP07: No adivinanza en 10 intentos
•	Descripción: Si después de 10 intentos no adivina, muestra mensaje rojo: "!!!Pérdistes!!!".
•	Pasos: Intentar 10 veces con números incorrectos.
•	Resultado esperado: Mensaje rojo después del décimo intento fallido.
CP08: Contador de intentos
•	Descripción: Verificar que el contador de intentos solo aumente con entradas válidas.
•	Pasos: Ingresar entradas válidas y no válidas alternadamente.
•	Resultado esperado: El contador solo aumenta con entradas válidas.
Riesgos
•	El número aleatorio puede no ser realmente aleatorio para pruebas (podría necesitarse mock).
•	La interfaz puede cambiar, afectando las pruebas automatizadas.

Errores Identificados
1. Generación incorrecta del número aleatorio
•	Línea: let randomNumber = Math.random() * 10;
•	Error: El número generado es decimal y entre 0-10, no entero entre 1-100
•	Requerimiento incumplido: El número a adivinar debe ser un entero entre 1-100
2. Número de intentos incorrecto
•	Línea: const ATTEMPS = 5;
•	Error: Solo permite 5 intentos en lugar de 10
•	Requerimiento incumplido: El juego debe permitir 10 intentos
3. Error en selector de elemento
•	Línea: const lowOrHi = document.querySelector('lowOrHi');
•	Error: Falta el punto (.) para seleccionar por clase
•	Consecuencia: El elemento no se encuentra, los mensajes de "mayor/menor" no se muestran
4. Validación de entrada faltante
•	Línea: let userGuess = guessField.value;
•	Error: No valida si la entrada es un número entero
•	Requerimiento incumplido: Debe mostrar alerta para entradas no enteras y no contar el intento
5. Comparación incorrecta
•	Error: Compara un string (userGuess) con un número (randomNumber)
•	Consecuencia: La comparación siempre falla incluso con el número correcto
6. Mensajes de resultado invertidos
•	Líneas:
o	lastResult.textContent = '!!!Pérdistes!!!'; (cuando acierta)
o	lastResult.textContent = 'Felicitaciones! adivinaste el número!'; (cuando falla)
•	Error: Los mensajes de éxito y fracaso están intercambiados
7. Colores incorrectos en los mensajes
•	Líneas:
o	lastResult.style.backgroundColor = 'black'; (debería ser verde para acierto)
o	lastResult.style.backgroundColor = 'red'; (debería ser para fracaso)
o	lastResult.style.backgroundColor = 'green'; (debería ser negro para pistas)
•	Requerimiento incumplido: Los colores no coinciden con lo especificado
8. Error de escritura en event listeners
•	Líneas:
o	guessSubmit.addeventListener('click', checkGuess);
o	resetButton.addeventListener('click', resetGame);
•	Error: Debe ser "addEventListener" (con mayúscula 'E')
9. Generación incorrecta de número en reinicio
•	Línea: randomNumber = Math.floor(Math.random()) + 1;
•	Error: Siempre genera el número 1
•	Consecuencia: Todos los juegos posteriores usarán el mismo número
10. Falta de alerta para entradas no válidas
•	Error: No hay código para mostrar alertas cuando la entrada no es un número entero
•	Requerimiento incumplido: Debe alertar al usuario sobre entradas inválidas

Conclusión
Esta estrategia de pruebas asegurará que el juego funcione según los requisitos del cliente. Los casos de prueba cubren los aspectos críticos de la funcionalidad.
