# Blog Web con Django

Aplicación web de tipo blog donde los usuarios pueden registrarse, iniciar sesión y publicar artículos con imagen. Cada usuario administra sus propias publicaciones y tiene un perfil con avatar. Proyecto final de la Diplomatura en Python de CoderHouse.

## Tecnologías

- **Python 3.10+**
- **Django 5.2**: framework web
- **Pillow**: procesamiento de imágenes para posts y avatares
- **python-decouple**: lectura de configuración sensible desde el archivo `.env`
- **SQLite**: base de datos de desarrollo
- **HTML y CSS**: templates con herencia desde `base.html`

## Funcionalidades

**Publicaciones**
- Listado de posts, vista de detalle, creación, edición y eliminación desde la interfaz web.
- Imagen opcional en cada post. Si un post no tiene imagen, la página se muestra igual sin errores.
- Solo el autor de un post puede editarlo o eliminarlo.
- Buscador por título o contenido, con aviso cuando no hay resultados.

**Usuarios**
- Registro, inicio y cierre de sesión.
- Perfil de usuario editable con imagen de avatar opcional.
- La barra de navegación cambia según si el visitante es anónimo o tiene la sesión iniciada.

**Seguridad**
- Crear, editar y eliminar posts y editar el perfil requieren sesión iniciada. La protección está en las vistas (`@login_required` / `LoginRequiredMixin`), no solo en ocultar botones: si un visitante anónimo entra a esas URLs, se lo redirige al login.
- La clave secreta no está en el código: se lee desde un archivo `.env` que no se sube al repositorio.

## Estructura del proyecto

```
blog_config/   Configuración general (settings, urls principales)
posts/         App de publicaciones: modelos, vistas, formularios, templates
usuarios/      App de usuarios: registro, login, perfil
templates/     Template base compartido por todo el sitio
static/        Archivos CSS e imágenes estáticas
```

## Instalación

**1. Clonar el repositorio**
```bash
git https://github.com/Leanweimann/blog-django-coderhouse-pithon.git
```

**2. Crear y activar el entorno virtual**
```bash
python -m venv venv
```
- Windows (PowerShell / CMD): `venv\Scripts\activate`
- Windows (Git Bash): `source venv/Scripts/activate`
- Linux / macOS: `source venv/bin/activate`

**3. Instalar dependencias**
```bash
pip install -r requirements.txt
```

**4. Configurar las variables de entorno**

Copiar el archivo de ejemplo:
```bash
cp .env.example .env
```
Generar una clave secreta propia:
```bash
python -c "import secrets; print(secrets.token_urlsafe(50))"
```
Abrir `.env` y pegar la clave generada en `SECRET_KEY`. Sin este paso el proyecto no arranca.

**5. Crear la base de datos**
```bash
python manage.py migrate
```

**6. (Opcional) Crear un superusuario para el panel de administración**
```bash
python manage.py createsuperuser
```
El panel queda disponible en `http://127.0.0.1:8000/admin/`.

**7. Iniciar el servidor**
```bash
python manage.py runserver
```
Abrir `http://127.0.0.1:8000/` en el navegador.

## Cómo probarlo desde cero

El repositorio **no incluye** la base de datos (`db.sqlite3`) ni las imágenes subidas (`media/`), para que cada persona arranque con el proyecto limpio. Después de los pasos de instalación:

1. Entrar al sitio sin sesión e intentar crear un post: debe redirigir al login.
2. Registrar un usuario nuevo e iniciar sesión.
3. Crear un post con imagen y otro sin imagen.
4. Editar y eliminar un post propio.
5. Usar el buscador con una palabra existente y con una inexistente.
6. Editar el perfil y cargar un avatar.
7. Cerrar sesión.

La carpeta `media/` se crea automáticamente al subir la primera imagen.

## Autor

**Leandro Weimann**
Diplomatura en Python — CoderHouse
GitHub: https://github.com/Leanweimann
