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

En palabras simples, un componente es una parte de tu aplicación independiente y reutilizable. 

### **¿Por qué usar componentes?**

Imaginemos una página web muy básica, en la que tienes una barra de navegación, esta contiene un menu que lleva a los usuarios a navegar por todo tu sitio web (Inicio, Sobre nosotros, Contacto, etc.), Inicias escribiendo tu código para la página de Inicio, escribes un encabezado, todo el contenido para darle la bienvenida al usuario y un pié de página para darle información adicional al visitante, una vez terminas vas con otra sección de tu sitio, copias y pegas el código del encabezado y del pié de página, escribes toda la información sobre tí o tu negocio y así repites para todas tus demás páginas, y sin duda, esto te funcionará perfectamente.

Pero... eso de estar copiando y pegando codigo repetido no es algo que se le da muy bien a un buen desarrollador, es más, imagina que tienes que hacer un cambio en el encabezado de todas tus secciones, te tomaría tiempo y trabajo que puedes usar para avanzar en otras partes importantes de tu código, pero que si te dijera que puedes escribir o modificar tu codigo una sola vez y afectar a todas tus demás páginas? , y aquí es donde vienen al rescate los componentes de React, que no es más que un trozo de código (por ejemplo puede ser tu encabezado o tu píe de página) que se encarga de evitar tu código repetido, hacer una única función y hacerla muy bien.

En React existen dos tipos de componentes: 

- Componentes de clase. 
- Componentes funcionales.

En esta guía nos centraremos en los **componentes funcionales**  ya que son los más nuevos propuestos por React.

### **Componentes funcionales:**

Un componente funcional como lo dice su nombre **Es una función en Javascript** y luce de la siguiente manera:

### **Funcion normal**
```JS
    function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
    }

    export default Welcome
```

### **Funcion de flecha**
```JS
    const Welcome = (props) => {
        return <h1>Hello, {props.name}</h1>;
    }

    export default Welcome
```


Hay algo **importante** que debes notar en este componente, y es que su nombre debe de iniciar con mayuscula para que React lo reconozca como componente, además es importante exportalo para poder usarlo en otro componente.

También notarás que nuestro componente esta recibiendo **props** como parametro, y los **props** no son más que variables que otro componente nos esta enviando, pero esto lo veremos más a fondo en un próximo capitulo.

### **Llamar a un componente desde otro**

Ahora que ya tienes tu componente creado, ya puedes utilizarlo desde otro componente llamandolo de la siguiente manera:

```JS
    /* /components/Welcome es la ruta en donde se encuentra tu componente creado*/

    import Welcome from '/components/Welcome'

    <Welcome />
```

Listo de esa forma ya puedes usar tu componente Welcome en donde quieras, y lo mejor de todo es que si haces un cambio en el componente se verá reflejado en todos los lugares en donde lo estes usando.

Recuerda que un componente no tiene porque ser tan simple como el ejemplo, puedes agregar toda la lógica que necesites dentro de el, al igual que todo el contenido en JSX que desees.

## Ciclo de vida de componentes
Un componente puede pasar por diversas etapas a lo largo de su existencia. Estas etapas se dividen en tres, que corresponden al momento en el que el componente es: montado, actualizado y desmontado.

En versiones anteriores e React, estos tres ciclos se podían encontrar con las siguientes funciones:

```JSX
    componentDidMount();
    componentDidUpdate();
    componentWillUnmount();
```

**componentDidMount()** Es usado para hacer operaciones cuando el componente es montado o creado. Y permite llevar a cabo efectos secundarios cuando el componente se monta (Una petición a un servidor, por ejemplo)

**componentDidUpdate(prevProps)** Se ejecuta cada vez que cambia el estado dentro de nuestra aplicación, también permite ejecutar operaciones con efectos secundarios.

**componentWillUnmount();** Se llamará cada vez que el componente vaya a ser desmontado, es de mucha utilidad para hacer limpieza. Un caso muy útil es cuando un componente que utiliza algún `eventListener` es creado y eliminado varias veces. No queremos tener múltiples `evetListener` haciendo lo mismo o peor, cosas que ya no necesitamos. También es muy útil para cancelar operaciones asíncronas. !Evita las fugas de memoria!

