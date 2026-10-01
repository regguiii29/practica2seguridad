# Práctica de Docker - Ejercicios para Evaluación
## Conceptos Fundamentales y Ejercicios Prácticos

**Nombre:** ______________________________  
**Fecha:** _______________________________  
**Grupo:** _______________________________

---

## Instrucciones Generales

Esta práctica evalúa tu comprensión de Docker y sus conceptos fundamentales. Lee cuidadosamente cada ejercicio y completa las tareas solicitadas. Documenta todos los comandos utilizados y explica brevemente cada paso.

**Tiempo estimado:** 2-3 horas  
**Puntuación total:** 100 puntos

---

## Ejercicio 1: Comandos Básicos de Docker (15 puntos)

### Parte A (5 puntos)
**Tarea:** Gestión básica de imágenes y contenedores

1. Lista todas las imágenes disponibles en tu sistema local
2. Descarga la imagen oficial de Ubuntu versión 20.04
3. Descarga la imagen oficial de Nginx versión alpine
4. Muestra información detallada del sistema Docker
5. Lista todos los contenedores (tanto activos como inactivos)

**Comandos utilizados:**
```
1. ________________________________
2. ________________________________
3. ________________________________
4. ________________________________
5. ________________________________
```

### Parte B (10 puntos)
**Tarea:** Explica qué hace cada uno de estos comandos y cuándo los usarías:

1. `docker ps -a`
2. `docker images --filter dangling=true`
3. `docker info`
4. `docker version`
5. `docker system df`

**Respuestas:**
1. ________________________________________________________________
2. ________________________________________________________________
3. ________________________________________________________________
4. ________________________________________________________________
5. ________________________________________________________________

---

## Ejercicio 2: Gestión de Contenedores - RUN, START, STOP (20 puntos)

### Parte A: Comando RUN (10 puntos)
**Tareas:**

1. **Ejecuta un contenedor de Ubuntu** que muestre el mensaje "Hola Docker" y se elimine automáticamente
2. **Crea un contenedor interactivo** de Ubuntu que permanezca activo y te permita acceder a su terminal
3. **Ejecuta un servidor Nginx** en segundo plano con un nombre personalizado "mi-servidor-web"
4. **Crea un contenedor** que se ejecute solo durante 30 segundos y luego se detenga automáticamente

**Comandos utilizados:**
```
1. ________________________________
2. ________________________________
3. ________________________________
4. ________________________________
```

### Parte B: START y STOP (10 puntos)
**Escenario:** Tienes un contenedor llamado "mi-app" que está detenido.

**Tareas:**
1. Inicia el contenedor "mi-app"
2. Verifica que está ejecutándose
3. Detén el contenedor de forma controlada
4. Fuerza la detención del contenedor (si fuera necesario)
5. Reinicia el contenedor

**Comandos y explicación:**
```
1. ________________________________
2. ________________________________
3. ________________________________
4. ________________________________
5. ________________________________
```

**Pregunta:** ¿Cuál es la diferencia entre `docker stop` y `docker kill`?
________________________________________________________________

---

## Ejercicio 3: Comunicación con Contenedores (20 puntos)

### Parte A: Mapeo de Puertos (10 puntos)
**Tarea:** Configura diferentes escenarios de mapeo de puertos

**Escenarios a implementar:**
1. Nginx ejecutándose en el puerto 8080 del host, mapeado al puerto 80 del contenedor
2. Nginx con puerto aleatorio asignado automáticamente
3. Aplicación web que escuche en múltiples puertos (80 y 443)
4. Servicio que solo sea accesible desde localhost en el puerto 3000

**Comandos utilizados:**
```
1. ________________________________
2. ________________________________
3. ________________________________
4. ________________________________
```

### Parte B: Ejecutar Comandos dentro del Contenedor (10 puntos)
**Escenario:** Tienes un contenedor Nginx llamado "web-server" ejecutándose.

**Tareas:**
1. Lista el contenido del directorio `/usr/share/nginx/html`
2. Accede al terminal interactivo del contenedor
3. Instala el editor `nano` dentro del contenedor
4. Visualiza los logs del contenedor en tiempo real
5. Muestra las estadísticas de uso del contenedor

