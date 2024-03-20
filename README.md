# Todo List
Es una lista de tareas, también conocida como lista de pendientes o lista de quehaceres. Es una herramienta comúnmente utilizada para organizar y administrar las tareas que una persona necesita realizar. En un "Todo List", cada tarea se enumera en forma de lista, y generalmente se pueden agregar, eliminar, marcar como completadas o editar las tareas según las necesidades del usuario. Estas listas son útiles para ayudar a las personas a mantenerse organizadas y productivas, ya sea en el ámbito personal o profesional.

### En esta parte del código es lo que nos permite subir el elemento a todolist
Es el encargado de manejar el envío de un nuevo elemento a la lista todolist. Cunado el usuario envía el formulario se ejecuta la funcion llamadad handleSubmit. 
###### Al ejecutarse esta función primero evita que la pagina recarge cada que se agregue un elemento.
###### Segundo obtiene el valor del elemento, es decir, del input que se muestra en la web.
###### Tercero se crea como objeto en la lista utilizando el newTodo.
###### Cuarto se verifica la longitud del texto de la nueva tarea, permite no mandar un input vacio.
###### Quinto se limpia el contenido del elemento de entrada para que este listo para recibir otra.
 ```js
    function handleSubmit(e) {
        e.preventDefault();
        let todo = document.getElementById('todoAdd').value
        const newTodo = {
            id: new Date().getTime(),
            text: todo.trim(),
            completed: false,
        };
        if (newTodo.text.length > 0) {
            setTodos([...todos].concat(newTodo));
        } else {
            alert("Enter Valid Task");
        }
    document.getElementById('todoAdd').value = ""
    }
```

### En esta parte del código es donde nos permite eliminar el elemento de la lista
Es responsable de eliminar el elemento de la lista todolist. Lo realiza obteniendo el id del elemento que se desea eliminar.
##### Primero la función al aplicarse obtiene el id del elemento que quiere eliminar.
##### Segundo se crea una nueva lista llamada updatedTodos, que seria la tarea actualizada. Lo que aplica es recorrer cada elemento de la lista y asi devolver solo aquellos elementos que no sean igual al id obtenido.
##### Tercero una vez se ha generado la nueva lista, se debe actualizar la lista todolist, para ello utilizamos el setTodos que reemplaza la lista de tareas actual con la lista actualizada.
```js
    function deleteTodo(id) {
        let updatedTodos = [...todos].filter((todo) => todo.id !== id);
        setTodos(updatedTodos);
    }
```

### En esta parte del código es donde nos permite alternar el estado completado de un elemento en la lista
Es responsable de alternar el estado completado de un elemento en la lista todolist. Lo hace obteniendo el id del elemento cuyo estado se desea alternar.
##### Primero, la función al aplicarse obtiene el id del elemento cuyo estado se desea alternar.
##### Segundo, se crea una nueva lista llamada updatedTodos, que sería la lista de tareas actualizada. Lo que hace es recorrer cada elemento de la lista y verificar si el id del elemento coincide con el id obtenido. Si es así, se invierte el estado completado del elemento.
##### Tercero, una vez se ha generado la nueva lista, se debe actualizar la lista todolist. Para ello, utilizamos setTodos, que reemplaza la lista de tareas actual con la lista actualizada.
```js
    function toggleComplete(id) {
        let updatedTodos = [...todos].map((todo) => {
        if (todo.id === id) {
            todo.completed = !todo.completed;
        }
        return todo;
        });
        setTodos(updatedTodos);
    }
```

### En esta parte del código es donde nos permite enviar las ediciones realizadas en un elemento de la lista
Es responsable de enviar las ediciones realizadas en un elemento de la lista todolist. Recibe como argumento el objeto newtodo, que contiene la información actualizada del elemento.
##### Primero, la función submitEdits se aplica para enviar las ediciones realizadas en un elemento de la lista todolist.
##### Segundo, se crea una nueva lista llamada updatedTodos, que sería la lista de tareas actualizada. Lo que hace es recorrer cada elemento de la lista y verificar si el id del elemento coincide con el id del objeto newtodo. Si es así, actualiza el texto del elemento con el valor del input correspondiente.
##### Tercero, una vez se ha generado la nueva lista, se debe actualizar la lista todolist. Para ello, utilizamos setTodos, que reemplaza la lista de tareas actual con la lista actualizada.
##### Cuarto, se establece setTodoEditing(null) para limpiar cualquier estado de edición que pueda estar activo.
```js
    function submitEdits(newtodo) {
        const updatedTodos = [...todos].map((todo) => {
        if (todo.id === newtodo.id) {
            todo.text = document.getElementById(newtodo.id).value;
        }
        return todo;
        });
    setTodos(updatedTodos);
    setTodoEditing(null);
    }
```

### En esta parte del código es donde se gestiona el almacenamiento local de la lista de tareas
Es responsable de gestionar el almacenamiento local de la lista de tareas. Utiliza el localStorage del navegador para guardar y cargar la lista de tareas.
##### El primer useEffect se ejecuta solo una vez al cargar el componente. Este efecto carga los datos de la lista de tareas desde el localStorage.
##### Si hay datos guardados en el localStorage, se establecen como el estado inicial de la lista de tareas utilizando setTodos.
##### El segundo useEffect se ejecuta cada vez que la lista de tareas cambia.
##### Si la lista de tareas tiene elementos, se convierte en formato JSON y se guarda en el localStorage con la clave "todos".
```js
    useEffect(() => {
        const json = localStorage.getItem("todos");
        const loadedTodos = JSON.parse(json);
        if (loadedTodos) {
            setTodos(loadedTodos);
        }
    }, []);
    useEffect(() => {
        if (todos.length > 0) {
            const json = JSON.stringify(todos);
            localStorage.setItem("todos", json);
        }
    }, [todos]);
```

### Conclusión
El código que hemos revisado es una aplicación de "Todo List" desarrollada con JavaScript y React. Este programa permite agregar, editar, eliminar y marcar como completadas las tareas de una lista. Cada función cumple un rol importante para la interacción del usuario, desde la validación de formularios hasta el almacenamiento local de datos para mantener la información entre sesiones. La aplicación ofrece una experiencia fluida y personalizada, facilitando la organización y gestión de tareas de manera eficiente. En conclusión, este "Todo List" es una herramienta valiosa para mantenerse organizado y productivo en las actividades diarias.