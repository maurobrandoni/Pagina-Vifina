# Actividad: ¡a programar en JavaScript desde la consola!

## Qué vamos a hacer

Vamos a escribir nuestras primeras líneas de código en **JavaScript**, el lenguaje que hace que las páginas web "hagan cosas". No hace falta instalar nada: usamos la **consola del navegador**.

Son 20 ejercicios cortos. Empiezan muy fáciles y suben de a poquito. Cada uno trae el código para copiar y una cosa para probar cambiando algo.

Tiempo: una o dos clases. Pueden hacerlo de a dos.

## Cómo abrir la consola

1. Abrí la página de Vifina en Chrome o Edge (puede ser en `localhost` o la que publicaron en GitHub Pages).
2. Apretá la tecla **F12**. También sirve clic derecho y **Inspeccionar**.
3. Entrá a la pestaña **Consola** (se llama *Console* si está en inglés).
4. Hacé clic en la zona de abajo, pegá el código y apretá **Enter**.

## Si algo sale mal

- **El navegador no te deja pegar** y dice algo de "no pegues código que no entiendas": escribí `allow pasting` a mano, apretá Enter, y ahora sí pegá.
- **Sale un error en rojo que dice `has already been declared`**: ya habías creado esa variable. Apretá **F5** para recargar la página y probá de nuevo. Después de recargar, hay que volver a pegar el ejercicio 3, porque los ejercicios siguientes usan lo que creaste antes.
- **Sale un error en rojo con otra cosa**: revisá que estén todos los paréntesis `( )`, las llaves `{ }` y las comillas, y que cada comilla que abrís la cerrés.
- **Las comillas tienen que ser rectas**: `'` o `"`. Si las copiás de un documento de Word o del WhatsApp pueden venir curvas y no funcionan.
- **Sale `undefined` después de tu código**: es normal, no es un error.
- **No entendés una línea**: pegásela a ChatGPT o Gemini y pedile *"explicame esta línea de JavaScript para alguien que recién empieza"*.

---

## Nivel 1: primeros pasos

### Ejercicio 1: Hola mundo

```js
alert('Hola mundo');
```

Tiene que aparecer una ventanita con el mensaje. Hacé clic en **Aceptar** para cerrarla.

**Probá:** cambiá el texto que está entre las comillas por otro mensaje.

### Ejercicio 2: escribir en la consola

```js
console.log('Estoy programando en JavaScript');
```

`console.log` escribe un mensaje en la consola, sin ventanita.

**Probá:** escribí tres `console.log` seguidos, cada uno con un mensaje distinto.

### Ejercicio 3: guardar una variable

Una **variable** es una cajita con nombre donde guardamos un dato.

```js
let nombre = 'Sofi';
console.log(nombre);
```

**Probá:** poné tu nombre en lugar de `Sofi`.

### Ejercicio 4: cambiar el valor de una variable

```js
nombre = 'Lu';
console.log(nombre);
```

Ahora no escribimos `let`, porque la cajita ya existe. Solo le cambiamos lo que tiene adentro.

**Probá:** cambiá `nombre` otra vez y mostralo.

### Ejercicio 5: juntar textos

```js
let ciudad = 'Buenos Aires';
console.log('Hola ' + nombre + ', bienvenida a ' + ciudad);
```

El signo `+` pega textos. Fijate en los espacios dentro de las comillas.

**Probá:** cambiá la ciudad y agregá una tercera frase al final.

### Ejercicio 6: números y cuentas

```js
let precio = 1500;
let cantidad = 3;
console.log(precio * cantidad);
```

Los números van **sin comillas**. Las cuentas se hacen con `+`, `-`, `*` (por) y `/` (dividido).

**Probá:** cambiá el precio y la cantidad.

### Ejercicio 7: una cuenta con varios pasos

```js
let total = precio * cantidad;
let descuento = total * 0.1;
console.log('Total: ' + total);
console.log('Con descuento: ' + (total - descuento));
```

`0.1` es el 10 %. Los paréntesis hacen que se resuelva primero la resta.

**Probá:** hacé un descuento del 25 % (`0.25`).

---

## Nivel 2: tomar decisiones

### Ejercicio 8: preguntarle algo a quien usa la página

```js
let tuNombre = prompt('¿Cómo te llamás?');
alert('Hola ' + tuNombre + ', ¡qué bueno que estés acá!');
```

`prompt` abre una ventanita con una pregunta y guarda lo que escribís.

**Probá:** hacé una segunda pregunta, por ejemplo `¿Cuál es tu comida favorita?`, y mostrala.

### Ejercicio 9: ¿puede entrar?

El `if` significa "si". El `else` significa "si no".

```js
let edad = 20;

if (edad >= 18) {
  console.log('Podés entrar');
} else {
  console.log('No podés entrar');
}
```

`>=` quiere decir "mayor o igual".

**Probá:** cambiá `edad = 20` por `edad = 15`. Para cambiarla, escribí solo `edad = 15;` y después pegá de nuevo el `if`.

### Ejercicio 10: preguntar la edad

```js
let edadIngresada = Number(prompt('¿Cuántos años tenés?'));

if (edadIngresada >= 18) {
  alert('Podés entrar al recital');
} else {
  alert('Todavía no podés entrar');
}
```

`Number(...)` convierte el texto que escribís en un número, para poder compararlo.

**Probá:** cambiá la edad mínima de 18 a 16.

### Ejercicio 11: más de dos casos

El `else if` sirve cuando hay varias opciones.

```js
let edadVisitante = Number(prompt('¿Cuántos años tenés?'));

if (edadVisitante < 13) {
  alert('Entrada infantil');
} else if (edadVisitante < 18) {
  alert('Entrada con autorización');
} else {
  alert('Entrada general');
}
```

