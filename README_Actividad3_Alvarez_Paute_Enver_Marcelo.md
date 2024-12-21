# Sistema de Gestión de Proyectos

Este es un sistema web para la gestión de proyectos y participantes, desarrollado con Web Components en el frontend y Node.js con Express en el backend.

## Requisitos Previos

- Node.js (v14 o superior)
- MySQL (v5.7 o superior)
- npm (incluido con Node.js)

## Estructura del Proyecto

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 600">
    <!-- Estilo para el texto -->
    <style>
        .folder { fill: #5B7EAC; }
        .file { fill: #333; }
        .line { stroke: #666; stroke-width: 1; }
        text { font-family: monospace; font-size: 14px; }
    </style>

    <!-- Conexiones -->
    <!-- Líneas verticales principales -->
    <line x1="60" y1="40" x2="60" y2="560" class="line"/>
    <line x1="100" y1="80" x2="100" y2="240" class="line"/>
    <line x1="100" y1="280" x2="100" y2="560" class="line"/>
    
    <!-- Líneas horizontales -->
    <line x1="60" y1="80" x2="80" y2="80" class="line"/>
    <line x1="60" y1="280" x2="80" y2="280" class="line"/>
    
    <!-- Conexiones frontend -->
    <line x1="140" y1="120" x2="140" y2="240" class="line"/>
    <line x1="100" y1="120" x2="120" y2="120" class="line"/>
    <line x1="100" y1="240" x2="120" y2="240" class="line"/>
    
    <!-- Conexiones backend -->
    <line x1="140" y1="320" x2="140" y2="560" class="line"/>
    <line x1="100" y1="320" x2="120" y2="320" class="line"/>
    <line x1="100" y1="360" x2="120" y2="360" class="line"/>
    <line x1="100" y1="520" x2="120" y2="520" class="line"/>
    <line x1="100" y1="560" x2="120" y2="560" class="line"/>

    <!-- Carpeta raíz -->
    <text x="80" y="40" class="folder">📁 proyecto</text>
    
    <!-- Frontend -->
    <text x="120" y="80" class="folder">📁 frontend</text>
    <text x="160" y="120" class="folder">📁 components</text>
    <text x="180" y="140" class="file">📄 data-table.js</text>
    <text x="180" y="160" class="file">📄 footer-info.js</text>
    <text x="180" y="180" class="file">📄 header-info.js</text>
    <text x="180" y="200" class="file">📄 main-menu.js</text>
    <text x="180" y="220" class="file">📄 nav-menu.js</text>
    <text x="160" y="240" class="file">📄 index.html</text>
    
    <!-- Backend -->
    <text x="120" y="280" class="folder">📁 backend</text>
    <text x="160" y="320" class="folder">📁 config</text>
    <text x="180" y="340" class="file">📄 database.js</text>
    <text x="160" y="360" class="folder">📁 routes</text>
    <text x="180" y="380" class="file">📄 participants.js</text>
    <text x="180" y="400" class="file">📄 projects.js</text>
    <text x="160" y="520" class="file">📄 server.js</text>
    <text x="160" y="560" class="file">📄 package.json</text>

</svg>

## Configuración de la Base de Datos

1. Crear una base de datos MySQL llamada `project_management`
2. Ejecutar el siguiente script SQL para crear las tablas necesarias:

```sql
-- Tabla de proyectos
CREATE TABLE IF NOT EXISTS projects (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    start_date DATE NOT NULL,
    end_date DATE,
    status ENUM('active', 'completed', 'cancelled') DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Tabla de participantes
CREATE TABLE IF NOT EXISTS participants (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    role VARCHAR(50) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Tabla de relación muchos a muchos
CREATE TABLE IF NOT EXISTS project_participants (
    project_id INT,
    participant_id INT,
    role_in_project VARCHAR(50),
    joined_date DATE NOT NULL,
    FOREIGN KEY (project_id) REFERENCES projects(id) ON DELETE CASCADE,
    FOREIGN KEY (participant_id) REFERENCES participants(id) ON DELETE CASCADE,
    PRIMARY KEY (project_id, participant_id)
);
```

## Instalación

### Backend

1. Navegar al directorio del backend:
```bash
cd backend
```

2. Instalar las dependencias:
```bash
npm install
```

3. Configurar la conexión a la base de datos:
   - Abrir el archivo `config/database.js`
   - Modificar los siguientes valores según tu configuración:
```javascript
{
    host: 'localhost',
    user: 'root',
    password: '',
    port: 3306,
    database: 'project_management'
}
```

4. Iniciar el servidor:
```bash
npm run dev
```

El servidor estará ejecutándose en `http://localhost:8080`

### Frontend

1. Para el frontend, simplemente abrir el archivo `index.html` en un navegador web moderno.
   - Recomendación: Usar Live Server en Visual Studio Code o un servidor web local similar.

2. Si usas Visual Studio Code:
   - Instalar la extensión "Live Server"
   - Click derecho en `index.html`
   - Seleccionar "Open with Live Server"

## Uso del Sistema

1. La aplicación tiene tres secciones principales:
   - **Inicio**: Menú principal con acceso a las diferentes funcionalidades
   - **Proyectos**: Gestión de proyectos (crear, editar, eliminar)
   - **Participantes**: Gestión de participantes (crear, editar, eliminar)

2. Funcionalidades principales:
   - Crear nuevos proyectos
   - Agregar participantes
   - Asignar participantes a proyectos
   - Ver listados de proyectos y participantes
   - Editar y eliminar registros

## Características

- Interfaz de usuario moderna y responsiva
- Componentes web reutilizables
- API RESTful
- Persistencia de datos en MySQL
- Notificaciones de acciones
- Validación de formularios

## Tecnologías Utilizadas

- Frontend:
  - HTML5
  - CSS3
  - JavaScript (Web Components)
- Backend:
  - Node.js
  - Express.js
  - MySQL2
  - CORS
- Base de Datos:
  - MySQL

## Contribuir

1. Fork el repositorio
2. Crear una rama para tu función (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abrir un Pull Request

## Autor

Enver Alvarez
