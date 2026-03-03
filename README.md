# 📊 Flujograma Operativo – Certificado E-14
## Sistema de Recepción Electoral · Cali, Valle del Cauca

---

## 📌 Descripción

Este componente React es un flujograma interactivo que documenta el diseño
completo del sistema de recepción, validación y control de actas electorales
(Certificado E-14) por mesa de votación.

Está pensado como guía visual para equipos de testigos electorales,
coordinadores de datos y desarrolladores que implementen el sistema en Google
Workspace (Forms + Sheets + Apps Script).

---

## 🗂️ Estructura del Flujograma

El flujograma está dividido en 6 fases secuenciales, cada una expandible
con un clic:

  FASE 1 · 🧱 Diseño de Datos
    - Entidad principal: Mesa
    - 8 campos estructurales (Municipio, Puesto, Número de mesa,
      Corporación, Estado, Foto, Testigo, Timestamp)
    - Clave única lógica: municipio + puesto + mesa + corporación
    - Ciclo de estados: Pendiente → Recibida → Validada / Rechazada

  FASE 2 · 🧩 Google Form – Recepción Oficial Certificado E-14
    - Sección 1: Identificación del testigo
        · Código de testigo (validado vs lista previa)
        · Número de celular
    - Sección 2: Clasificación estructural
        · Corporación, Municipio, Comuna, Puesto, Número de mesa
    - Sección 3: Evidencia
        · Fotografía del E-14 (obligatoria, solo imagen, máx 10MB)
        · Declaración de confirmación del testigo

  FASE 3 · 🧮 Google Sheets – Base Central
    - Columnas: ID, Timestamp, Testigo, Corporación, Municipio, Comuna,
      Puesto, Mesa, Ruta Imagen, Estado, Observaciones
    - Columna calculada: CLAVE_UNICA = Corporación_Puesto_Mesa
      Ejemplo: SENADO_SANTA_LIBRADA_12
    - Hoja MESA_MAESTRA con 1.058 mesas precargadas

  FASE 4 · ⚙️ Google Apps Script – Automatización
    - Validación automática de duplicados (decisión SÍ/NO por CLAVE_UNICA)
    - Clasificación automática de carpetas en Drive
    - Renombrado de archivos con nomenclatura estándar
    - Control de mesas faltantes: esperadas vs recibidas
    - Reportes de avance por comuna, por puesto y total faltantes

  FASE 5 · 📊 Dashboard + Control Anti-Sesgo
    - Panel: mesas esperadas, recibidas, duplicadas, faltantes, % cobertura
    - Regla 1: Sin edición manual de votos en hoja de recepción
    - Regla 2: Hoja separada para digitación de votos
    - Regla 3: Doble digitación con comparación automática por script

  FASE 6 · 🔐 Control de Roles
    - Administrador : edita estructura (máx. 2 personas)
    - Equipo        : solo lectura del dashboard
    - Testigos      : solo envío por formulario

---

## 🛠️ Tecnologías utilizadas

  - React (hooks: useState)
  - CSS-in-JS (estilos en línea, sin dependencias externas de estilo)
  - Sin librerías de UI adicionales
  - Compatible con cualquier entorno React (Vite, CRA, Next.js, etc.)

---

## 🚀 Cómo usar el componente

  1. Copia el archivo del componente en tu proyecto React.
  2. Importa y renderiza el componente:

       import E14Flowchart from './E14Flowchart';

       function App() {
         return <E14Flowchart />;
       }

  3. No requiere props. Toda la data está contenida en el componente.
  4. Haz clic en cualquier fase para expandir su contenido detallado.

---

## 🎨 Diseño

  Paleta de colores por fase:
    F1 – Dorado    #f5c842   Diseño de datos
    F2 – Teal      #00d9b8   Google Form
    F3 – Púrpura   #a78bfa   Google Sheets
    F4 – Azul      #60a5fa   Apps Script
    F5 – Verde     #4ade80   Dashboard
    F6 – Rojo      #f87171   Control de roles

  Fondo general   : #080e1a (azul marino oscuro)
  Superficie       : #0f1c30
  Tipografía base : DM Sans / system-ui

---

## 📐 Lógica de negocio clave

  Clave única irrepetible:
    municipio + puesto + número_de_mesa + corporación

  Ejemplo de CLAVE_UNICA en Sheets:
    SENADO_SANTA_LIBRADA_12

  Regla de duplicados (Apps Script):
    SI CLAVE_UNICA ya existe en la hoja → estado = "DUPLICADO"
    SI NO existe                         → estado = "RECIBIDO"

  Nomenclatura de archivos en Drive:
    {CORPORACION}_{PUESTO}_{MESA}.jpg
    Ejemplo: SENADO_SANTA_LIBRADA_12.jpg

---

## 📁 Estructura de carpetas en Google Drive

  /Certificados_E14/
    /Senado/
      /Santa_Librada/
        /Mesa_12/
          SENADO_SANTA_LIBRADA_12.jpg
      /...otros puestos.../
    /Camara/
      /...

---

## ✅ Checklist de implementación

  [ ] Diseñar modelo de datos en Sheets (FASE 1)
  [ ] Crear Google Form con las 3 secciones (FASE 2)
  [ ] Configurar columnas y CLAVE_UNICA en Sheets (FASE 3)
  [ ] Precargar MESA_MAESTRA con las 1.058 mesas
  [ ] Implementar Apps Script para duplicados y carpetas (FASE 4)
  [ ] Crear dashboard de métricas (FASE 5)
  [ ] Configurar permisos y roles en Google Workspace (FASE 6)

---

## 👤 Autor / Contexto
  Autor     : Luigiands -tech 
  Proyecto  : Recepción Oficial Certificado E-14
  Ciudad    : Cali, Valle del Cauca, Colombia
  Alcance   : 1.058 mesas de votación
  Plataforma: Google Workspace (Forms + Sheets + Drive + Apps Script)

---

## 📄 Licencia

  Uso interno del equipo electoral. No distribuir sin autorización.
