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

## Estado

## useEffect

## Reglas

## Construir tu propio hook.