Los tres métodos mencionados anteriormente son para Class Componentes o componentes basados en clases. Pero, a partir de la versión 16.8 de React, contamos con los hooks, los cuales nos permiten controlar el estado de la aplicación de forma más sencilla. 

Entre los hooks disponibles, el que cubre los tres métodos anteriormente es el hook de efecto `useEffect`

**Montado**
```JSX
    useEffect(() => {
        console.log('This will be executed when the component is created. What about calling our server?');
        return () => {
            console.log('This will be executed when your component is destroyed. What about cancelling asynchronous operations?');
        }
    }, [dependencyArray]); // Will re execute your effect every time a variable of your dependency array change
```

Más adelante, iremos a fondo sobre este hook. Hay cosas que debemos evitar o seguir para mantener las buenas prácticas.

## Props

### **¿Que son los props?** 

Los props no son más que variables que puedes enviar desde un componente padre a un componente hijo.

Estos props pueden contener cualquier tipo:

- Texto
- Numero
- Arreglos
- Booleanos
- Objetos 

Veamos un ejemplo de como puede un componente padre puede enviar props a su componente hijo.

#### **Componente padre**

```JS
    import Hijo from './Hijo'

    const Padre = () => {
        return (
            <Hijo 
                name = "Alexander"
                age = {23}
                favoriteColors = {["Blue", "Green", "Purple"]}
                familyNames = {{
                    father: "Mike",
                    mother: "Rose",
                    sister: "Emily"
                }}
            />
        )
    }

    export default Padre
```

Veamos a profundidad que esta pasando en el componente padre:

Antes que nada importamos el componente hijo `import Hijo from './Hijo'` al que le enviaremos los props desde el padre, recuerda que **'./Hijo'** es la ruta en donde esta creado el componente.

Si quisieramos usar el componente hijo dentro del componente padre, simplemente lo usaríamos de esta forma: `<Hijo />` pero como nuestra intención en este ejemplo es pasarle props notaremos que tiene algunas cosas adicionales que no son nada más que nombres de variables (name, age, favoriteColors, familyNames) con sus respectivos valores.

Hay algo muy importante en cada props que queremos enviar, y es que, todas estan encerradas entre **{ }** ( menos **name** que contiene un string ) y esto es para decirle a JSX que ese contenido lo debe de interpretar como JavaScript nativo y no como una cadena de texto. te estarás preguntando que pasa con las dobles {} en **familyNames** y la respuesta es simple:  
Las llaves externas son las que usará JSX y las segundas es porque estas enviando un objeto de Javascript y un objeto se representa con {}.

Ahora vamos a ver como recibir esas props en el componente hijo:

#### **Componente hijo**

```JS
const Hijo = (props) => {
    console.log(props);
    return (
        <div>
            <h1>Welcome {props.name}</h1>
        </div>
    )
}

export default Hijo
```

Como puedes ver se recibe como parametro **props** que no es más que un objeto con todas las propiedades que esta enviando el componente padre, dejamos `console.log(props)` intencionalmente para que puedas ver lo que trae:

#### **Respuesta del console log**
```JS
{
    age: 23
    familyNames:{
        father: "Mike"
        mother: "Rose"
        sister: "Emily"
    }
    favoriteColors:[
        "Blue"
        "Green"
        "Purple"
    ]
    name: "Alexander"
}
```

Y como es solo un objeto de JavaScript puedes acceder a sus propiedades:
`<h1>Hijo to props {props.name}</h1>` o bien puedes usar destructuring de Javascript para ahorrarte un poco de código:

#### **Componente hijo destructuring props**

```JS
const Hijo = ({name, age}) => {
    return (
        <div>
            <h1>Welcome {name}, your age is {age}</h1>
        </div>
    )
}
```

Ahora imaginemos que estamos esperando recibir el valor de **lastname** en las props que serán enviadas por el componente padre y tu app realiza algunas acciones importantes con ese valor, adivina que pasará...? si, tu app volará en mil pedazos, pero tranquilx React y sus props tienen la solución para esto: **Props con valor por defecto** y se usan de esta forma:

```JS
const Hijo = ({name, age, lastname = "Mike"} ) => {
    return (
        <div>
            <h1>Welcome {name} {lastname}, your age is {age}</h1>
        </div>
    )
}
```

Y ahora sí, tu app seguirá funcionando aunque el padre no envie esa props.




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