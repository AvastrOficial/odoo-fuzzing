# odoo-fuzzing - Odoo Module Path Validator

**Odoo Module Path Validator** es un auditor de seguridad web especializado en Odoo que permite escanear automáticamente una instancia para detectar:

- 🔍 Módulos instalados y activos  
- 📁 Estructura de directorios expuesta  
- 🌐 Endpoints vulnerables conocidos  
- 🔐 Rutas críticas de administración  
- 🛡️ Vulnerabilidades históricas (CVE)  

---

## 🔄 Flujo de Ejecución

### 1. Inicialización
- Carga lista de **180+ módulos Odoo**

### 2. Generación de rutas
Cada módulo genera múltiples rutas:

```javascript
/modulo/static/
/modulo/static/src/js/
/modulo/controllers/
/modulo/views/
/modulo/models/
```

### 3. Peticiones concurrentes
- Uso de `Promise.all`
- Procesamiento en batches

### 4. Análisis de respuestas

| Código HTTP | Resultado |
|------------|----------|
| 200–299 | ✅ Activo |
| 301–308 | 🔄 Redirección |
| 403 | 🔒 Restringido |
| 404 | ❌ No existe |

### 5. Detección de vulnerabilidades
- CVE conocidos  
- Endpoints críticos  
- Path traversal  

---

## 🔧 Componentes Técnicos

### 📦 Módulos Odoo

| Categoría | Ejemplos |
|----------|---------|
| Core | base, web, mail |
| Negocio | sale, purchase |
| E-commerce | website |
| Servicios | helpdesk |
| Seguridad | auth_ldap |

---

### 📁 Rutas validadas

```javascript
/modulo/static/
/modulo/controllers/
/modulo/views/
/modulo/models/
/modulo/security/
/modulo/report/
/modulo/tests/
/modulo/__manifest__.py
```
### 🚨 Endpoints críticos
```javascript
/web
/web/login
/web/database/backup
/web/database/restore
/web/database/drop
/jsonrpc
/xmlrpc/2/object
/web/static/src/libs/../../../../etc/passwd
```
### 🛡️ Vulnerabilidades Detectadas
| Módulo  | CVE            | Tipo   | Severidad  |
| ------- | -------------- | ------ | ---------- |
| web     | CVE-2020-11678 | RCE    | 🔴 Crítica |
| base    | CVE-2021-45080 | SQLi   | 🔴 Crítica |
| website | CVE-2022-21368 | XSS    | 🔴 Crítica |
| payment | CVE-2022-21369 | Bypass | 🔴 Crítica |
| sale    | CVE-2021-45079 | Acceso | 🟡 Alta    |

### 📊 Estadísticas
- 📦 180+ módulos
- 📁 19 rutas por módulo
- 🌐 35+ endpoints
- ⚡ ~3455 peticiones
- ⏱️ 2–5 minutos
- 🎨 Visualización

| Color | Significado |
| ----- | ----------- |
| 🟢    | Activo      |
| 🟠    | Vulnerable  |
| 🔴    | Error       |
| 🟣    | Core        |

### 💾 Exportación JSON
```javascript
{
  "timestamp": "2024-01-01T12:00:00Z",
  "baseUrl": "https://example.com",
  "stats": {
    "total": 180,
    "active": 45,
    "vulnerable": 12
  }
}
```
### ⚙️ Configuración
| Parámetro    | Valor  |
| ------------ | ------ |
| Timeout      | 5000ms |
| Concurrencia | 3      |
| Protocolo    | HTTPS  |
