# Actividad: "hackeá" Roblox (con datos públicos)

## Qué vamos a hacer

Vamos a hacer que una página **le pregunte a Roblox** por un usuario y muestre lo que Roblox contesta. Para eso hay que escribir **un botón** y **unas líneas de JavaScript**.

No es hackear de verdad. Roblox tiene una **API**: una puerta que ellos dejan abierta para que cualquiera pida datos **públicos**, como el nombre de un usuario o cuándo se creó la cuenta. Es lo mismo que ves en el perfil de la página.

Hacker de verdad es el que **protege**. Por eso esto va con el tema de Vifina: aprendemos cómo se piden datos para después saber cómo se cuidan.

Tiempo: una clase. Pueden hacerlo de a dos.

## Reglas del juego (leelas, en serio)

- Solo pedimos datos **públicos**. No tocamos cuentas de nadie.
- **Nunca** pegues código en la consola cuando estás en `roblox.com`. Esa es la estafa más común: te dicen "pegá esto y conseguís Robux gratis" y en realidad te roban la cuenta.
- **Nunca** le des tu contraseña ni tu cookie `.ROBLOSECURITY` a nadie. Con eso se quedan con tu cuenta, aunque tengas verificación en dos pasos.

## Antes de empezar

1. Abrí el archivo `roblox/index.html` con doble clic. Se abre en el navegador.
2. Abrilo también en tu editor (VS Code o el que uses).
3. Vas a ver una terminal verde con una casilla de ID y una pantalla vacía. Todavía no hace nada: eso lo escribís vos.

---

## Paso 1: el botón

En el archivo, buscá el comentario que dice `PASO 1` y escribí abajo:

```html
<button id="boton">Hackear</button>
```

Guardá y apretá **F5** en el navegador. Tiene que aparecer el botón. Todavía no hace nada.

**Probá:** cambiá la palabra `Hackear` por otra, por ejemplo `Espiar` o `Escanear`.

## Paso 2: que el botón haga algo

Buscá el `<script>` y escribí adentro:

```js
const boton = document.getElementById('boton');
const pantalla = document.getElementById('pantalla');

boton.addEventListener('click', function () {
  pantalla.textContent = 'Escaneando...';
});
```

- `getElementById` busca una cosa de la página por su `id`.
- `addEventListener('click', ...)` significa "cuando alguien haga clic, hacé esto".
- `textContent` cambia el texto de lo que encontramos.

Guardá, apretá **F5** y hacé clic en el botón. La pantalla tiene que decir `Escaneando...`.

**Probá:** cambiá el mensaje.

## Paso 3: preguntarle a Roblox

Ahora reemplazá el bloque del botón por este. Es el paso importante:

```js
boton.addEventListener('click', async function () {
  const id = document.getElementById('idUsuario').value;
  pantalla.textContent = 'Escaneando...';

  const respuesta = await fetch('https://users.roproxy.com/v1/users/' + id);
  const usuario = await respuesta.json();

  pantalla.textContent = 'Nombre: ' + usuario.name;
});
```

- `fetch` es "andá a esta dirección y traeme lo que haya".
- `await` significa "esperá a que llegue la respuesta antes de seguir". Por eso la función tiene `async` adelante.
- `.json()` convierte la respuesta en algo que JavaScript entiende.
- `usuario.name` es el nombre. Roblox manda más datos: `displayName`, `created`, `description`, `isBanned`.

Hacé clic con el ID `1`. Tiene que aparecer `Nombre: Roblox`.

**Probá:** cambiá el ID por otros números (`2`, `3`, `156`...). Cada número es un usuario distinto.

## Paso 4: más datos

Mostrá varias líneas. El `\n` es un salto de línea:

```js
pantalla.textContent =
  'Nombre: ' + usuario.name + '\n' +
  'Nombre visible: ' + usuario.displayName + '\n' +
  'Cuenta creada: ' + usuario.created;
```

---

## Retos (elegí los que quieras)

1. **Cuenta verificada.** Mostrá si la cuenta tiene la tilde de verificada (`usuario.hasVerifiedBadge`). Usá un `if` para escribir `Sí` o `No`.
2. **Año de creación.** `usuario.created.slice(0, 4)` te da solo el año. Mostralo como `Cuenta del año 2006`.
3. **Usuario al azar.** Elegí un ID con `Math.floor(Math.random() * 1000) + 1` y escaneá ese.
4. **Modo hacker.** Mostrá cada línea con un poquito de demora, como si estuviera "hackeando" (buscá `setTimeout`).
5. **Colores.** Cambiá en el `<style>` el verde por otro color.

## Si algo sale mal

- **No pasa nada al hacer clic:** abrí la consola (**F12**, pestaña *Consola*) y fijate si hay un error en rojo. Revisá que el `id` del botón sea exactamente `boton`.
- **Sale `Cannot read properties of null`:** el nombre que le pusiste a `getElementById` no coincide con el `id` del HTML. Tienen que ser iguales.
- **Sale `undefined`:** pediste un dato que Roblox no manda, o lo escribiste mal (`Name` en vez de `name`). Se distingue mayúscula de minúscula.
- **Error con `429` o `Too Many Requests`:** pediste demasiadas veces seguidas. Esperá un minuto y probá de nuevo.
- **Error que dice `CORS` o `Failed to fetch`:** no es tu culpa. Avisale a quien da la clase: puede que el servicio que usamos haya cambiado.
- **El ID no existe:** Roblox contesta un error y `usuario.name` queda `undefined`. Probá con un ID más chico.

## Una pregunta para pensar

Roblox deja pedir datos públicos, pero **no** deja pedir tu contraseña ni tu mail. ¿Por qué creés que decidieron qué datos son públicos y cuáles no? Pensarlo es el primer paso para trabajar en seguridad.

<details>
<summary>Solución completa (para quien da la clase)</summary>

```html
<button id="boton">Hackear</button>
```

```js
const boton = document.getElementById('boton');
const pantalla = document.getElementById('pantalla');

boton.addEventListener('click', async function () {
  const id = document.getElementById('idUsuario').value;
  pantalla.textContent = 'Escaneando...';

  const respuesta = await fetch('https://users.roproxy.com/v1/users/' + id);
  const usuario = await respuesta.json();

  pantalla.textContent =
    'Nombre: ' + usuario.name + '\n' +
    'Nombre visible: ' + usuario.displayName + '\n' +
    'Cuenta creada: ' + usuario.created;
});
```

Nota: Roblox no permite pedir sus datos desde una página que no es de ellos (bloqueo CORS), por eso usamos `roproxy.com`, un espejo público que sí lo permite. Es un servicio de terceros: si deja de andar, hay que cambiar la dirección en el `fetch`.

</details>