**Comandos utilizados:**
```
1. ________________________________
2. ________________________________
3. ________________________________
4. ________________________________
5. ________________________________
```

---

## Ejercicio 4: Montaje de Volúmenes (20 puntos)

### Tarea Principal: Servidor Web con Contenido Personalizado
**Objetivo:** Crear un servidor web Apache que sirva contenido desde tu sistema de archivos local.

**Requisitos:**
1. Crea un directorio local llamado `mi-sitio-web`
2. Dentro del directorio, crea un archivo `index.html` con:
   - Título personalizado
   - Tu nombre y fecha
   - Al menos 3 párrafos de contenido
   - Algo de CSS básico para darle estilo
3. Ejecuta un contenedor Apache que:
   - Use la imagen `httpd:alpine`
   - Sirva el contenido de tu directorio local
   - Sea accesible en el puerto 8080
   - Tenga un nombre descriptivo

**Documentación requerida:**

**Estructura de directorios creada:**
```
mi-sitio-web/
├── ________________________________
└── ________________________________ (si agregas más archivos)
```

**Comando para ejecutar el contenedor:**
```
________________________________
```

**Verificación:**
- URL para acceder al sitio: ________________________________
- Comando para verificar que funciona: ________________________________

**Pregunta:** ¿Qué sucede con los archivos dentro del contenedor si lo eliminas pero mantienes el volumen?
________________________________________________________________

**Pregunta adicional:** Explica la diferencia entre bind mounts y volúmenes Docker:
________________________________________________________________

---

## Ejercicio 5: Docker Compose (15 puntos)

### Tarea: Stack de Aplicación Multi-contenedor
**Objetivo:** Crear un archivo `docker-compose.yml` que defina los siguientes servicios y código PHP para probar la conexión.

**Requisitos del stack:**
1. **Servicio Web (PHP + Apache):**
   - Imagen: `php:8.0-apache`
   - Puerto: 8080 (host) → 80 (contenedor)
   - Debe montar un volumen con código PHP
   - Nombre del contenedor: `web-app`

2. **Servicio de Base de Datos:**
   - Imagen: `mysql:8.0`
   - Variables de entorno necesarias para MySQL
   - Volumen persistente para los datos
   - Nombre del contenedor: `database`

3. **Servicio de Administración:**
   - Imagen: `phpmyadmin:latest`
   - Puerto: 8081 (host) → 80 (contenedor)
   - Debe conectarse automáticamente a la base de datos
   - Nombre del contenedor: `admin`

**Preparación de archivos PHP:**

Antes de crear el docker-compose.yml, debes crear la siguiente estructura de carpetas y archivos:

**Estructura de directorios:**
```
mi-proyecto/
├── docker-compose.yml
└── src/
    ├── index.php
    └── Dockerfile
```

**Archivo `src/Dockerfile` (necesario para instalar extensión MySQL):**
```dockerfile
FROM php:8.0-apache

# Instalar extensión PDO para MySQL
RUN docker-php-ext-install pdo pdo_mysql

# Habilitar mod_rewrite de Apache (opcional)
RUN a2enmod rewrite
```

