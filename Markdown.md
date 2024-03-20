# Explicación del código 
============================================================================================
- Evita que el formulario se envíe y recargue la página
 ```
function handleSubmit(e) {
    e.preventDefault();
```

- Obtiene el valor del input con el id 'todoAdd'
 ```
    let todo = document.getElementById('todoAdd').value;
```

- Crea un nuevo objeto 'newTodo' con un id único, el texto del input y la tarea sin completar
 ```
    const newTodo = {
        id: new Date().getTime(), Se utiliza el tiempo actual como id único
        text: todo.trim(), #Elimina los espacios en blanco al principio y al final del texto
        completed: false, Indica que la tarea está sin completar
    };
 ```

 - Verifica si el texto de la nueva tarea no está vacío
 ```
    if (newTodo.text.length > 0 ) {
      Agrega la nueva tarea al arreglo de tareas utilizando el spread operator y concat
        setTodos([...todos].concat(newTodo));
    } else {
       Si el texto está vacío, muestra una alerta para ingresar una tarea válida
        alert("Enter Valid Task");
    }
 ```
- Limpia el valor del input 'todoAdd'
 ```
    document.getElementById('todoAdd').value = "";
}
 ```
============================================================================================
 ```
<div id="todo-list">
    <h1>Todo List</h1>
        <form onSubmit={handleSubmit}>
 ```

- Crea un formulario que llama a la función 'handleSubmit' al enviarse 
 ```
            <input
              type="text"
              id='todoAdd' <!-- Asigna el id 'todoAdd' al input -->
                 />
 ```
 ```
            <button type="submit">Add Todo</button> <!-- Botón para agregar una tarea -->
        </form>
        <!-- Mapea sobre la lista de tareas 'todos' y muestra cada una -->
        {todos.map((todo) =>
            <div className="todo" key={todo.id}>
                <div className="todo-text">{todo.text}</div> <!-- Muestra el texto de la tarea -->
            <!-- insert delete button below this line -->
            </div>)}
</div>
 ```
============================================================================================
 #Filtra las tareas que no coincidan con el id proporcionado
```
function deleteTodo(id) {
    let updatedTodos = [...todos].filter((todo) => todo.id !== id);
```
 #Actualiza el estado 'todos' con las tareas filtradas
 ```
    setTodos(updatedTodos);
}
```
============================================================================================
Este botón está asociado a la función deleteTodo, que se ejecutará cuando se haga clic en él. Al hacer clic en el botón, se llama a la función deleteTodo con el id de la tarea (todo.id) como argumento. Esto provocará que la tarea correspondiente se elimine de la lista de tareas cuando se presione el botón "Delete".
```
<button onClick={() => deleteTodo(todo.id)}>Delete</button>
```
