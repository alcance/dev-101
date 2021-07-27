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
### ¿Qué son los Hooks?
Los Hooks son funciones que permiten conectarse a funciones incorporadas en la librería de React. Los hooks dan la posibilidad de controlar el estado así como otras características dentro de nuestra aplicación. 

* ***useState***
`useState` es el hook más común, se utiliza para mantener el estado dentro de un valor dentro de un componente (un componente puede tener varios hooks de estado). Este hook tiene la siguiente sintaxis:

```JSX
    const [state, setState] = useState('This is my initial state');
```
Podemos inicializarlo con cualquier valor y utilizarlo dentro de nuestra aplicación. Y cada vez que necesitemos cambiar su valor, llamaremos la función setState y le pasaremos como parámetro el nuevo valor.

Es importante saber que setState es una función asíncrona, por lo tanto, si necesitas inmediatamente su valor para realizar otra operación, podremos acompañarlo con useEffect.

* ***useEffect***  
`useEffect` es el segundo hook más utilizado dentro de React. Y, como se ha mencionado anteriormente, engloba las tres etapas del ciclo de vida de un componente. Este hook tiene la siguiente sintaxis:
```JSX
    useEffect(() => {
        // Desired Effect
        return () => {
            // Cleanup
        }
    }, [/* Dependency Array */]);
```
Cuando nuestro componente es montado, nuestro efecto será ejecutado; aunque, debemos tener en cuenta que los efectos secundarios no deben ejecutarse dentro del useEffect, esto puede llevar a un comportamiento extraño dentro de nuestra aplicación. Estos efectos pueden ser llamados dentro de nuestro useEffect y ser ejecutados en algún otro lugar de la aplicación.

En la sección de cleanup, deberemos cancelar todas las operaciones que hagan necesite nuestro componente. No debemos actualizar el estado, dejar `eventListeners` escuchando, operaciones asíncronas en proceso, etcétera. Cuando nuestro componente se destruya, se debe destruir todo lo que tenga relación directa a él.

Por último queda hablar sobre el arreglo de dependencias.
Dentro de este arreglo colocaremos todas las variables que queremos estar 'escuchando' y cada vez que cambie alguna de ellas, nuestro efecto será lanzado nuevamente.

Imaginemos un caso donde tengamos que hacer una petición a nuestro servidor con una url, podríamos hacerlo de la siguiente forma

```JSX
    export const Component = ({ url }) => {
        const fetchData = (url) => {
            // Do Request
        }

        useEffect(() => {
            fetchData(url);
        }, [url]);
    }
```

Y si te lo preguntas, también podemos colocar funciones dentro de nuestro arreglo, pero hay que tener cuidado, ya que, en el arreglo de dependencias estará la referencia a la función, y, al igual que los objetos, dos funciones pueden llamarse igual, realizar las mismas operaciones pero estarán ambas harán referencia a una ubicación de memoria distinta. ¿Por qué mencionamos esto? Porque, cada vez que el estado del componente cambia, las funciones también son creadas nuevamente y, por lo tanto, cambian de referencia; nuestro arreglo de dependencias nota el cambio y lanza nuevamente el efecto, y con esto, cayendo en un ciclo infinito.

Entonces, ¿cómo le hacemos para ejecutar funciones con efectos secundarios?

Hay dos principales maneras, la primera y más sencilla es mover la función dentro del mismo efecto, dejándolo de la siguiente manera:

```JSX
    export const Component = ({ url }) => {
        useEffect(() => {
            const fetchData = (url) => {
                // Do Request
            }

            fetchData(url);
        }, [url]);
    }
```

La segunda manera es memorizando la función con otro hook *useCallback()*, dejando nuestro código de la siguiente manera:

```JSX
    export const Component = ({ url }) => {
        const fetchData = useCallback((url) => {
            // Do Request
        }, [url]);

        useEffect(() => {
            fetchData();
        }, [fetchData]);
    }
```

* ***useContext***  
`useContext` nos sirve para utilizar valores que se encuentren dentro del contexto actual. Devuelven el valor proveído por el mismo contexto (*React.createContext()*). Su sintaxis es la siguiente: 
```JSX
    const context = useContext(Context);
```