**Archivo `src/index.php` (código proporcionado):**
```php
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi App Docker - Práctica</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: rgba(255,255,255,0.1);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(31, 38, 135, 0.37);
        }
        .status {
            padding: 15px;
            margin: 10px 0;
            border-radius: 8px;
            font-weight: bold;
        }
        .success { background: rgba(76, 175, 80, 0.8); }
        .error { background: rgba(244, 67, 54, 0.8); }
        .info { background: rgba(33, 150, 243, 0.8); }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            background: rgba(255,255,255,0.1);
        }
        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid rgba(255,255,255,0.2);
        }
        th { background: rgba(255,255,255,0.2); }
    </style>
</head>
<body>
    <div class="container">
        <h1>🐳 Mi Aplicación Docker - Stack Completo</h1>
        
        <div class="info">
            <h3>📊 Información del Sistema</h3>
            <p><strong>Servidor:</strong> <?php echo $_SERVER['SERVER_NAME']; ?></p>
            <p><strong>PHP Version:</strong> <?php echo phpversion(); ?></p>
            <p><strong>Fecha y Hora:</strong> <?php echo date('Y-m-d H:i:s'); ?></p>
        </div>

        <div class="info">
            <h3>🔧 Prueba de Conexión a MySQL</h3>
            <?php
            // Configuración de conexión a la base de datos
            $host = 'database';  // Nombre del servicio en docker-compose
            $dbname = 'mi_base_datos';
            $username = 'mi_usuario';
            $password = 'mi_password';

            try {
                // Crear conexión PDO
                $pdo = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8", $username, $password);
                $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
                
                echo '<div class="success">✅ Conexión a MySQL exitosa</div>';
                
                // Crear tabla de prueba si no existe
                $pdo->exec("CREATE TABLE IF NOT EXISTS usuarios (
                    id INT AUTO_INCREMENT PRIMARY KEY,
                    nombre VARCHAR(100) NOT NULL,
                    email VARCHAR(100) NOT NULL,
                    fecha_registro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
                )");
                
                // Insertar datos de prueba si la tabla está vacía
                $stmt = $pdo->query("SELECT COUNT(*) FROM usuarios");
                if ($stmt->fetchColumn() == 0) {
                    $pdo->exec("INSERT INTO usuarios (nombre, email) VALUES 
                        ('Juan Pérez', 'juan@ejemplo.com'),
                        ('María García', 'maria@ejemplo.com'),
                        ('Carlos López', 'carlos@ejemplo.com')");
                    echo '<div class="success">📝 Datos de prueba insertados</div>';
                }
                
                // Mostrar datos de la tabla
                echo '<h4>👥 Usuarios en la Base de Datos:</h4>';
                $stmt = $pdo->query("SELECT * FROM usuarios ORDER BY fecha_registro DESC");
                $usuarios = $stmt->fetchAll(PDO::FETCH_ASSOC);
                
                if ($usuarios) {
                    echo '<table>';
                    echo '<tr><th>ID</th><th>Nombre</th><th>Email</th><th>Fecha Registro</th></tr>';
                    foreach ($usuarios as $usuario) {
                        echo '<tr>';
                        echo '<td>' . htmlspecialchars($usuario['id']) . '</td>';
                        echo '<td>' . htmlspecialchars($usuario['nombre']) . '</td>';
                        echo '<td>' . htmlspecialchars($usuario['email']) . '</td>';
                        echo '<td>' . htmlspecialchars($usuario['fecha_registro']) . '</td>';
                        echo '</tr>';
                    }
                    echo '</table>';
                } else {
                    echo '<p>No hay usuarios en la base de datos.</p>';
                }
                
            } catch(PDOException $e) {
                echo '<div class="error">❌ Error de conexión: ' . htmlspecialchars($e->getMessage()) . '</div>';
                echo '<div class="error">💡 Verifica que el servicio de base de datos esté ejecutándose correctamente</div>';
            }
            ?>
        </div>

        <div class="info">
            <h3>🔗 Enlaces Útiles</h3>
            <p><strong>phpMyAdmin:</strong> <a href="http://localhost:8081" target="_blank" style="color: #fff;">http://localhost:8081</a></p>
            <p><strong>Esta aplicación:</strong> <a href="http://localhost:8080" target="_blank" style="color: #fff;">http://localhost:8080</a></p>
        </div>

        <div class="info">
            <h3>🎯 Objetivos Completados</h3>
            <ul>
                <li>✅ Servidor web PHP funcionando</li>
                <li>✅ Base de datos MySQL conectada</li>
                <li>✅ phpMyAdmin disponible</li>
                <li>✅ Datos de prueba insertados</li>
                <li>✅ Stack multi-contenedor operativo</li>
            </ul>
        </div>
    </div>
</body>
</html>
```

**Archivo docker-compose.yml (a completar):**
```yaml
# Completa el archivo aquí:
version: '______________'

services:
  web:
    # Construir desde el Dockerfile en src/
    build: ________________________________
    container_name: ________________________________
    ports:
      - "________________________________"
    volumes:
      - ________________________________
    depends_on:
      - ________________________________
    networks:
      - ________________________________
    
  database:
    image: ________________________________
    container_name: ________________________________
    environment:
      MYSQL_ROOT_PASSWORD: ________________________________
      MYSQL_DATABASE: ________________________________
      MYSQL_USER: ________________________________
      MYSQL_PASSWORD: ________________________________
    volumes:
      - ________________________________
    networks:
      - ________________________________
    
  phpmyadmin:
    image: ________________________________
    container_name: ________________________________
    ports:
      - "________________________________"
    environment:
      PMA_HOST: ________________________________
    depends_on:
      - ________________________________
    networks:
      - ________________________________

# Completa las secciones adicionales necesarias:
volumes:
  ________________________________

networks:
  ________________________________
```

