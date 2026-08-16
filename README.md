# 🎌 Crunchyroll Account Checker

Herramienta para verificar cuentas de Crunchyroll y detectar suscripciones premium. Basada en el script .svb original de **@PROO_IS_BACK**.

## ✨ Características

- ✅ Verificación de cuentas Crunchyroll
- 🌟 Detección de cuentas Premium vs Free
- 📊 Información detallada de suscripción (plan, precio, ciclo de facturación)
- 🌍 Detección de país de la cuenta
- 📱 Compatible con Termux (Android)
- 🚀 Sin necesidad de proxies (con uso moderado)
- 🎨 Interfaz colorida en terminal

## 📋 Requisitos

- Python 3.7 o superior
- Conexión a Internet

## 🔧 Instalación en Termux

### 1. Instalar Termux
Descarga Termux desde [F-Droid](https://f-droid.org/packages/com.termux/) o Google Play Store.

### 2. Actualizar paquetes
```bash
pkg update && pkg upgrade -y
```

### 3. Instalar Python y Git
```bash
pkg install python git -y
```

### 4. Clonar el repositorio
```bash
git clone https://github.com/TU_USUARIO/crunchyroll-checker.git
cd crunchyroll-checker
```

### 5. Instalar dependencias
```bash
pip install -r requirements.txt
```

## 🚀 Uso

### 1. Preparar archivo de combos
Crea un archivo de texto (por ejemplo `combos.txt`) con el formato:
```
email1@example.com:password123
email2@example.com:pass456
email3@example.com:mypass789
```

### 2. Ejecutar el checker
```bash
python crunchyroll_checker.py
```

### 3. Seguir las instrucciones
- Ingresa el nombre del archivo de combos
- Espera los resultados

## 📁 Archivos de salida

- **premium.txt**: Cuentas premium con información detallada
- **free.txt**: Cuentas gratuitas

## 📝 Ejemplo de uso

```bash
$ python crunchyroll_checker.py

╔═══════════════════════════════════════════════════════╗
║            CRUNCHYROLL ACCOUNT CHECKER                ║
║              Basado en script de @PROO_IS_BACK        ║
╚═══════════════════════════════════════════════════════╝

[?] Ingresa el nombre del archivo de combos: combos.txt

[INFO] Cargados 50 combos
[INFO] Iniciando verificación...

[1/50] Verificando: test@example.com ★ PREMIUM [Mega Fan Pack | 9.99USD]
[2/50] Verificando: user@example.com ◆ FREE [Country: US]
[3/50] Verificando: fake@example.com ✗ INVÁLIDA
...
```

## ⚙️ Funcionamiento

La herramienta replica exactamente la lógica del archivo .svb original:

### 1. **Autenticación**
- Usa la API oficial de Crunchyroll: `beta-api.crunchyroll.com/auth/v1/token`
- Envía credenciales con client_id y client_secret oficiales
- Obtiene access_token si las credenciales son válidas

### 2. **Información de cuenta**
- Consulta: `beta-api.crunchyroll.com/accounts/v1/me`
- Obtiene: email_verified, phone, external_id

### 3. **Beneficios de suscripción**
- Consulta: `beta-api.crunchyroll.com/subs/v1/subscriptions/{id}/benefits`
- Detecta: país, tipo de plan (Fan Pack, Mega Fan Pack, Ultimate Fan Pack)

### 4. **Productos de suscripción**
- Consulta: `beta-api.crunchyroll.com/subs/v1/subscriptions/{id}/products`
- Determina: Premium vs Free, precio, ciclo de facturación, free trial

## 🎯 Tipos de planes detectados

| Concurrent Streams | Plan |
|-------------------|------|
| 1 stream | Fan Pack |
| 4 streams | Mega Fan Pack |
| 6 streams | Ultimate Fan Pack |

## 💰 Ciclos de facturación

| Código | Descripción |
|--------|-------------|
| P1D | Daily (Diario) |
| P1W | Weekly (Semanal) |
| P1M | Monthly (Mensual) |
| P3M | 3 Months (3 Meses) |
| P1Y | Annual (Anual) |

## 🔒 Sobre Proxies

El archivo .svb original tiene `"NeedsProxies": true`, pero en la práctica:

- ✅ **No son estrictamente necesarios** para uso moderado
- ⚠️ **Recomendados** si verificas muchas cuentas (100+)
- 🚫 **Crunchyroll puede rate-limit** sin proxies en uso intensivo

**Consejos:**
- Usa delays entre peticiones (ya implementado: 1-3 segundos)
- No verifiques más de 50-100 cuentas por sesión sin proxies
- Espera entre ejecuciones si ves muchos errores

## 📊 Formato de resultados

### premium.txt
```
user@example.com:password123
  Plan: Mega Fan Pack | Price: 9.99USD | Cycle: Monthly | Country: US

premium@example.com:pass456
  Plan: Ultimate Fan Pack | Price: 14.99USD | Cycle: Annual | Country: JP
  ⚠ Free Trial Active
```

### free.txt
```
free@example.com:password | Country: US
another@example.com:pass123 | Country: GB
```

## 🐛 Solución de problemas

### Error: "Module not found"
```bash
pip install -r requirements.txt --upgrade
```

### Error: "Permission denied"
```bash
chmod +x crunchyroll_checker.py
```

### Muchos errores de "Timeout"
- Verifica tu conexión a Internet
- Reduce la velocidad (aumenta delays)
- Considera usar proxies

### Errores de rate limiting
- Espera 5-10 minutos entre ejecuciones
- Reduce el número de cuentas por sesión
- Usa proxies para grandes volúmenes

## ⚠️ Advertencias

- Esta herramienta es solo para fines educativos y de prueba
- No uses esta herramienta para acceder a cuentas sin autorización
- El uso indebido puede violar los términos de servicio de Crunchyroll
- El autor no se hace responsable del mal uso de esta herramienta

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.

## 👤 Créditos

- Script original (.svb): **@PROO_IS_BACK**
- Adaptación a Python: Comunidad

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📧 Soporte

Si tienes problemas o preguntas, abre un issue en GitHub.

---

**Nota**: Esta herramienta replica la funcionalidad del archivo .svb original usando las mismas APIs de Crunchyroll sin modificaciones en la lógica.
