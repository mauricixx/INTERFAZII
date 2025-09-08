# INTERFAZ II

##### Ejercicio n° 1: "Hola Mundo!" en Arduino.

```js
void setup() {
  Serial.begin(9600); // Inicia la comunicación serie a 9600 bps
  Serial.println("Hola, Mundo!"); // Envía "Hola, Mundo!" al monitor serie
}

void loop() {
  // No es necesario poner nada en el loop para este ejemplo
}
```

##### Ejercicio n° 2: LED Intermitente (Blink)
```js
void setup() {  // Configuración inicial (ej: pines como entrada/salida)
  pinMode(13, OUTPUT);  // Pin 13 como salida
}

void loop() {   // Se repite infinitamente
  digitalWrite(13, HIGH);  // Encender LED
  delay(1000);             // Esperar 1 segundo
  digitalWrite(13, LOW);   // Apagar LED
  delay(1000);             // Esperar 1 segundo
}
```
<img src="https://raw.githubusercontent.com/mauricixx/INTERFAZII/refs/heads/main/img/LedParpadeante.png"/>


##### Ejercicio n° 3: Control por Pulsador
Objetivo: Encender un LED solo al presionar un botón. Circuito: Pulsador en pin 2 (con resistencia pull-down de 10k Ω). LED en pin 13.
```js
void setup() {
  pinMode(2, INPUT);  // Botón como entrada
  pinMode(13, OUTPUT);
}
void loop() {
  if (digitalRead(2) == HIGH) {  // Si se presiona el botón
    digitalWrite(13, HIGH);
  } else {
    digitalWrite(13, LOW);
  }
}
```

##### Ejercicio n° 4: LED con Potenciómetro
Objetivo: Regular brillo de un LED con un potenciómetro. Circuito: Potenciómetro: Patas extremas a +5V y GND, central a pin A0. LED en pin 9 (con resistencia 220 Ω).
```js
void setup() {
  pinMode(9, OUTPUT);  // Pin PWM (símbolo ~)
}
void loop() {
  int valor = analogRead(A0);           // Leer potenciómetro (0-1023)
  int brillo = map(valor, 0, 1023, 0, 255);  // Convertir a rango PWM
  analogWrite(9, brillo);               // Ajustar brillo
}
```



##### Ejercicio n° 2: Semáforo en Arduino.

```js
// C++ code - Semáforo Autos y Peatones

// Definición de pines
int LED_1 = 6;  // Luz roja autos
int LED_2 = 7;  // Luz amarilla autos
int LED_3 = 8;  // Luz verde autos
int LED_4 = 9;  // Luz verde peatones
int LED_5 = 10; // Luz roja peatones

void setup() {
  // Configuramos todos los pines como salida
  pinMode(LED_1, OUTPUT);
  pinMode(LED_2, OUTPUT);
  pinMode(LED_3, OUTPUT);
  pinMode(LED_4, OUTPUT);
  pinMode(LED_5, OUTPUT);
}

void loop() {
  // 🚦 Fase 1: Autos en verde, peatones en rojo
  digitalWrite(LED_1, LOW);   // Rojo autos apagado
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado
  digitalWrite(LED_3, HIGH);  // Verde autos encendido
  digitalWrite(LED_4, LOW);   // Verde peatones apagado
  digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  delay(5000); // 5 segundos

  // 🚦 Fase 2: Amarillo autos, peatones siguen en rojo
  digitalWrite(LED_3, LOW);   // Verde autos apagado
  digitalWrite(LED_2, HIGH);  // Amarillo autos encendido
  delay(2000); // 2 segundos
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado

  // 🚦 Fase 3: Rojo autos, verde peatones
  digitalWrite(LED_1, HIGH);  // Rojo autos encendido
  digitalWrite(LED_5, LOW);   // Rojo peatones apagado
  digitalWrite(LED_4, HIGH);  // Verde peatones encendido
  delay(5000); // 5 segundos

  // 🚦 Fase 4: Rojo autos, rojo peatones (tiempo intermedio)
  digitalWrite(LED_4, LOW);   // Verde peatones apagado
  digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  delay(2000); // 2 segundos
}
```
<img src="https://raw.githubusercontent.com/mauricixx/INTERFAZII/refs/heads/main/img/semaforo.png"/>

### Estructuras de control en Arduino:
Es el conjunto de herramientas del lenguaje de programación que permiten organizar la lógica de un programa, ya sea repitiendo instrucciones (ciclos) o tomando decisiones (condicionales), con el fin de controlar dispositivos electrónicos de manera eficiente y adaptable.
En Arduino (C/C++) se usan estructuras de control como for, if, else if y else para repetir instrucciones y tomar decisiones. 

##### 1. For
Sirve para repetir un bloque de código un número determinado de veces.
##### Estructura:
```js
for (inicialización; condición; incremento) {
  // código que se repite
}
```
##### Ejemplo:
```js
for (int i = 0; i < 5; i++) {
  Serial.println(i);  // imprime 0,1,2,3,4
}
```
	•	int i = 0; → la variable empieza en 0
	•	i < 5; → se repite mientras i sea menor a 5
	•	i++ → aumenta de 1 en cada vuelta

