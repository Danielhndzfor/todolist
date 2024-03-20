# Todo List


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