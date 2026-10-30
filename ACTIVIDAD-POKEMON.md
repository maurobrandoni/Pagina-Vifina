# Actividad: armá tu Pokédex

## Qué vamos a hacer

Una página donde **escribís el número de un Pokémon** y aparece su **nombre, su imagen y todos sus datos**: tipos, altura, peso, habilidades, descripción y estadísticas.

Los datos no están en nuestra página: los pide a **PokéAPI**, una base de datos gratis que tiene los más de mil Pokémon. A eso se le llama **API**: una puerta para que un programa pida datos a otro.

**No tenés que escribir nada.** Alcanza con copiar, pegar y probar.

Tiempo: 10 minutos para que ande, y el resto para jugar.

## Paso a paso

1. En tu carpeta del proyecto creá una carpeta nueva que se llame `pokemon`.
2. Adentro creá un archivo que se llame `index.html`.
3. Copiá **todo** el código de más abajo (el bloque entero, de `<!DOCTYPE html>` a `</html>`) y pegalo en ese archivo.
4. Guardá el archivo.
5. Abrilo con doble clic. Se abre en el navegador y tiene que aparecer **Pikachu**.

Si no querés copiar, el mismo archivo ya está hecho en `pokemon/index.html`. Abrilo directamente.

## Probá esto

- Escribí `1` y apretá **Buscar** (o la tecla **Enter**). Es Bulbasaur.
- Probá con `6`, `25`, `94`, `150`, `249`, `384`.
- Apretá **Al azar** varias veces. ¿Cuántos Pokémon nuevos te salen?
- Escribí `0` o `5000`. ¿Qué dice la página? ¿Por qué?
- Buscá el Pokémon con más **Ataque** que puedas encontrar. Compará con tus compañeros.
- Buscá uno **legendario**. ¿Cuáles de los que probaste lo son?

## El código completo

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Pokédex</title>
    <style>
      * {
        box-sizing: border-box;
      }

      body {
        margin: 0;
        padding: 24px 16px;
        background: #b3262d;
        font-family: Arial, Helvetica, sans-serif;
        color: #1c1c1c;
      }

      .pokedex {
        max-width: 520px;
        margin: 0 auto;
      }

      h1 {
        margin: 0 0 16px;
        color: #ffffff;
        font-size: 1.6rem;
        letter-spacing: 2px;
      }

      .buscador {
        display: flex;
        gap: 8px;
        margin-bottom: 16px;
      }

      input,
      button {
        font-size: 1rem;
        padding: 10px 12px;
        border: 0;
        border-radius: 6px;
      }

      input {
        flex: 1;
        min-width: 0;
      }

      button {
        background: #ffcb05;
        color: #1c1c1c;
        font-weight: bold;
        cursor: pointer;
      }

      button:hover {
        background: #ffe066;
      }

      #pantalla {
        padding: 20px;
        background: #f4f4f4;
        border-radius: 10px;
        text-align: center;
      }

      #pantalla img {
        width: 220px;
        max-width: 100%;
      }

      .numero {
        color: #777777;
        font-weight: bold;
      }

      h2 {
        margin: 4px 0 12px;
        font-size: 1.8rem;
      }

      .tipos {
        display: flex;
        justify-content: center;
        gap: 8px;
        margin-bottom: 16px;
      }

      .tipo {
        padding: 4px 14px;
        background: #3b4cca;
        color: #ffffff;
        border-radius: 20px;
        font-size: 0.9rem;
      }

      .descripcion {
        margin: 0 0 16px;
        font-style: italic;
        color: #444444;
      }

      .datos {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 8px;
        margin-bottom: 16px;
        text-align: start;
      }

      .dato {
        padding: 8px 12px;
        background: #ffffff;
        border-radius: 6px;
      }

      .dato small {
        display: block;
        color: #777777;
      }

      .stat {
        display: grid;
        grid-template-columns: 110px 36px 1fr;
        align-items: center;
        gap: 8px;
        margin-bottom: 6px;
        text-align: start;
      }

      .barra {
        height: 10px;
        background: #dddddd;
        border-radius: 5px;
        overflow: hidden;
      }

      .barra div {
        height: 100%;
        background: #4caf50;
      }
    </style>
  </head>
  <body>
    <div class="pokedex">
      <h1>POKÉDEX</h1>

      <div class="buscador">
        <input id="numero" type="number" min="1" max="1025" value="25" />
        <button id="buscar">Buscar</button>
        <button id="alAzar">Al azar</button>
      </div>

      <div id="pantalla">Escribí un número del 1 al 1025 y apretá Buscar.</div>
    </div>

    <script>
      const campoNumero = document.getElementById('numero');
      const pantalla = document.getElementById('pantalla');

      const tiposEnEspanol = {
        normal: 'Normal', fire: 'Fuego', water: 'Agua', electric: 'Eléctrico',
        grass: 'Planta', ice: 'Hielo', fighting: 'Lucha', poison: 'Veneno',
        ground: 'Tierra', flying: 'Volador', psychic: 'Psíquico', bug: 'Bicho',
        rock: 'Roca', ghost: 'Fantasma', dragon: 'Dragón', dark: 'Siniestro',
        steel: 'Acero', fairy: 'Hada',
      };

      const statsEnEspanol = {
        hp: 'PS', attack: 'Ataque', defense: 'Defensa',
        'special-attack': 'Ataque especial', 'special-defense': 'Defensa especial',
        speed: 'Velocidad',
      };

      function enEspanol(lista) {
        const texto = lista.find(function (item) {
          return item.language.name === 'es';
        });
        return texto ? texto : null;
      }

      async function buscarPokemon() {
        const numero = campoNumero.value;
        pantalla.textContent = 'Buscando...';

        const respuesta = await fetch('https://pokeapi.co/api/v2/pokemon/' + numero);
        if (!respuesta.ok) {
          pantalla.textContent = 'No encontré ningún Pokémon con el número ' + numero + '.';
          return;
        }
        const pokemon = await respuesta.json();

        const especie = await (await fetch(pokemon.species.url)).json();
        const habilidades = await Promise.all(
          pokemon.abilities.map(async function (item) {
            const habilidad = await (await fetch(item.ability.url)).json();
            const nombre = enEspanol(habilidad.names);
            return nombre ? nombre.name : item.ability.name;
          })
        );

        const nombre = enEspanol(especie.names);
        const descripcion = enEspanol(especie.flavor_text_entries);

        const tipos = pokemon.types.map(function (item) {
          return '<span class="tipo">' + tiposEnEspanol[item.type.name] + '</span>';
        });

        const stats = pokemon.stats.map(function (item) {
          const ancho = Math.min(100, (item.base_stat / 255) * 100);
          return (
            '<div class="stat">' +
            '<span>' + statsEnEspanol[item.stat.name] + '</span>' +
            '<strong>' + item.base_stat + '</strong>' +
            '<div class="barra"><div style="width:' + ancho + '%"></div></div>' +
            '</div>'
          );
        });

        pantalla.innerHTML =
          '<img src="' + pokemon.sprites.other['official-artwork'].front_default + '" alt="">' +
          '<div class="numero">N.º ' + pokemon.id + '</div>' +
          '<h2>' + (nombre ? nombre.name : pokemon.name) + '</h2>' +
          '<div class="tipos">' + tipos.join('') + '</div>' +
          '<p class="descripcion">' + (descripcion ? descripcion.flavor_text : '') + '</p>' +
          '<div class="datos">' +
          '<div class="dato"><small>Altura</small>' + pokemon.height / 10 + ' m</div>' +
          '<div class="dato"><small>Peso</small>' + pokemon.weight / 10 + ' kg</div>' +
          '<div class="dato"><small>Experiencia base</small>' + pokemon.base_experience + '</div>' +
          '<div class="dato"><small>Legendario</small>' + (especie.is_legendary ? 'Sí' : 'No') + '</div>' +
          '<div class="dato"><small>Habilidades</small>' + habilidades.join(', ') + '</div>' +
          '</div>' +
          stats.join('');
      }

      document.getElementById('buscar').addEventListener('click', buscarPokemon);

      document.getElementById('alAzar').addEventListener('click', function () {
        campoNumero.value = Math.floor(Math.random() * 1025) + 1;
        buscarPokemon();
      });

      campoNumero.addEventListener('keydown', function (evento) {
        if (evento.key === 'Enter') {
          buscarPokemon();
        }
      });

      buscarPokemon();
    </script>
  </body>
