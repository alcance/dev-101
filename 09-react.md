# React

## JSX
Es una extensión de la sintaxis de JavaScript. Se usa con React para describir describir cómo debe ser la interfaz de usuario.

JSX puede parecer simple HTML, pero viene con todo el poder de JavaScript. En React, JSX es usado para producer 'elementos' de React.

### ¿Por qué JSX?
En React, la lógica de renderizado está relacionado a la lógica de interfaz del usuario: cómo se manejan los eventos, cómo cambia el estado con el tiempo y cómo se preparan los datos para su visualización.

En lugar de separar el maquetado y la lógica en archivos independientes, React [separa intereses](http://www.limni.net) en *componentes*, los cuales contienen tanto el maquetado como la lógica.

Es importante saber que, en React, no es forzoso el uso de JSX, pero hace el código más legible y visual. Esto también permite a React mostrar errores y/o warnings más útiles.

### Insertando expresiones en un JSX
Imaginemos que queremos cambiar el contenido de una etiqueta `<p></p>` a *Karla*

SI estuviéramos en JavaScript puro, (o VainillaJS), tendríamos que hacer algo similar a esto:

**HTML**
```HTML
    <p id="p"></p>
```
**JavaScript**
```JS
    const p = document.getElementById('p');
    p.textContent = 'Karla';
```
Si bien, el código es bastante corto, tenemos que tener en cuenta que esto podría estar en archivos separados. Y también podríamos tener que ver constantemente el HTML para saber dónde está la etiqueta `<p></p>`, qué id tiene y a qué hace referencia dentro de nuestra página (y esto si no hay nada más que necesitemos). 

Como puedes imaginar, estas tres líneas de código, pueden requerir más trabajo del que de le debe dedicar a una simple etiqueta `<p></p>`. Ahora imagina una página completa.

Ahora, si estuviéramos en React, esto se puede hacer de una manera mucho más simple, el código para hacer generar este mismo HTML sería similar a este

```JSX
    export const P = () => {
        const name = 'Karla';

        return (
            <p>{name}<p/>
        );
    }
```

Nuestro código es un poco más largo y menos intuitivo, sí. Pero se entiende perfectamente qué es lo que hace. Es un componente (más adelante veremos a profundidad el tema de los componentes) que genera una etiqueta <p></p> que tiene el contenido de nuestra variable `name`.

Ahora imaginemos que queremos cambiar el contenido de esta etiqueta a Carlos al hacer click en un botón. En JavaScript puro, tendríamos que renderizar el botón, colocarle un id, agregarle un `eventListener` y llamar una función que cambie el varlo.

En React, esto es mucho más sencillo y el código se entiende con mayor facilidad. Sería algo similar a: 

```JSX
    const P = () => {
        const [name, setName] = useState('Karla');

        const changeNameToCarlos = () => {
            setName('Carlos');
        }

        return (
            <div>
                <p>{name}</p>
                <button onClick={changeNameToCarlos}>Change!</button>
            </div>
        )
    }
```

Hay elementos aquí que no serán vistos más adelante, sin embargo, el código es bastante comprensible por sí mismo.


### JSX También es una expresión
Después de compilarse, las expresiones JSX se convierten en llamadas a funciones JavaScript regulares y se evalúan en objetos JavaScript.

Esto significa que puedes usar JSX dentro de declaraciones if y bucles for, asignarlo a variables, aceptarlo como argumento, y retornarlo desde dentro de funciones:

```JSX
    function getGreeting(user) {
        if (user) {
            return <h1>Hello, {user}!</h1>;
        }
        return <h1>Hello, Stranger.</h1>;
}

```

**Importante**: Para especificar atributos a nuestras etiquetas, por ejemplo class, src, tab-index, etc. En JSX se utiliza nomenclatura *camelCase*, esto debido a que JSX es más parecido a JS que a HTML, y, como sabemos. En JS no se pueden declarar variables de esta forma `let variable-name;` asimismo, JS también cuenta con palabras reservadas como `class` que no deben ser utilizadas para otro propósito.

### Hijos en JSX
Al igual que en `xml`, si una etiqueta no tiene hijos, puede **autocerrarse**, por ejemplo:
```HTML
    <p />
    <div />

    O, en caso de que tenga hijos
    
    <div>
        <p>I'm a children of div</p>
    </div>
```

## Componentes

## Ciclo de vida de componentes

## Props

## React Hooks

## Estado

## PropTypes
Conforme un componente crece de tamaño, se puede caer en errores al momento de usarlo. Puede que entre sus props, necesite algún atributo que sea *string* y se pase uno de tipo *number*, o que algún prop requerido sea omitido al punto de usarlo. Esto claramente conduce a errores durante el desarrollo.

Una manera de solucionarlos es con TypeScript, sin embargo, React proporciona habilidades de verificación. 

Imaginemos que tenemos un componente que recibe un número y lo muestra en pantalla, y al hacer click en un botón, su valor se duplica

```JSX
    import { useState } from 'React';

    export const Component = ({ number }) => {

        const [state, setState] = useState(number);

        const doubleValue = () => {
            setState(state + state);
        }

        return (
            <div>
                <p>Current value: {state} </p>
                <button onClick={doubleValue}>Double it!</button>
            </div>
        );
    }
```

Ahora supongamos que nuestro componente es utilizado de la siguiente forma:

```JSX
    <Component number="1" />
```

Esto causaría un efecto inesperado, y es que, cada vez que el botón sea presionado, nuestro estado será concatenado a sí mismo, causando que sus valores sean

Número de Vuelta | Valor del Estado
| :---: | :---: |
1 | "1"
2 | "11"
3 | "1111"
4 | "11111111"
5 | "1111111111111111"

¡Y podría ser peor! ¿Y si nos mandaran una función? ¿O un objeto? Nuestra aplicación se rompería.

Para esto podemos usar los PropTypes y especificar desde un inicio qué tipo de valor está esperando nuestro componente de la siguiente forma:

```JSX
    import PropTypes from 'prop-types';
    import { useState } from 'React';

    export const Component = ({ number }) => {

        const [state, setState] = useState(number);

        const doubleValue = () => {
            setState(state + state);
        }

        return (
            <div>
                <p>Current value: {state} </p>
                <button onClick={doubleValue}>Double it!</button>
            </div>
        );
    }

    Component.propTypes = {
        number: PropTypes.number.isRequired
    }
```

Con esto especificamos que forzosamente necesitamos que el prop **number** sea de tipo number.

Los PropTypes no son sólo para verificar números, también podemos comprobar: arreglos, booleanos, funciones, objectos string y symbols. 

En este [enlace](https://es.reactjs.org/docs/typechecking-with-proptypes.html) podrás revisar el alcance que tienen los PropTypes para tipar nuestros componentes.

## Reglas

## Construir tu propio hook.
