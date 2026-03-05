# Capa de Aplicación

La **capa de aplicación** es la encargada de **coordinar los casos de uso del sistema**. Su función principal es actuar como intermediaria entre la **capa de dominio**, donde se encuentra la lógica de negocio, y **las capas externas** como controladores, APIs o interfaces de usuario.

A diferencia de la capa de dominio, que contiene reglas de negocio puras, la capa de aplicación **orquesta operaciones** utilizando las entidades y repositorios definidos en el dominio.

En otras palabras, esta capa responde a la pregunta:

    ¿Qué acciones puede realizar el sistema?

Por ejemplo:

* Crear una tarea

* Eliminar una tarea

* Marcar una tarea como completada

* Obtener una lista de tareas

Estas acciones se implementan mediante **casos de uso** (Use Cases).

## ¿Qué responsibilidades tiene la Capa de Aplicación?

Las principales responsabilidades de esta capa son:

* Ejecutar **casos de uso del sistema**

* Coordinar entidades del dominio

* Utilizar repositorios definidos en el dominio

* Controlar el flujo de la aplicación

* Preparar los datos para otras capas

Es importante destacar que **la capa de aplicación no contiene lógica de negocio compleja**, ya que esta debe pertenecer al dominio.

## Ejemplo de caso de uso

Supongamos que queremos implementar la funcionalidad de crear una nueva tarea.

Para ello creamos el siguiente caso de uso:

    CreateTaskUseCase

Este caso de uso se encargará de:

* Recibir el título de la tarea

* Crear la entidad del dominio

* Guardarla utilizando el repositorio

## Ejemplo de implementación

```php
<?php

namespace App\Application\Task;

use App\Domain\Task\Repositories\TaskRepositoryInterface;
use App\Domain\Task\Entities\Task;
use App\Domain\Task\ValueObjects\TaskTitle;

class CreateTaskUseCase
{
    private TaskRepositoryInterface $repository;

    public function __construct(TaskRepositoryInterface $repository)
    {
        $this->repository = $repository;
    }

    public function execute(string $title): Task
    {
        // Crear el value object con la validación del dominio
        $taskTitle = new TaskTitle($title);

        // Crear la entidad del dominio
        $task = new Task(null, $taskTitle);

        // Guardar la tarea utilizando el repositorio
        return $this->repository->save($task);
    }
}
```