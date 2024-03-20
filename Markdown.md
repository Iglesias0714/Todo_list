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
```
function deleteTodo(id) {
    let updatedTodos = [...todos].filter((todo) => todo.id !== id);
    setTodos(updatedTodos);
  }
  ```
 - Filtra las tareas que no coincidan con el id proporcionado
```
function deleteTodo(id) {
    let updatedTodos = [...todos].filter((todo) => todo.id !== id);
```
 - Actualiza el estado 'todos' con las tareas filtradas
 ```
    setTodos(updatedTodos);
}
```
============================================================================================
- Este botón está asociado a la función deleteTodo, que se ejecutará cuando se haga clic en él.
  Al hacer clic en el botón, se llama a la función deleteTodo con el id de la tarea (todo.id)
  como argumento.Esto provocará que la tarea correspondiente se elimine de
  la lista de tareas cuando se presione el botón "Delete".
```
<button onClick={() => deleteTodo(todo.id)}>Delete</button>
```
============================================================================================
   ```
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
 - Crea una copia del arreglo 'todos' utilizando el spread operator
   ```
   function toggleComplete(id) {
    let updatedTodos = [...todos].map((todo) => {
   ```
 - Comprueba si el id de la tarea coincide con el id proporcionado
     ```
        if (todo.id === id) {
     ```
- Cambia el estado de completado de la tarea a su opuesto
  ```
            todo.completed = !todo.completed;
        }
        return todo; // Devuelve la tarea actualizada
    });
    ```
 - Actualiza el estado 'todos' con las tareas modificadas
   ```
    setTodos(updatedTodos);
     }
    ```
   ============================================================================================
  - Este es un elemento de entrada de tipo checkbox. Cuando se selecciona, cambia el estado de
    completado de una tarea específica en la lista de tareas. La propiedad checked determina
    si el checkbox está marcado o desmarcado según el estado de completado de la tarea todo.
    Cuando se produce un cambio en el checkbox (seleccionar o deseleccionar), se ejecuta la
    función toggleComplete(todo.id), que cambia el estado de completado de la tarea correspondiente
    en la lista de tareas.
  ```
 <input type="checkbox" id="completed" checked={todo.completed} onChange={() => toggleComplete(todo.id)}/>
  ```
   ============================================================================================
  -Esto es un estado de React que se inicializa con un valor nulo. Se utiliza para realizar un 
  seguimiento de la tarea que se está editando en la lista de tareas. La variable todoEditing 
  almacena el ID de la tarea que se está editando actualmente, mientras que setTodoEditing es 
  una función que se utiliza para actualizar ese valor. Cuando una tarea se selecciona para 
  edición, su ID se asigna a todoEditing, y cuando se completa la edición o se cancela, todoEditing
  vuelve a ser null. Esto permite que la interfaz de usuario responda dinámicamente al estado de 
  edición de las tareas.
    ``` 
    const [todoEditing, setTodoEditing] = useState(null);
    ```
     ============================================================================================
     
