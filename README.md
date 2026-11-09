# Balance API (v1.0.0)

API RESTful backend construida con **Node.js** y **Express.js** para el control de flujo de dinero, ingresos y gastos categorizados. Diseñada bajo una arquitectura limpia y un nivel técnico impecable, utilizando consultas SQL nativas, contenedores Docker y autenticación segura con JWT.

## 🚀 Tecnologías Principales

* **Runtime:** Node.js (ES Modules)
* **Framework Web:** Express.js
* **Gestor de Paquetes:** pnpm
* **Base de Datos:** MySQL (Driver nativo `mysql2` sin ORMs)
* **Autenticación:** JSON Web Tokens (JWT)
* **Contenedores:** Docker & Docker Compose

---

## 🛠️ Requisitos Previos

Asegúrate de tener instalado en tu entorno local:

* [Node.js](https://nodejs.org/) (v18+ recomendado)
* [pnpm](https://pnpm.io/)
* [Docker](https://www.docker.com/) y Docker Compose

---

## 📦 Configuración del Proyecto

1. **Clona el repositorio e instala las dependencias con pnpm:**
```bash
pnpm install

```


2. **Configura las variables de entorno:**
Crea un archivo `.env` en la raíz del proyecto basándote en la plantilla de ejemplo:
```env
PORT=4000
NODE_ENV=development

DB_HOST=localhost
DB_USER=root
DB_PASSWORD=tu_password
DB_NAME=balance_db
DB_PORT=3306

JWT_SECRET=tu_jwt_secret_super_seguro
JWT_EXPIRES_IN=1d

```



---

## 🐳 Ejecución con Docker (Recomendado)

Puedes levantar toda la aplicación y la base de datos MySQL de forma aislada utilizando Docker Compose:

```bash
# Construir y levantar los contenedores en segundo plano
docker-compose up --build -d

```

Para detener los contenedores:

```bash
docker-compose down

```

---

## 🏃‍♂️ Ejecución en Desarrollo (Local)

Si prefieres ejecutar el servidor en tu máquina local conectándote a una instancia de MySQL existente:

```bash
# Iniciar en modo desarrollo con recarga en vivo (watch)
pnpm run dev

```

---

## 📌 Endpoints Principales (v1.0.0)

| Método | Endpoint | Descripción |
| --- | --- | --- |
| `POST` | `/api/v1/auth/register` | Registro de nuevo usuario |
| `POST` | `/api/v1/auth/login` | Inicio de sesión y generación de JWT |
| `GET` | `/api/v1/categories` | Listar categorías del usuario |
| `POST` | `/api/v1/categories` | Crear una categoría personalizada (Ingreso/Gasto) |
| `GET` | `/api/v1/transactions` | Listar transacciones y movimientos |
| `POST` | `/api/v1/transactions` | Registrar un nuevo ingreso o gasto |
| `DELETE` | `/api/v1/transactions/:id` | Eliminar una transacción |
| `GET` | `/api/v1/balance/summary` | **Core:** Obtener balance total, ingresos, gastos y desglose |

---

## 🛡️ Decisiones Técnicas y Buenas Prácticas

* **Sin ORM:** Se utiliza el driver oficial `mysql2/promise` con consultas SQL puras y uso estricto de sentencias preparadas (`prepared statements`) para prevenir ataques de Inyección SQL y garantizar el máximo rendimiento.
* **Manejo de Moneda:** Para evitar errores de punto flotante en JavaScript, los montos monetarios se manejan de forma estricta (o almacenados como enteros multiplicados por 100).
* **Seguridad:** Cabeceras HTTP protegidas mediante `Helmet`, control de CORS y validación de esquemas robusta en las peticiones de entrada.