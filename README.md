# AulaQR Campus · Horario H-01.3 · Paquete de revisión

Dos rutas: `administracion/` (generador y selector de docentes guía, PIN **demostrativo** `0086`) y `personal-docente/` (solo consulta, filtros, impresión, CSV para Excel). Conserva las cinco pestañas originales.

## Flujo editorial

1. Administración configura los docentes guía y genera una propuesta.
2. Revisa choques, docentes pendientes, cobertura de asignaturas y disponibilidad real. No implica aprobación automática.
3. Pulsa **Descargar horario aprobado (JSON)**. El archivo se descarga localmente; no cambia el sitio.
4. Con autorización institucional y revisión de privacidad, reemplaza `assets/horario-aprobado.json` en una rama de desarrollo y crea un Pull Request.
5. Tras fusionar y desplegar, Personal Docente carga la misma versión JSON al abrir o actualizar la página. No usa localStorage.

## Riesgo de publicación

**NO SUBIR ESTA VERSIÓN CON NOMBRES A GITHUB PAGES HASTA APROBAR SU DIVULGACIÓN.** En GitHub Pages el PIN de 4 dígitos no es una medida de seguridad: cualquiera puede ver el código, el JSON y los datos docentes. Los botones de administrador no requieren un backend y pueden manipularse. Para uso restringido real se necesita autenticación en servidor, autorización por roles y almacenamiento privado. La primera verificación debe hacerse en un servidor local.

## Ejecución local

Desde la carpeta extraída: `python3 -m http.server 8000` y abrir `http://localhost:8000/`. No usar `file://` para la ruta docente, porque el navegador bloquea la carga fetch del JSON local.

El archivo inicial `horario-aprobado.json` es una **BASE_DE_REVISION_NO_APROBADA**, deliberadamente no se presenta como aprobación real. El generador solo permuta las asignaciones importadas y no conoce disponibilidad real. Pendientes heredados se conservan.


## Presentación pública de nombres docentes (P-02C.2a)

Esta edición muestra la inicial del primer nombre, punto y primer apellido (ejemplo: `A. Ovando`). En los casos de apellidos compuestos se conserva el conjunto (`P. de los Santos`). Los códigos `DOC-001` a `DOC-014` siguen identificando internamente a los docentes sin usar los nombres completos. La etiqueta de docente pendiente se mantiene sin inventar identidad.

**Advertencia:** Esta nomenclatura es una seudonimización parcial, no anonimización irreversible. Todos los archivos de GitHub Pages y los datos exportados son públicos, y el PIN de demostración no protege el código ni el JSON. Los horarios aún requieren validación y aprobación institucional.

No volver a subir la edición anterior P-02C.2, que contiene nombres completos.