**Notas importantes:**
- El archivo PHP ya está proporcionado y no necesitas modificarlo
- El Dockerfile instala automáticamente la extensión MySQL para PHP
- Las credenciales de la base de datos en docker-compose.yml deben coincidir con las del archivo PHP
- Recuerda crear la estructura de carpetas antes de ejecutar docker-compose

**Comandos de Docker Compose:**
1. Comando para iniciar todos los servicios: ________________________________
2. Comando para ver logs de todos los servicios: ________________________________
3. Comando para detener y eliminar todos los contenedores: ________________________________

---

## Ejercicio 6: Creación de Imagen Personalizada (10 puntos)

### Tarea: Imagen Ubuntu con Herramientas
**Objetivo:** Crear un Dockerfile que genere una imagen basada en Ubuntu con herramientas útiles instaladas.

**Requisitos de la imagen:**
- Base: Ubuntu 20.04
- Herramientas a instalar: `curl`, `wget`, `vim`, `git`, `ping`, `telnet`
- Usuario no-root llamado `estudiante`
- Directorio de trabajo: `/home/estudiante`
- Comando por defecto: bash interactivo

**Dockerfile:**
```dockerfile
# Completa el Dockerfile aquí:
FROM ________________________________

# Actualizar sistema e instalar herramientas


# Crear usuario no-root


# Configurar directorio de trabajo


# Comando por defecto

```

**Comandos necesarios:**
1. Construir la imagen: ________________________________
2. Ejecutar contenedor interactivo: ________________________________
3. Listar imágenes para verificar: ________________________________

---

## Preguntas Teóricas (Bonus - 5 puntos extra)

1. **¿Cuál es la diferencia entre una imagen y un contenedor en Docker?**
   ________________________________________________________________
   ________________________________________________________________

2. **Explica qué es el Docker Daemon y cómo interactúas con él:**
   ________________________________________________________________
   ________________________________________________________________

3. **¿Por qué es importante usar usuarios no-root en contenedores?**
   ________________________________________________________________
   ________________________________________________________________

4. **¿Cuándo usarías Docker Compose en lugar de comandos docker individuales?**
   ________________________________________________________________
   ________________________________________________________________

5. **¿Qué sucede con los datos almacenados en un contenedor cuando lo eliminas?**
   ________________________________________________________________
   ________________________________________________________________

---

## Entrega

### Formato de Entrega:
- [ ] Documento con todos los comandos completados
- [ ] Capturas de pantalla mostrando los resultados
- [ ] Archivos creados (Dockerfile, docker-compose.yml, HTML, etc.)
- [ ] Explicaciones de los conceptos solicitados

### Criterios de Evaluación:

**Comandos Básicos (15 pts):**
- Sintaxis correcta: 5 pts
- Explicaciones claras: 10 pts

**Gestión de Contenedores (20 pts):**
- Uso correcto de run, start, stop: 15 pts
- Comprensión de diferencias: 5 pts

**Comunicación (20 pts):**
- Mapeo de puertos correcto: 10 pts
- Ejecución de comandos: 10 pts

**Volúmenes (20 pts):**
- Implementación correcta: 15 pts
- Comprensión conceptual: 5 pts

**Docker Compose (15 pts):**
- Archivo yml funcional: 10 pts
- Comandos correctos: 5 pts

**Imagen Personalizada (10 pts):**
- Dockerfile correcto: 7 pts
- Construcción exitosa: 3 pts

### Notas Adicionales:
- Los comandos deben ser funcionales y estar probados
- Se valorará la documentación clara y ordenada
- Las capturas de pantalla deben mostrar los resultados exitosos
- Se permite consultar documentación oficial de Docker

**Fecha de entrega:** ________________________  
**Medio de entrega:** ________________________