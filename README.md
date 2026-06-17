# MRT Executive Mining OS — Comité Ejecutivo Semanal

Sistema web ejecutivo para la gestión del Comité de Dirección semanal de MRT. Diseño estilo consultora internacional, operación completa en navegador sin servidor ni base de datos externa.

---

## Despliegue en GitHub Pages (5 pasos)

### 1. Crear repositorio en GitHub

1. Ir a [github.com/new](https://github.com/new)
2. Nombre sugerido: `mrt-comite-ejecutivo`
3. Visibilidad: **Privado** (recomendado para uso interno)
4. No inicializar con README (ya lo tienes)

### 2. Subir los archivos

Desde tu computadora, en la carpeta con estos archivos:

```bash
git init
git add .
git commit -m "MRT Executive OS — Initial deploy"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/mrt-comite-ejecutivo.git
git push -u origin main
```

> Reemplaza `TU-USUARIO` con tu usuario de GitHub.

### 3. Habilitar GitHub Pages

1. Ir al repositorio → **Settings** → **Pages**
2. En "Source", seleccionar: **GitHub Actions**
3. Guardar

El primer deploy se dispara automáticamente. En 2–3 minutos el sistema estará en:

```
https://TU-USUARIO.github.io/mrt-comite-ejecutivo/
```

### 4. Compartir con los directores

Enviar la URL a cada director con sus credenciales (ver tabla abajo).

### 5. Actualizaciones futuras

Cualquier `git push` a `main` redespliega automáticamente vía GitHub Actions.

---

## Primer Acceso — Configuración Inicial

La primera vez que alguien abre el sistema (o en cualquier dispositivo nuevo), aparece el **Asistente de Configuración** que solicita crear la cuenta de administrador:

1. Ingresar **nombre**, **email corporativo** y **contraseña** (mínimo 8 caracteres)
2. Confirmar la contraseña y hacer clic en **"Crear Administrador y Acceder"**
3. El administrador queda registrado y el sistema abre directamente

> Las contraseñas se almacenan con **hash SHA-256** — nunca en texto plano en el código ni en el navegador.

### Agregar Directores y Usuarios

Una vez dentro como Admin:

1. Ir a **Administración → Usuarios → + Nuevo Usuario**
2. Asignar rol **Director** y su sección correspondiente
3. Enviar las credenciales al director por canal seguro

| Rol | Qué puede hacer |
|-----|----------------|
| **Admin** | Todo: editar todas las secciones, gestionar usuarios, publicar reuniones |
| **Director** | Editar solo su sección, ver el resto en modo lectura |
| **Viewer** | Solo lectura — todas las secciones y el historial |

### Cambio de Contraseña

Cualquier usuario puede cambiar su propia contraseña desde el **menú lateral → "Cambiar Contraseña"** sin necesidad del administrador.

---

## Funcionalidades del Sistema

### Dashboard Ejecutivo
- KPIs consolidados de la semana actual
- Estado semáforo por área (VERDE / ÁMBAR / ROJO)
- Temas abiertos por nivel de prioridad
- Decision Board de la semana

### Reunión Semanal
- **Navegación por semana** — anterior / actual / siguiente
- **Secciones por Director** (2 min máx cada una):
  - Dirección General
  - Operaciones (OzEqAu, AISC)
  - Metalurgia
  - RRHH (Headcount, Vacantes)
  - Finanzas (Costo/Oz, Cash Flow)
- Cada sección registra: KPI Crítico, KPI Secundario, Riesgo, Apoyo Requerido, Acción/Decisión
- **Decision Board** — decisiones con impacto, deadline y owner
- **Acuerdos** — compromisos con responsable y plazo
- Estados: **Borrador** → **Publicado**
- Impresión / exportación nativa del navegador

### Seguimiento de Temas
- Registro de temas con prioridad (Alta / Media / Baja)
- Estados: Abierto / En Progreso / Cerrado / Diferido
- Contador de apariciones semana a semana
- Filtros por estado, prioridad, área y búsqueda
- Ordenamiento automático por prioridad y estado

### Historial
- Registro completo de reuniones
- Gráfico de temas más recurrentes
- Estadísticas por estado (publicadas / borradores)
- Acceso directo a cualquier semana pasada

### Administración (solo Admin)
- Alta, edición y baja de usuarios
- Asignación de rol y sección por director
- Sin límite de usuarios

---

## Arquitectura Técnica

- **Frontend:** HTML5 + CSS3 + JavaScript vanilla (sin frameworks)
- **Almacenamiento:** `localStorage` del navegador (datos por dispositivo)
- **Hosting:** GitHub Pages (estático, gratuito)
- **CI/CD:** GitHub Actions (deploy automático en push a `main`)
- **Sin servidor:** No requiere backend, base de datos ni configuración de red

> **Nota sobre datos:** Los datos se guardan en el navegador de cada usuario (`localStorage`). Si necesitas datos compartidos entre dispositivos en el futuro, el siguiente paso es integrar Firebase Firestore (gratuito hasta cierto volumen). Consulta con TI para esa migración.

---

## Agregar Nuevas Secciones de Director

Editar `index.html`, array `SECTIONS` cerca de la línea 280:

```javascript
const SECTIONS = [
  { id:'dg',          num:'01', label:'Dirección General',    sub:'Decisiones & Estrategia' },
  { id:'operaciones', num:'02', label:'Operaciones',           sub:'Producción / OzEqAu / AISC' },
  // Agregar nueva sección aquí:
  { id:'exploración', num:'06', label:'Exploración',           sub:'Sondeos / Recursos / Reservas' },
];
```

---

MRT Corporativo / Minería — Uso Interno Confidencial