##### A. se ejecuta una vez al iniciar la placa y se define en el setup():
 ```js
void setup() {
  Serial.begin(9600);   // Inicia la comunicación serial

  for (int i = 0; i < 5; i++) {
    Serial.println(i);  // imprime 0,1,2,3,4
  }
}

void loop() {
  // vacío porque no necesitamos repetir
}
```
##### B. Se ejecua cada vez en bucle y se define en el loop():
```js
void setup() {
  Serial.begin(9600);   // Inicia la comunicación serial
}

void loop() {
  for (int i = 0; i < 5; i++) {
    Serial.println(i);  // imprime 0,1,2,3,4
    delay(500);         // medio segundo entre cada número
  }
}
```

##### 2. if, else if, else:
Se usan para tomar decisiones.

##### Estructura:
```js
if (condición1) {
  // si condición1 es verdadera
} else if (condición2) {
  // si condición1 es falsa, pero condición2 es verdadera
} else {
  // si ninguna condición es verdadera
}
```
##### Ejemplo con un sensor:
```js
int valor = analogRead(A0);

if (valor < 200) {
  Serial.println("Muy bajo");
} else if (valor < 500) {
  Serial.println("Medio");
} else {
  Serial.println("Alto");
}
```
##### código completo:
```js
int valor;  // aquí guardaremos la lectura del sensor

void setup() {
  Serial.begin(9600);   // Inicia la comunicación serial
}

void loop() {
  valor = analogRead(A0);   // lee el pin analógico A0

  if (valor < 200) {
    Serial.println("Muy bajo");
  } else if (valor < 500) {
    Serial.println("Medio");
  } else {
    Serial.println("Alto");
  }

  delay(500); // medio segundo entre lecturas
}
```
##### Donde va cada cosa:
	•	setup() → se ejecuta una sola vez al iniciar la placa. Aquí ponemos Serial.begin(9600); para abrir la comunicación con el PC.
	•	loop() → se ejecuta infinitamente. Aquí ponemos el analogRead() y el if/else if/else.

 Este ejemplo lo puedes probar aunque no tengas sensor:
si en lugar de analogRead(A0) escribes un número (por ejemplo valor = 350;), vas a ver cómo cambia lo que imprime el if/else.


##### 3. Combinar for con if/else
Puedes usar ambas estructuras juntas. Por ejemplo, encender LEDs de forma secuencial con condiciones:
```js
int leds[] = {2, 3, 4, 5}; // Creamos un arreglo con los pines donde van conectados los LEDs

void setup() {
  // Esta función corre solo una vez al iniciar Arduino
  for (int i = 0; i < 4; i++) {         // Recorre el arreglo desde i = 0 hasta i = 3
    pinMode(leds[i], OUTPUT);           // Configura cada pin del arreglo como salida (para controlar LEDs)
  }
}

void loop() {
  // Esta función corre en bucle infinito
  for (int i = 0; i < 4; i++) {         // Recorre los 4 LEDs, uno por uno
    if (i % 2 == 0) {                   // Si el índice es par (0, 2)...
      digitalWrite(leds[i], HIGH);      // Enciende el LED correspondiente
    } else {                            // Si el índice es impar (1, 3)...
      digitalWrite(leds[i], LOW);       // Apaga el LED correspondiente
    }
    delay(500);                         // Espera 0,5 segundos antes de pasar al siguiente
  }
}
```

##### Resumen de lo que hace el código
	1.	Define 4 LEDs conectados a los pines 2, 3, 4 y 5.
	2.	En setup() configura esos pines como salidas.
	3.	En loop(), recorre los LEDs uno por uno con for.
	•	Si la posición es par → enciende el LED.
	•	Si la posición es impar → apaga el LED.
	4.	Espera 0,5 segundos y sigue al siguiente LED.
	5.	Al terminar, vuelve a empezar infinitamente.

 ##### ¿Qué hace el módulo %?
 Devuelve el resto de una división entera.
Es decir, divide dos números y se queda con lo que sobra.

##### Ejemplo:
```js
5 % 2 = 1   // 5 dividido entre 2 es 2, sobra 1
6 % 2 = 0   // 6 dividido entre 2 es 3 exacto, sobra 0
7 % 3 = 1   // 7 dividido entre 3 es 2, sobra 1
10 % 4 = 2  // 10 dividido entre 4 es 2, sobra 2
```
###### ¿Cómo se usa en el código?:
esta linea:
```js
if (i % 2 == 0) {
```
	•	Aquí se pregunta si el resto de dividir i entre 2 es igual a 0.
	•	Eso significa que i es par (0, 2, 4, …).
	•	Si no es 0, entonces i es impar (1, 3, 5, …).

 En tu ejemplo, el % sirve para decidir si el LED que toca en ese momento es par (lo enciende) o impar (lo apaga).






