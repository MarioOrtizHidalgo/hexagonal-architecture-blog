# Capa HTTP

La **capa HTTP** es la encargada de gestionar la comunicación entre el sistema y los clientes externos a través del protocolo HTTP. En aplicaciones Laravel, esta capa incluye principalmente **controladores, rutas y peticiones** que reciben las solicitudes de los usuarios.

Dentro de una arquitectura hexagonal, la capa HTTP actúa como un **adaptador de entrada (Input Adapter)**. Su función principal es **recibir una petición, transformarla en datos que entienda la aplicación y ejecutar el caso de uso correspondiente**.

Es importante destacar que los controladores **no deben contener lógica de negocio**, ya que esta pertenece al dominio o a los casos de uso de la capa de aplicación.

## Responsabilidades de la capa HTTP

Las principales responsabilidades de esta capa son:

* Recibir peticiones HTTP

* Validar datos de entrada

* Llamar a los casos de uso de la aplicación

* Transformar la respuesta en JSON o HTML

* Gestionar códigos de estado HTTP

Esta capa es la más cercana al framework Laravel y al cliente que consume la aplicación.

## Estructura de carpetas

```
app/
 ├── Http/
 │   └── Controllers/
 │       └── TaskController.php
```

## Ejemplo de controlador

En este ejemplo implementaremos un controlador encargado de crear una nueva tarea utilizando el caso de uso **CreateTaskUseCase**.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Application\Task\CreateTaskUseCase;

class TaskController extends Controller
{
    private CreateTaskUseCase $createTask;

    public function __construct(CreateTaskUseCase $createTask)
    {
        $this->createTask = $createTask;
    }

    public function store(Request $request)
    {
        $task = $this->createTask->execute(
            $request->input('title')
        );

        return response()->json([
            'id' => $task->getId(),
            'title' => $task->getTitle()->value(),
            'completed' => $task->isCompleted()
        ]);
    }
}
```