# Estructura del proyecto

El proyecto sigue una arquitectura basada en **Domain Driven Design (DDD)** separando responsabilidades por capas.

```
app/
 ├── Domain/
 │   └── Task/
 │       ├── Entities/
 │       │   └── Task.php
 │       ├── Repositories/
 │       │   └── TaskRepositoryInterface.php
 │       └── ValueObjects/
 │           └── TaskTitle.php
 │
 ├── Application/
 │   └── Task/
 │       └── CreateTaskUseCase.php
 │
 ├── Infrastructure/
 │   └── Persistence/
 │       └── EloquentTaskRepository.php
 │
 └── Http/
     └── Controllers/
         └── TaskController.php
```

## Capas

### Dominio
Contiene la **lógica de negocio pura** y es independiente del framework.

- **Entities**: Modelos del dominio con comportamiento (ej: **Task**).
- **Repositories**: Interfaces que definen cómo se accede a los datos.
- **ValueObjects**: Objetos inmutables que representan valores del dominio.

### Aplicación
Contiene los **casos de uso de la aplicación**.  
Orquesta la lógica del dominio para ejecutar acciones específicas (ej: **CreateTaskUseCase**).

### Infraestructura
Implementaciones técnicas como acceso a base de datos, servicios externos, etc.  
Aquí se implementan las interfaces del dominio (ej: **EloquentTaskRepository**).

### Http
Capa de entrada de la aplicación.  
Recibe las peticiones HTTP y delega la lógica en los **casos de uso** (ej: **TaskController**).