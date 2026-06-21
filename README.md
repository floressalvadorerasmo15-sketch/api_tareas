# API Tareas — Laravel 13

API REST pública (sin autenticación) para gestionar tareas, construida con Laravel 13 y PostgreSQL.

**Materia:** INF560 — Desarrollo Web Backend
**Guía:** Laboratorio N° 10 — Construcción de una API REST
**Universidad:** Universidad Autónoma Tomás Frías (UATF)

## Stack

- Laravel 13
- PHP 8.3+
- PostgreSQL
- Laravel Sanctum (instalado, sin usar todavía — se activará en la GL11)

## Instalación

1. Clonar el repositorio:
   ```
   git clone https://github.com/floressalvadorerasmo15-sketch/api_tareas.git
   cd api_tareas
   ```

2. Instalar dependencias:
   ```
   composer install
   ```

3. Configurar el archivo `.env`:
   ```
   cp .env.example .env
   php artisan key:generate
   ```

   Editar las variables de conexión a PostgreSQL:
   ```
   DB_CONNECTION=pgsql
   DB_HOST=127.0.0.1
   DB_PORT=5432
   DB_DATABASE=api_tareas
   DB_USERNAME=postgres
   DB_PASSWORD=tu_password
   ```

4. Crear la base de datos en PostgreSQL:
   ```sql
   CREATE DATABASE api_tareas;
   ```

5. Ejecutar las migraciones:
   ```
   php artisan migrate
   ```

6. Levantar el servidor:
   ```
   php artisan serve
   ```

   La API queda disponible en `http://127.0.0.1:8000/api`

## Endpoints

Todas las peticiones deben incluir el header `Accept: application/json`.

| Método | Endpoint | Acción | Código de éxito |
|---|---|---|---|
| GET | `/api/tareas` | Listar tareas (paginadas, 10 por página) | 200 |
| POST | `/api/tareas` | Crear una tarea | 201 |
| GET | `/api/tareas/{id}` | Ver una tarea | 200 |
| PUT | `/api/tareas/{id}` | Actualizar una tarea | 200 |
| DELETE | `/api/tareas/{id}` | Eliminar una tarea | 204 |

### Campos del recurso Tarea

| Campo | Tipo | Reglas de validación |
|---|---|---|
| titulo | string | required, max:255 |
| descripcion | string | nullable |
| completada | boolean | opcional (default: false) |
| vence_el | date | nullable |

### Códigos de error

- `404 Not Found` — el recurso solicitado no existe.
- `422 Unprocessable Content` — la validación falló (incluye detalle de errores por campo).

## Ejemplos con cURL

**Crear una tarea:**
```bash
curl -X POST http://127.0.0.1:8000/api/tareas \
  -H "Accept: application/json" \
  -d "titulo=Preparar laboratorio" \
  -d "descripcion=Guia 10 API REST" \
  -d "vence_el=2026-07-01"
```

**Listar tareas:**
```bash
curl http://127.0.0.1:8000/api/tareas -H "Accept: application/json"
```

**Ver una tarea:**
```bash
curl http://127.0.0.1:8000/api/tareas/1 -H "Accept: application/json"
```

**Actualizar una tarea:**
```bash
curl -X PUT http://127.0.0.1:8000/api/tareas/1 \
  -H "Accept: application/json" \
  -d "titulo=Tarea actualizada"
```

**Eliminar una tarea:**
```bash
curl -X DELETE http://127.0.0.1:8000/api/tareas/1 -H "Accept: application/json"
```

## Colección de Postman

Se incluye el archivo `api-tareas.postman_collection.json` con todas las peticiones listas para importar en Postman.

## Próximos pasos

Este proyecto continuará en la **GL11**, donde se añadirá autenticación con Laravel Sanctum.

## Autor

Erasmo — Ingeniería Informática, UATF
