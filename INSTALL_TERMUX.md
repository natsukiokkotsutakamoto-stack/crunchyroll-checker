# 📱 Guía de Instalación en Termux - Crunchyroll Checker

Esta es una guía paso a paso para instalar y usar el **Crunchyroll Checker** en Termux (Android).

## 🔧 Instalación Rápida

Copia y pega estos comandos uno por uno en Termux:

### Paso 1: Actualizar Termux
```bash
pkg update && pkg upgrade -y
```

### Paso 2: Instalar Python y Git
```bash
pkg install python git -y
```

### Paso 3: Clonar el repositorio
```bash
git clone https://github.com/TU_USUARIO/crunchyroll-checker.git
```

### Paso 4: Entrar al directorio
```bash
cd crunchyroll-checker
```

### Paso 5: Instalar dependencias
```bash
pip install -r requirements.txt
```

### Paso 6: Dar permisos de ejecución
```bash
chmod +x crunchyroll_checker.py
```

## 🚀 Uso

### 1. Crear archivo de combos
Crea un archivo llamado `combos.txt` con tus cuentas:

```bash
nano combos.txt
```

Escribe tus combos en formato `email:password` (uno por línea):
```
cuenta1@example.com:password123
cuenta2@example.com:pass456
cuenta3@example.com:mipass789
```

Guarda el archivo:
- Presiona `Ctrl + X`
- Presiona `Y`
- Presiona `Enter`

### 2. Ejecutar el checker
```bash
python crunchyroll_checker.py
```

### 3. Seguir las instrucciones
1. Ingresa el nombre del archivo de combos: `combos.txt`
2. Espera los resultados

## 📊 Resultados

Los resultados se guardan automáticamente en:
- **premium.txt**: Cuentas premium con detalles
- **free.txt**: Cuentas gratuitas

Para ver los resultados:
```bash
cat premium.txt
cat free.txt
```

## 💡 Consejos

### Usar un editor más fácil
Si `nano` es complicado, puedes crear el archivo desde tu gestor de archivos de Android:

1. Abre tu gestor de archivos
2. Ve a: `Almacenamiento interno/Android/data/com.termux/files/home/crunchyroll-checker/`
3. Crea un archivo llamado `combos.txt`
4. Edítalo con cualquier editor de texto

### Copiar archivo desde tu teléfono
Si ya tienes un archivo de combos en tu teléfono:

```bash
# Dar permisos de almacenamiento a Termux
termux-setup-storage

# Copiar archivo desde Descargas
cp ~/storage/downloads/combos.txt ~/crunchyroll-checker/combos.txt
```

### Ver resultados en tiempo real
Para ver los archivos de resultados mientras se ejecuta:

```bash
# En otra sesión de Termux
cd crunchyroll-checker
tail -f premium.txt
```

## 🎯 Entender los Resultados

### Cuenta Premium
```
[5/50] Verificando: user@example.com ★ PREMIUM [Mega Fan Pack | 9.99USD]
```

En `premium.txt`:
```
user@example.com:password123
  Plan: Mega Fan Pack | Price: 9.99USD | Cycle: Monthly | Country: US
```

### Cuenta Free
```
[10/50] Verificando: free@example.com ◆ FREE [Country: US]
```

En `free.txt`:
```
free@example.com:password | Country: US
```

### Cuenta Inválida
```
[15/50] Verificando: fake@example.com ✗ INVÁLIDA
```

No se guarda en ningún archivo.

## 🐛 Solución de Problemas

### Error: "No module named 'requests'"
```bash
pip install requests colorama --upgrade
```

### Error: "Permission denied"
```bash
chmod +x crunchyroll_checker.py
```

### El script se cierra solo
- Verifica que el archivo `combos.txt` existe
- Verifica que el formato sea correcto (email:password)
- Verifica tu conexión a Internet

### Muchos errores de "Timeout"
- Asegúrate de tener Internet activo
- Intenta con WiFi en lugar de datos móviles
- Crunchyroll puede estar bloqueando temporalmente

### Rate Limiting (demasiadas peticiones)
- Espera 5-10 minutos entre ejecuciones
- Reduce el número de cuentas por sesión
- No verifiques más de 50-100 cuentas sin pausas

## 🔄 Actualizar la herramienta

Para obtener la última versión:

```bash
cd crunchyroll-checker
git pull
pip install -r requirements.txt --upgrade
```

## 📱 Comandos Útiles en Termux

```bash
# Ver archivos en el directorio actual
ls -la

# Ver contenido de un archivo
cat archivo.txt

# Editar un archivo
nano archivo.txt

# Limpiar la pantalla
clear

# Salir de Termux
exit
```

## ⚡ Script de Instalación Automática

Puedes usar este comando único para instalar todo:

```bash
pkg update -y && pkg install python git -y && git clone https://github.com/TU_USUARIO/crunchyroll-checker.git && cd crunchyroll-checker && pip install -r requirements.txt && chmod +x crunchyroll_checker.py && echo "✅ Instalación completada! Ejecuta: python crunchyroll_checker.py"
```

## ⚠️ Sobre Proxies

El script original dice que necesita proxies (`NeedsProxies: true`), pero:

- ✅ **No son necesarios** para uso normal (menos de 50 cuentas)
- ⚠️ **Recomendados** para grandes volúmenes (100+ cuentas)
- 🚫 **Crunchyroll puede bloquear** si detecta demasiadas peticiones

**Consejos:**
- Usa delays entre verificaciones (ya implementado)
- No abuses del checker
- Espera entre ejecuciones

## 📞 Soporte

Si tienes problemas, abre un issue en: https://github.com/TU_USUARIO/crunchyroll-checker/issues

---

**¡Listo!** Ahora puedes verificar cuentas de Crunchyroll directamente desde tu teléfono Android con Termux.
