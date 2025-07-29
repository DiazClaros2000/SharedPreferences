# Explicación del Código - Login con SharedPreferences

## Estructura del Proyecto

### 1. Layout (activity_main.xml)

El layout utiliza **ConstraintLayout** y **Material Design Components** para crear una interfaz moderna:

```xml
<!-- Campos de entrada con Material Design -->
<com.google.android.material.textfield.TextInputLayout
    style="@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox"
    android:hint="@string/username_hint">
    
    <com.google.android.material.textfield.TextInputEditText
        android:id="@+id/etUsername"
        android:inputType="text" />
</com.google.android.material.textfield.TextInputLayout>
```

**Características del Layout:**
- **TextInputLayout**: Proporciona campos de entrada con estilo Material Design
- **Password Toggle**: Permite mostrar/ocultar la contraseña
- **CheckBox**: Para la funcionalidad "Recordarme"
- **MaterialButton**: Botón de login con estilo moderno
- **TextView de Estado**: Para mostrar mensajes de éxito/error

### 2. MainActivity.java

#### Constantes y Variables

```java
private static final String PREF_NAME = "LoginPrefs";
private static final String KEY_USERNAME = "username";
private static final String KEY_REMEMBER_ME = "remember_me";
```

- **PREF_NAME**: Nombre del archivo de SharedPreferences
- **KEY_USERNAME**: Clave para almacenar el nombre de usuario
- **KEY_REMEMBER_ME**: Clave para almacenar el estado del checkbox

#### Inicialización de SharedPreferences

```java
sharedPreferences = getSharedPreferences(PREF_NAME, Context.MODE_PRIVATE);
```

- **MODE_PRIVATE**: Solo la aplicación puede acceder a estos datos
- Se crea un archivo XML en `/data/data/com.example.sharedpreferences/shared_prefs/LoginPrefs.xml`

#### Carga de Datos Guardados

```java
private void loadSavedData() {
    boolean rememberMe = sharedPreferences.getBoolean(KEY_REMEMBER_ME, false);
    cbRememberMe.setChecked(rememberMe);
    
    if (rememberMe) {
        String savedUsername = sharedPreferences.getString(KEY_USERNAME, "");
        if (!TextUtils.isEmpty(savedUsername)) {
            etUsername.setText(savedUsername);
        }
    }
}
```

**Funcionamiento:**
1. Lee el estado del checkbox "Recordarme"
2. Si está marcado, carga el nombre de usuario guardado
3. Lo establece en el campo de texto automáticamente

#### Validación de Login

```java
private void performLogin() {
    String username = etUsername.getText().toString().trim();
    String password = etPassword.getText().toString().trim();
    
    if (TextUtils.isEmpty(username) || TextUtils.isEmpty(password)) {
        showError(getString(R.string.error_empty_fields));
        return;
    }
    
    if (validateCredentials(username, password)) {
        if (cbRememberMe.isChecked()) {
            saveUserData(username);
        } else {
            clearSavedData();
        }
        showSuccess(getString(R.string.success_login));
    } else {
        showError(getString(R.string.error_invalid_credentials));
    }
}
```

**Proceso de Validación:**
1. **Validación de Campos**: Verifica que no estén vacíos
2. **Validación de Credenciales**: Simula autenticación (admin/123456)
3. **Guardado Condicional**: Solo guarda si "Recordarme" está marcado
4. **Feedback Visual**: Muestra mensajes de éxito/error

#### Guardado de Datos

```java
private void saveUserData(String username) {
    SharedPreferences.Editor editor = sharedPreferences.edit();
    editor.putString(KEY_USERNAME, username);
    editor.putBoolean(KEY_REMEMBER_ME, true);
    editor.apply();
}
```

**SharedPreferences.Editor:**
- **putString()**: Guarda el nombre de usuario
- **putBoolean()**: Guarda el estado del checkbox
- **apply()**: Guarda los cambios de forma asíncrona

#### Limpieza de Datos

```java
private void clearSavedData() {
    SharedPreferences.Editor editor = sharedPreferences.edit();
    editor.remove(KEY_USERNAME);
    editor.putBoolean(KEY_REMEMBER_ME, false);
    editor.apply();
}
```

**Funciones:**
- **remove()**: Elimina una clave específica
- **putBoolean(false)**: Desmarca el checkbox
- Se ejecuta cuando se desmarca "Recordarme"

## Flujo de la Aplicación

### 1. Primera Apertura
```
App se inicia → loadSavedData() → No hay datos → Campos vacíos
```

### 2. Login Exitoso con "Recordarme"
```
Usuario ingresa datos → Validación exitosa → saveUserData() → Datos guardados
```

### 3. Reapertura de la App
```
App se inicia → loadSavedData() → Datos encontrados → Campo usuario lleno
```

### 4. Desmarcar "Recordarme"
```
Checkbox desmarcado → clearSavedData() → Datos eliminados
```

## Archivos de SharedPreferences

Los datos se almacenan en:
```
/data/data/com.example.sharedpreferences/shared_prefs/LoginPrefs.xml
```

**Contenido del archivo:**
```xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
    <string name="username">admin</string>
    <boolean name="remember_me" value="true" />
</map>
```

## Ventajas de SharedPreferences

1. **Simplicidad**: API fácil de usar
2. **Persistencia**: Los datos sobreviven al cierre de la app
3. **Eficiencia**: Acceso rápido a datos pequeños
4. **Seguridad**: Datos privados de la aplicación
5. **Automatización**: No requiere gestión manual de archivos

## Consideraciones de Seguridad

- **Contraseñas**: No se almacenan contraseñas en SharedPreferences
- **Datos Sensibles**: Solo se guarda información no crítica
- **Encriptación**: Para datos sensibles, usar EncryptedSharedPreferences

## Extensibilidad

El código está diseñado para ser fácilmente extensible:

1. **Más Campos**: Agregar nuevas claves para más datos
2. **Validación Compleja**: Conectar con base de datos real
3. **Encriptación**: Migrar a EncryptedSharedPreferences
4. **Múltiples Usuarios**: Implementar sistema de múltiples perfiles 