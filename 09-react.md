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

## useEffect

## Reglas

## Construir tu propio hook

Todo el código que nosotros escribamos en React debe ser: entendible, escalable y reutilizable. Es por esto que debemos intentar que nuestros componentes sean simples y claros de leer. Y aquí es donde entran los *custom hook*.

Un custom hook es una función común y corriente de JavaScript en la cual se extrae la lógica de un componente con la finalidad de hacerlo reutilizable.

Por estándar, los hooks comienzan con la palabra *use* seguido de un alias a las operaciones que se realizan en él. Por ejemplo, un custom hook que haga peticiones a un servidor, podría llamarse *useFetch*.

Tomemos el custom hook *useFetch* de ejemplo, supongamos que tenemos un componente que hace una petición a una api y muestra la información en pantalla; este componente puede lucir de esta forma: 

```JSX
    export const Component = () => {
        const [state, setState] = useState();

        useEffect(() => {
            const fetchData = () => {
                const resp = // We fetch data

                setState(resp);
            }
        }, []);

        return (
            <div>Respose: {state}</div>
        );
    }
```

Podemos extraer la lógica en nuestro custom hook, el cual luciría de esta manera:
```JSX
    // useFetch.js

    export const useFetch() {
        const [state, setState] = useState();

        useEffect(() => {
            const fetchData = () => {
                const resp = // We fetch data

                setState(resp);
            }
        }, []);

        return { state };
    }
```

Y nuestro el código de nuestro componente sería mucho más fácil de leer

```JSX
    // Component.js

    export const Component = () => {
        const {state} = useFetch();

        return (
            <div>Respose: {state}</div>
        );
    }
```

Este es un ejemplo bastante básico, sin embargo, nuestros componentes pueden retornar tantas funciones o valores como necesitemos y lo mejor, ¡Podemos usarlos en otros componentes!