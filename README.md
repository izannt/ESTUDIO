# Práctica 2
# Introducción a la electrónica con el LED RGB

## Izan Nieto y Nathan Morán

### Objetivos
En esta práctica se pueden apreciar 3 objetivos diferentes:
- Entender los componentes del circuito y hacer uso del datasheet. Gracias al ejercicio 1, podemos calcular los valores y conocer los colores de las resistencias para poder hacer un uso correcto de ellas y que no haya problemas en montajes de circuitos. Por otro lado, el apartado 2 de este mismo ejercicio, nos permite aprender sobre el funcionamiento y la configuración del LED RGB de manera digital y físicamente. Además, usando el datasheet de los ledes podemos entender la relación de las resistencias con la intensidad que llega a los componentes: como cada led necesita una intensidad distinta para que brille correctamente, debemos usar las resistencias adecuadas para que se puedan apreciar los colores que emiten.
- Aprender cómo controlar la intensidad de colores. El ejercicio 2 tiene como fin combinar diferentes intensidades de los canales para que observemos cómo podemos generar colores diferentes según cada valor de estas intensidades.
- Emplear la interfaz de usuario. En el ejercicio final, implementamos funciones para habilitar, configurar y usar la comunicación serial en Arduino y, así, poder modificar programas para que el usuario pueda controlar los componentes de un circuito, en este caso, el LED RGB.

### Resumen del trabajo realizado.
En el ejercicio 1 apartado 1, hemos calculado la resistencia que se necesita para el color haciendo uso de la página LED Resistor Calculator. Esta web calcula la resistencia necesaria usando la siguiente fórmula: R = (Vs -  Vled)/ Iled
- R: resistencia a calcular.
- Vs: voltaje de la fuente (la placa arduino) en nuestro caso 5V. 
- Vled: caída de voltaje a través del led. Cada led tiene un valor diferente y usando el datasheet del led RGB: el led rojo empleando el valor mínimo, tiene un valor de 1.9V, mientras que el verde y azul de 2.9V. 
- Iled: corriente que pasa por el LED, como es constante es la misma corriente que pasa por el resistor, 8mA.

Obteniendo como resultado una resistencia de 387,5 ohmios para el color rojo, y dos resistencias de 262,5 ohmios para el color verde y azul del LED RGB. Aún así, físicamente hemos tenido que usar resistencias de valores superiores ya que no teniamos esas exactas: una resistencia de 470 ohmios para el rojo y dos resistencias de 330 ohmios para el resto de colores.

Luego, en el apartado 2 hemos añadido al código proporcionado dos cosas: el color cian (encendiendo el color verde y el azul) y, una función que recibe 1s y 0s para encender aquellos pines correspondientes. Es decir, si la función recibe un 1 (HIGH) como dato de esa variable pin, se encenderá el canal del LED atribuido a ese pin. Por el contrario, se apagará si recibe un 0 (LOW).

Respecto a lo realizado en el ejercicio 2,  tanto en el apartado 1 como en el 2, hemos implementado una función que controla el color de los leds según 3 variables. Esta recibe los datos de las variables, cuyos valores son las intensidades correspondientes a cada color del led. Según la intensidad de cada color y la combinación de estos, podemos generar diferentes colores. En nuestro caso, hemos generado estos colores: rojo, verde, azul, cian, magenta, amarillo, naranja, blanco y apagado.

Por último, en el ejercicio 3 hemos implementado funciones y condiciones relacionadas con la comunicación serial para poder controlar el LED RGB según una cadena de números introducida por el usuario en el Monitor Serie. Luego, esa cadena es manipulada para que, al llamar a la función del ejercicio anterior, se haga una lectura adecuada de los valores de las intensidades de los leds.

```C++
	Serial.begin(9600);
```
```C++	
	Serial.print();
```
```C++	
	Serial.read();
```
```C++	
	if (Serial.available() > 0) {
		String input = Serial.readStringUntil('\n');
		String led1 = input.substring(0,1);
		pin1 = led1.toInt();
	}
```

### Particularidades: Problemas encontrados, funcionalidad extra, etc.
En esta práctica la dificultad encontrada ha sido debido al LED RGB.
En un principio pensamos que se trataba de un LED con ánodo común debido al enunciado de la práctica. Por ello, intercambiamos los valores convencionales: HIGH para apagar y LOW para encender. Además, cuando montamos el circuito tuvimos en cuenta que no debíamos conectar el pin común a tierra (GND) sino a la fuente de 5V. 
Al comenzar a realizar pruebas e intentos con el programa, tuvimos errores de funcionamiento, así que intentamos ver qué pasaba si  volvíamos a cambiar los valores convencionales a  HIGH para encender y LOW para apagar. También, conectamos el pin común a tierra (GND), como si fuese un LED con cátodo común. 
Finalmente, se trataba de un LED con cátodo común y por ello si funcionaban todos los programas y el montaje con la polaridad sin invertir.

### Enlace al vídeo del funcionamiento del ejercicio.
[Ejercicio 1](https://drive.google.com/file/d/1_Xki1zHdtQLGS-2fTEsxTEoa8_AtGQ8l/view?usp=sharing)

[Ejercicio 2.1](https://drive.google.com/file/d/1pNgpyGi0CMoF1dm_hZpItOXN7pM4EMfY/view?usp=sharing)

[Ejercicio 2.2](https://drive.google.com/file/d/17yTvLtuk9TkoaHPaS7Kf8cQCJFrMyQzn/view?usp=sharing)

[Ejercicio 3](https://drive.google.com/file/d/1wPQ4ywWFBtWpIfaU7ZS2sc8_YVie-zQN/view?usp=sharing)

### Esquemático del circuito (Tinkercad).
Ejercicio 1, 2 y 3.
[Esquematico](https://drive.google.com/file/d/1vjf4Pfmb44O1rLOI-nvaM6V6K1QGA2ao/view?usp=sharing)