</html>
```

## Cambios chiquitos (opcionales)

Cada uno es cambiar **una cosa** y apretar **F5**.

1. **Otro Pokémon al arrancar.** Buscá `value="25"` y cambiá el 25 por otro número.
2. **Otro color de fondo.** En el bloque `body`, cambiá `background: #b3262d;` por otro color, por ejemplo `#1e3a8a` (azul) o `#14532d` (verde).
3. **Otro título.** Cambiá `POKÉDEX` por tu nombre, por ejemplo `POKÉDEX DE SOFI`.
4. **Otro color para los tipos.** En `.tipo`, cambiá `background: #3b4cca;`.
5. **Imagen más grande.** En `#pantalla img`, cambiá `width: 220px;` por `320px`.

Si algo se rompe, no pasa nada: deshacé con **Ctrl + Z** o volvé a copiar el código de arriba.

## Cómo funciona (para los que tienen curiosidad)

Todo pasa en la función `buscarPokemon`:

1. Lee el número que escribiste.
2. Le pide los datos a PokéAPI con `fetch('https://pokeapi.co/api/v2/pokemon/' + numero)`.
3. Convierte la respuesta con `.json()` para poder usarla en JavaScript.
4. Arma un poco de HTML con esos datos (`pokemon.id`, `pokemon.height`, `pokemon.types`...) y lo pone en la pantalla.

Probá esto: abrí en otra pestaña https://pokeapi.co/api/v2/pokemon/25 . Eso es **exactamente** lo que recibe tu página. Es muchísimo texto, y tu página se encarga de ordenarlo para que se vea lindo.

## Si algo sale mal

- **No aparece nada o dice "Buscando..." para siempre:** revisá que tengas internet. Probá de nuevo con **F5**.
- **La página se ve sin colores o con texto raro:** faltó copiar una parte. Volvé a copiar el bloque **entero**, de `<!DOCTYPE html>` a `</html>`.
- **Se ve el código en el navegador en vez de la página:** el archivo se guardó con otro nombre. Tiene que llamarse `index.html`, no `index.html.txt`.
- **Dice "No encontré ningún Pokémon":** probá un número del 1 al 1025.
- **Para ver el error real:** apretá **F12** y mirá la pestaña **Consola**. Si hay algo en rojo, pegáselo a ChatGPT o Gemini y pedile *"explicame este error para alguien que recién empieza"*.

## Una pregunta para pensar

Esta página nunca tuvo guardados los 1025 Pokémon. Se los pide a otro programa cada vez que apretás **Buscar**. ¿Qué otras páginas o aplicaciones que usás todos los días creés que funcionan igual?
