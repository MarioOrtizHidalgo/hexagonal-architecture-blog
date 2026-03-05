# Capa de Infraestructura

La **capa de infraestructura** es la encargada de **conectar el sistema con el mundo exterior**. En una arquitectura hexagonal, esta capa contiene las implementaciones concretas de los servicios que el dominio necesita, como el acceso a bases de datos, APIs externas, sistemas de almacenamiento o servicios de mensajería.

Mientras que el **dominio define las interfaces (puertos)** que necesita para funcionar, la infraestructura proporciona las **implementaciones reales (adaptadores)** que permiten interactuar con tecnologías específicas.

Por ejemplo, el dominio puede definir una interfaz para guardar tareas, pero la capa de infraestructura decide **si se guardan en una base de datos MySQL, PostgreSQL o incluso en un servicio externo**.

## Responsabilidades de la capa de infraestructura

Las principales responsabilidades de esta capa son:

* Implementar los repositorios definidos en el dominio

* Gestionar la persistencia de datos

* Integrarse con frameworks o librerías externas

* Conectar con bases de datos

* Implementar servicios externos (APIs, almacenamiento, etc.)

Es importante destacar que **la infraestructura depende del dominio**, pero el dominio **no depende de la infraestructura**.

Esto mantiene el sistema desacoplado y facilita cambios tecnológicos en el futuro.

## Estructura de carpetas

En este ejemplo, la carpeta Persistence contiene las implementaciones relacionadas con la persistencia de datos utilizando Eloquent, el ORM de Laravel.

```app/
 ├── Infrastructure/
 │   └── Persistence/
 │       └── EloquentTaskRepository.php
```

## Implementación de un repositorio

El dominio define una interfaz llamada:

    TaskRepositoryInterface

Esta interfaz describe las operaciones necesarias para trabajar con tareas, pero **no especifica cómo se implementan**.

La capa de infraestructura se encarga de implementar esa interfaz utilizando Eloquent.

```php
<?php

namespace App\Infrastructure\Persistence;

use App\Domain\Task\Repositories\TaskRepositoryInterface;
use App\Domain\Task\Entities\Task;
use App\Domain\Task\ValueObjects\TaskTitle;
use App\Models\Task as TaskModel;

class EloquentTaskRepository implements TaskRepositoryInterface
{
    public function save(Task $task): Task
    {
        $model = new TaskModel();

        $model->title = $task->getTitle()->value();
        $model->completed = $task->isCompleted();

        $model->save();

        return new Task(
            $model->id,
            new TaskTitle($model->title),
            $model->completed
        );
    }

    public function find(int $id): ?Task
    {
        $model = TaskModel::find($id);

        if (!$model) {
            return null;
        }

        return new Task(
            $model->id,
            new TaskTitle($model->title),
            $model->completed
        );
    }
}
```

## Explicación del código

### Implementación de la interfaz del dominio

    class EloquentTaskRepository implements TaskRepositoryInterface

Aquí la clase implementa la interfaz definida en el dominio. De esta forma se respeta el principio de **inversión de dependencias**, donde el dominio define el contrato y la infraestructura proporciona la implementación.

### Uso de Eloquent

    use App\Models\Task as TaskModel;

La infraestructura puede utilizar tecnologías específicas como:

Eloquent

APIs externas

sistemas de archivos

servicios de terceros

Estas dependencias **no deben aparecer en la capa de dominio**.

### Conversión entre modelo y entidad

La infraestructura también se encarga de convertir entre:

* Modelos de base de datos

* Entidades del dominio

Ejemplo:

```php
return new Task(
    $model->id,
    new TaskTitle($model->title),
    $model->completed
);
```

Esto permite que el dominio **trabaje únicamente con sus propias entidades**, sin depender del ORM.