**Probá:** agregá un caso más para las personas de 65 años o más, que tienen entrada gratis.

### Ejercicio 12: la contraseña secreta

```js
let claveSecreta = 'vifina2026';
let intento = prompt('Ingresá la contraseña');

if (intento === claveSecreta) {
  alert('Acceso concedido ✅');
} else {
  alert('Acceso denegado ❌');
}
```

`===` quiere decir "es exactamente igual". Ojo: una mayúscula de más ya cuenta como distinto.

**Probá:** escribí `Vifina2026` con mayúscula y mirá qué pasa. Después cambiá la contraseña secreta.

### Ejercicio 13: dos condiciones juntas

`&&` quiere decir **y**. `||` quiere decir **o**.

```js
let edadInvitada = 19;
let tieneEntrada = true;

if (edadInvitada >= 18 && tieneEntrada) {
  console.log('Pasá, bienvenida');
} else {
  console.log('No podés pasar');
}
```

Para entrar tienen que cumplirse **las dos** cosas.

**Probá:** poné `tieneEntrada = false;` y mirá qué cambia. Después probá cambiar `&&` por `||`.

---

## Nivel 3: listas y repeticiones

### Ejercicio 14: una lista

A una lista se le dice **array**. Va entre corchetes `[ ]`.

```js
let servicios = ['Seguridad frente a hackers', 'Protección de datos', 'Monitoreo mensual'];

console.log(servicios);
console.log(servicios[0]);
console.log(servicios.length);
```

Mostró toda la lista, el primer elemento y cuántos hay. **Se empieza a contar desde 0**: el primero es `servicios[0]`, el segundo es `servicios[1]`.

**Probá:** mostrá el último elemento. Después agregá uno con `servicios.push('Soporte técnico');` y mostrá la lista.

### Ejercicio 15: repetir con un ciclo

El `for` repite lo mismo muchas veces.

```js
for (let numero = 1; numero <= 10; numero++) {
  console.log(numero);
}
```

Dice: "arrancá en 1, repetí mientras sea 10 o menos, y sumá 1 cada vez".

**Probá:** que cuente hasta 20. Después, que muestre la tabla del 5 con `console.log('5 x ' + numero + ' = ' + 5 * numero);`.

### Ejercicio 16: recorrer una lista

```js
for (let posicion = 0; posicion < servicios.length; posicion++) {
  console.log('Servicio ' + (posicion + 1) + ': ' + servicios[posicion]);
}
```

Recorre la lista de servicios, uno por uno.

**Probá:** cargá más servicios con `push` y volvé a correr el ciclo. Mostrá todos sin cambiar el `for`.

---

## Nivel 4: funciones

Una **función** es una receta con nombre: la escribimos una vez y la usamos todas las veces que queramos.

### Ejercicio 17: tu primera función

```js
function saludar(persona) {
  console.log('Hola ' + persona + ', bienvenida a Vifina');
}

saludar('Sofi');
saludar('Lu');
```

`persona` es el dato que le pasamos a la función cada vez que la llamamos.

**Probá:** llamala con tu nombre y con el de una amiga.

### Ejercicio 18: una función que devuelve una respuesta

`return` es lo que la función "devuelve" cuando termina.

```js
function puedeEntrar(edadPersona) {
  return edadPersona >= 18;
}

console.log(puedeEntrar(20));
console.log(puedeEntrar(12));
```

Devuelve `true` (verdadero) o `false` (falso).

**Probá:** cambiá la función para que la edad mínima sea 16.

### Ejercicio 19: ¿la contraseña es segura?

```js
function claveSegura(clave) {
  if (clave.length >= 8) {
    return 'Clave segura 💪';
  } else {
    return 'Clave muy corta, usá al menos 8 caracteres';
  }
}

console.log(claveSegura('hola'));
console.log(claveSegura('MiClaveSegura2026'));
```

`clave.length` cuenta cuántos caracteres tiene el texto.

**Probá:** hacé que una clave segura necesite 12 caracteres.

### Ejercicio 20: ¡cambiar la página!

La consola también puede tocar la página que tenés abierta.

```js
document.querySelector('h1').textContent = 'Cambié el título con JavaScript';
document.querySelector('h1').style.color = 'limegreen';
```

El título grande de la página cambió de texto y de color. Es solo en tu pantalla: apretá **F5** y todo vuelve a como estaba.

**Probá:** cambiá el texto por el que quieras y el color por `hotpink`, `orange` o `dodgerblue`.

---

## Desafío final

Armen un **control de acceso** para Vifina, con todo lo que aprendieron:

1. Que pregunte la contraseña con `prompt`.
2. Que use la función `claveSegura(...)` para decir si la contraseña es segura.
3. Que muestre el resultado con `alert`.

Intenten hacerlo solas. Si se traban, abran la pista.

<details>
<summary>Ver la pista</summary>

```js
let claveNueva = prompt('Elegí una contraseña nueva');
alert(claveSegura(claveNueva));
```

Después pueden sumarle lo que quieran: preguntar la edad, mostrar un saludo, o cambiar el título de la página con lo que aprendieron en el ejercicio 20.

</details>

## Para cerrar

Contesten en grupo, con sus palabras:

1. ¿Qué es una variable y para qué sirve?
2. ¿Qué diferencia hay entre `=` y `===`?
3. ¿Para qué sirven el `if` y el `for`?
4. ¿Cuál fue el ejercicio que más les gustó? ¿Cuál se les hizo más difícil?
5. ¿Qué les gustaría que hiciera su página de Vifina con JavaScript?