* ***useReducer***  
`useReducer` brinda una alternativa a useState, se utiliza frecuentemente en combinación a el contexto de la aplicación. Es preferible usar *useReducer* cuando el estado tiene un valor complejo con múltiples subvalores.

Su sintaxis es la siguiente: 
```JSX
    const [state, dispatch] = useReducer(reducer, initialArg, init);
```

Acepta un reducer de tipo `(state, action)` y devuelve el estado actual junto con la función dispatch (la cual nos servirá para actualizar el estado de la aplicación).

Los reducers son funciones de que reciben el estado inicial y una acción a realizar; deben forzosamente regresar un estado de tipo `state` el cual puede variar (es lo que buscamos) dependiendo de la acción.

Veamos cómo luce un reducer

```JSX
    export const reducer(state, action) => {
        switch(action.type) {
            case 'logIn': 
                return {
                    ...state,
                    isLogged: true,
                    name: action.payload
                }
            case 'logout':
                return {
                    ...state,
                    isLogged: false,
                    name: null
                }
            default: 
                return state;
        }
    }
``` 

Como puedes notar, nuestro reducer sólo tiene dos operaciones, para iniciar y cerrar sesión. Y también habrás notado que estamos pasando una copia al estado, esto no es necesario en este caso, pero es recomedable hacerlo para que siempre tengamos nuestro estado completo y evitar potenciales errores.

```JSX
    export const Component = () => {
        
        const [state, dispatch] = useReducer(reducer, {
            isLogged: false,
            name: null
        });

        const { isLogged, name } = state;

        const logOut = () => {
            dispatch({
                type: 'logOut'
            });
        }

        const logIn = () => {
            dispatch({
                type: 'logIn',
                payload: 'Karla'
            });
        }

        return (
            {
                isLogged ? (
                    <>
                        <p>Welcome {name}</p>
                        <button onClick={logOut}>Log Out</button>
                    </>
                ) : (
                    <button onClick={logIn}>Log In</button>
                )
            }
        );
    }
```

* ***useCallback***  
```useCallback``` Antes de entrar a la utilidad de useCallback, es importante recalcar que, cada vez que se hace un re render en un componente, las funciones que lo componen son re creadas en un espacio de memoria distinto. Y si, este componente tiene componentes hijos que reciben esta función, aunque usen React.memo, volverán a renderizarse.

Esta es la solución de useCallback, memoriza una función para que ésta sea exactamente la misma en cada render. Su sintaxis es la siguiente

```JSX
    const memoizeFunction = useCallback((params) => {
        // Do your Job!
    }, []);
```
El arreglo de dependencias funciona prácticamente igual al de useEffect.
Pero, ¿qué pasa si queremos mandar un setState a nuestros hijos?, si nosotros hacemos usamos `useCallback` de la siguiente forma sería desaprovechar este hook, podríamos hacer que setState también use `useCallback` pero esto nos puede llevar a un *callback hell*.

```JSX
    const [state, setState] = useState();

    const memoizeFunction = useCallback((params) => {
        setState(params);
    }, [setState]);
```

Es importante saber que setState nos retorna el mismo state, por lo tanto podemos utilizar `useCallback` de esta forma y obtener las operaciones deseadas.

```JSX
    const [state, setState] = useState();

    const memoizeFunction = useCallback((params) => {
        setState(state => params);
    }, []);
```

* ***useRef***  
`useRef` Lo más común en React es forzar un nuevo renderizado cuando queremos modificar algún elemento del DOM. Sin embardo, ¿cómo podemos hacer para hacer focus a algún punto, realizar alguna animación o reproducir algún archivo?

Para este tipo de casos es para lo que existe useRef. Este hook crea una referencia a un elemento del DOM que ha sido renderizado y a través de él permite ejecutar este tipo de acciones. Prácticamente podemos acceder a un elemento con JavaScript puro y sin necesidad de colocar ID's. Es bastante útil para realizar cambios que no necesitan un nuevo renderizado.

Se usa de la siguiente manera:
```JSX
    export const Component() => {
        const ref = useRef();

        const focusInput = () => {
            ref.current.focus();
        }

        return (
            <>
                <input 
                    type="text" 
                    ref={ref}
                />
                <button onCLick={focusInput}>Focus!</button>
            </>
        );
    }
```

## Estado

## useEffect

## Reglas

## Construir tu propio hook.
