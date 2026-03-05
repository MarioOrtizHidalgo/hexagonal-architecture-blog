# Capa de Dominio

La **Capa de Dominio** es el núcleo de la aplicación. Aquí vive la lógica de negocio pura, completamente independiente de frameworks, bases de datos o cualquier tecnología externa.

## ¿De qué se encarga la Capa de Dominio?

Su única misión es representar las **reglas de negocio**. Imagina que mañana decides cambiar Laravel por otro framework o decides que ya no usarás MySQL sino MongoDB; la capa de dominio **no debería cambiar ni una sola línea de código**.

**Sus responsabilidades principales son:**
* Definir los procesos y reglas que hacen que tu negocio sea único.

* Asegurar la consistencia de los datos del negocio.

* Ser independiente de la infraestructura (no sabe qué es Eloquent, ni qué es un Request de HTTP).

## ¿Qué contiene la Capa de Dominio?

Normalmente encontraremos lo siguiente:

1. **Entidades** (Entities)

Son objetos que tienen una identidad propia que persiste en el tiempo. En Laravel, **no son modelos de Eloquent**. Son clases de PHP puras (POJOs).

```php
<?php

namespace App\Domain\Task\Entities;

use App\Domain\Task\ValueObjects\TaskTitle;

class Task
{
    private ?int $id;
    private TaskTitle $title;
    private bool $completed;

    public function __construct(?int $id, TaskTitle $title, bool $completed = false)
    {
        $this->id = $id;
        $this->title = $title;
        $this->completed = $completed;
    }

    public function getId(): ?int
    {
        return $this->id;
    }

    public function getTitle(): TaskTitle
    {
        return $this->title;
    }

    public function isCompleted(): bool
    {
        return $this->completed;
    }

    public function complete(): void
    {
        $this->completed = true;
    }
}
```

2. **Objetos de Valor** (Value Objects)

Son objetos que se identifican por sus propiedades y no por su identidad. Con esto hacen que sean inmutables.

* **Ejemplos**: Email, Price, Cpf, Uuid.

* **Ventaja**: En lugar de pasar un string para un email, pasas un objeto Email que se valida a sí mismo al crearse.

En este ejemplo vamos a crear un **Value Object** para el titulo de la tarea.

```php
<?php

namespace App\Domain\Task\ValueObjects;

class TaskTitle
{
    private string $value;

    public function __construct(string $value)
    {
        if (strlen($value) < 3) {
            throw new \InvalidArgumentException("El título debe tener al menos 3 caracteres");
        }

        $this->value = $value;
    }

    public function value(): string
    {
        return $this->value;
    }
}
```

3. **Repositorios** (Interfaces)

Aquí es donde aplicamos el principio de inversión de dependencia. El dominio define qué necesita (una interfaz), pero no **cómo** se obtiene.

```php
<?php

namespace App\Domain\Task\Repositories;

use App\Domain\Task\Entities\Task;

interface TaskRepositoryInterface
{
    public function save(Task $task): Task;

    public function find(int $id): ?Task;
}
```