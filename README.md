REYES OROPEZA NICOLE SAMAHARA
GARCIA VALENCIA VALERIA SARAHÍ

Práctica:
Implementar una aplicación web funcional que permita a los usuarios crear, visualizar, editar y eliminar tareas. 
Utilizar HTML5 para la estructura de la aplicación, CSS3 para el diseño y estilos, y JavaScript puro (Vanilla JS) para la lógica de la aplicación. 
La aplicación debe ser responsiva y ofrecer una buena experiencia de usuario en dispositivos móviles y de escritorio.
Introducción:
La aplicación es una lista de tareas simple y efectiva que permite a los usuarios organizar y administrar sus actividades diarias de manera eficiente. Con una interfaz limpia y fácil de usar, los usuarios pueden agregar, editar, marcar como completadas y eliminar tareas según sea necesario.
Cómo funciona:
•	Cuando se hace clic en el botón "AÑADIR", se llama a la función agregarTarea().
•	Esta función recoge el texto de la tarea del campo de entrada, crea un objeto de tarea con un identificador único generado por la fecha y hora actual, marca la tarea como no completada inicialmente y la agrega al array tareas.
•	Después de agregar la tarea, se llama a la función renderizarTareas() para actualizar la lista de tareas en la interfaz de usuario.
•	La función renderizarTareas() borra la lista actual de tareas y vuelve a crear los elementos <li> para cada tarea en el array tareas.
•	Cada tarea tiene un checkbox para marcarla como completada, un campo de texto para editar su contenido y un botón para eliminarla.
•	Cuando se marca o desmarca una tarea como completada, se llama a la función marcarTarea(), que actualiza el estado de la tarea y vuelve a renderizar las tareas.
•	Si se edita el texto de una tarea, se llama a la función actualizarTarea(), que actualiza el texto de la tarea en el array tareas.
•	Si se hace clic en el botón "Eliminar" de una tarea, se llama a la función eliminarTarea(), que elimina la tarea del array tareas.
•	Al cargar la página, se llama a renderizarTareas() para mostrar las tareas almacenadas inicialmente en el array tareas.
Enlace GitHub: https://github.com/nicoleSamahara12/proyecto.github.io.git

Código Fuente:
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LISTA DE TAREAS</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-image: url("imagenes/fondo3.jpg");
        }
        .container {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #f7dada; 
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
        }
        h1 {
            text-align: center;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        li {
            margin-bottom: 10px;
        }
        .task {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #ccc;
            padding: 10px;
        }
        .task input[type="text"] {
            width: 70%;
            padding: 5px;
        }
        .task button {
            padding: 8px 15px;
            cursor: pointer;
            background-color: #ff9dbd; /* Rosa claro */
            border: none;
            border-radius: 20px;
            color: white;
            font-size: 16px;
            transition: background-color 0.3s;
        }
        .task button:hover {
            background-color: #ff749d; /* Rosa oscuro */
        }
        .task input[type="checkbox"] {
            margin-right: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>LISTA DE TAREAS</h1>
        <input type="text" id="taskInput" placeholder="Agregar una nueva tarea">
        <button onclick="agregarTarea()">AÑADIR</button>
        <ul id="taskList"></ul>
</div>
    <script>
        // Array para almacenar las tareas
        let tareas = [];

        // Función para agregar una nueva tarea
        function agregarTarea() {
            const entradaTarea = document.getElementById('taskInput');
            const textoTarea = entradaTarea.value.trim();
            if (textoTarea !== '') {
                const nuevaTarea = {
                    id: Date.now(),
                    texto: textoTarea,
                    completada: false
                };
                tareas.push(nuevaTarea);
                renderizarTareas();
                entradaTarea.value = '';
            }
        }
        // Función para renderizar las tareas
        function renderizarTareas() {
            const listaTareas = document.getElementById('taskList');
            listaTareas.innerHTML = '';
            tareas.forEach(tarea => {
                const li = document.createElement('li');
                li.classList.add('task');
                if (tarea.completada) {
                    li.classList.add('completed');
                }
                li.innerHTML = `
                    <input type="checkbox" ${tarea.completada ? 'checked' : ''} onchange="marcarTarea(${tarea.id}, this.checked)">
                    <input type="text" value="${tarea.texto}" ${tarea.completada ? 'disabled' : ''} onchange="actualizarTarea(${tarea.id}, this.value)">
                    <button onclick="eliminarTarea(${tarea.id})">Eliminar</button>
                `;
                listaTareas.appendChild(li);
            });
        }
        // Función para marcar una tarea como completada
        function marcarTarea(id, completada) {
            const tarea = tareas.find(tarea => tarea.id === id);
            if (tarea) {
                tarea.completada = completada;
                renderizarTareas();
            }
        }
        // Función para actualizar una tarea
        function actualizarTarea(id, nuevoTexto) {
            const tarea = tareas.find(tarea => tarea.id === id);
            if (tarea) {
                tarea.texto = nuevoTexto;
            }
        }
        // Función para eliminar una tarea
        function eliminarTarea(id) {
            tareas = tareas.filter(tarea => tarea.id !== id);
            renderizarTareas();
        }
        // Renderizado inicial
        renderizarTareas();
    </script>
</body>
</html>


