# API Tareas — Laravel 13

API REST con autenticación basada en tokens (Laravel Sanctum).

**Materia:** INF560 — Desarrollo Web Backend  
**Universidad:** Universidad Autónoma Tomás Frías (UATF)  
**GL10 tag:** v1.0.0 | **GL11 tag:** v2.0

## Stack
- Laravel 13 · PHP 8.3+ · PostgreSQL · Laravel Sanctum

## Instalación
```bash
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan serve
```

## Endpoints públicos (sin token)
| Método | Endpoint | Código |
|---|---|---|
| POST | /api/register | 201 |
| POST | /api/login | 200 |

## Endpoints protegidos (Bearer token)
| Método | Endpoint | Código |
|---|---|---|
| GET | /api/user | 200 |
| POST | /api/logout | 200 |
| GET | /api/tareas | 200 |
| POST | /api/tareas | 201 |
| GET | /api/tareas/{id} | 200 |
| PUT | /api/tareas/{id} | 200 |
| DELETE | /api/tareas/{id} | 204 |

## Errores
- 401 — Sin token o token revocado
- 403 — Tarea de otro usuario
- 404 — No encontrado
- 422 — Validación fallida