# Aplicación de Login con SharedPreferences

Esta aplicación Android demuestra el uso de SharedPreferences para almacenar y recuperar datos de usuario de forma persistente.

## Características

- **Pantalla de Login**: Interfaz moderna y atractiva con Material Design
- **Validación de Campos**: Verifica que todos los campos estén completos
- **Simulación de Autenticación**: Valida credenciales básicas (admin/123456)
- **Persistencia de Datos**: Utiliza SharedPreferences para guardar el nombre de usuario
- **Funcionalidad "Recordarme"**: Checkbox opcional para controlar si se guarda el usuario
- **Recuperación Automática**: El nombre de usuario se carga automáticamente al reiniciar la app

## Funcionalidades Implementadas

### 1. Pantalla de Inicio de Sesión
- Campo para nombre de usuario
- Campo para contraseña (con toggle de visibilidad)
- Checkbox "Recordarme"
- Botón de inicio de sesión
- Indicador de estado (éxito/error)

### 2. Validación de Credenciales
- Verifica que los campos no estén vacíos
- Simula validación de credenciales (usuario: "admin", contraseña: "123456")
- Muestra mensajes de error apropiados

### 3. Persistencia con SharedPreferences
- Guarda el nombre de usuario cuando "Recordarme" está marcado
- Recupera automáticamente el usuario al abrir la aplicación
- Limpia los datos guardados cuando se desmarca "Recordarme"

### 4. Experiencia de Usuario
- Interfaz moderna con Material Design
- Mensajes de estado con colores apropiados
- Toast de bienvenida al iniciar sesión exitosamente
- Auto-ocultamiento de mensajes de estado

## Cómo Usar

1. **Primera vez**: Ingresa cualquier nombre de usuario y contraseña "123456"
2. **Marcar "Recordarme"**: Para que el usuario se guarde automáticamente
3. **Cerrar y abrir la app**: El nombre de usuario aparecerá automáticamente
4. **Desmarcar "Recordarme"**: Para limpiar los datos guardados

## Credenciales de Prueba

- **Usuario**: admin
- **Contraseña**: 123456

## Estructura del Proyecto

```
app/src/main/
├── java/com/example/sharedpreferences/
│   └── MainActivity.java          # Lógica principal de la aplicación
├── res/
│   ├── layout/
│   │   └── activity_main.xml      # Layout de la pantalla de login
│   ├── values/
│   │   ├── colors.xml            # Definición de colores
│   │   └── strings.xml           # Strings de la aplicación
│   └── drawable/
│       └── ic_launcher_*.xml     # Iconos de la aplicación
```

## Tecnologías Utilizadas

- **Android SDK**: Para desarrollo nativo
- **Material Design**: Para componentes de UI modernos
- **SharedPreferences**: Para persistencia de datos
- **ConstraintLayout**: Para layout responsivo
- **Java**: Lenguaje de programación

## Compilación y Ejecución

1. Abre el proyecto en Android Studio
2. Sincroniza las dependencias de Gradle
3. Conecta un dispositivo Android o inicia un emulador
4. Presiona "Run" para compilar y ejecutar la aplicación

## Notas Técnicas

- **SharedPreferences**: Se utiliza para almacenar datos de forma persistente
- **Validación**: Simulación básica de autenticación (en producción se conectaría a una base de datos)
- **UI/UX**: Interfaz moderna siguiendo las guías de Material Design
- **Compatibilidad**: Mínimo SDK 24 (Android 7.0) 