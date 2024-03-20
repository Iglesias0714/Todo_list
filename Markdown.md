# Explicación del código 

 # Evita que el formulario se envíe y recargue la página
```
function handleSubmit(e) {
    e.preventDefault();
```

  # Obtiene el valor del input con el id 'todoAdd'
```
    let todo = document.getElementById('todoAdd').value;
```

 # Crea un nuevo objeto 'newTodo' con un id único, el texto del input y la tarea sin completar
```
    const newTodo = {
        id: new Date().getTime(), Se utiliza el tiempo actual como id único
        text: todo.trim(), #Elimina los espacios en blanco al principio y al final del texto
        completed: false, Indica que la tarea está sin completar
    };
```
"
    # Verifica si el texto de la nueva tarea no está vacío
 ```
    if (newTodo.text.length > 0 ) {
      Agrega la nueva tarea al arreglo de tareas utilizando el spread operator y concat
        setTodos([...todos].concat(newTodo));
    } else {
       Si el texto está vacío, muestra una alerta para ingresar una tarea válida
        alert("Enter Valid Task");
    }
 ```
   #Limpia el valor del input 'todoAdd'
 ```
    document.getElementById('todoAdd').value = "";
}
 ```
