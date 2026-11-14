# AulaQR Campus · P-02C.3 · Área de Estudiantes y PIN docente

## Alcance

- **Administración:** mantiene el generador y el PIN de demostración `0086`. No se modifica su lógica.
- **Personal Docente:** conserva las cinco pestañas, filtros, impresión y exportación CSV; añade un PIN **demostrativo** `2027` antes de mostrar la vista.
- **Estudiantes:** `estudiantes/` permite escoger `Secundaria · PREPARA (EPJA)`, uno de los cinco grados y la sección disponible; muestra sus cinco bloques sabatinos, permite imprimir/descargar CSV y seleccionar cada asignatura para permanecer en el horario o acceder a AulaQR.
- Las dos consultas reutilizan la **misma** fuente `assets/horario-aprobado.json`. Si Administración aprueba y publica una nueva versión, ambas vistas la consultan al recargar el sitio.

## Rutas AulaQR

`assets/aulaqr-rutas.json` centraliza las URL específicas por asignatura. Inicialmente están definidas como `null`: **no se ha afirmado que existan páginas específicas publicadas para todas las asignaturas**. Al pulsar una clase sin ruta asociada, se informa y se ofrece un enlace separado al AulaQR original (sin presentarlo como lección de esa asignatura).

Antes de habilitar «Ir al AulaQR de la asignatura» debe verificarse y registrar la URL HTTPS real para cada asignatura. En fases futuras, las rutas deberán asociarse también a grado, sección y período, no únicamente a asignatura.

## Privacidad y seguridad

**Ambos PIN son demostrativos; no autentican a nadie ni restringen recursos en GitHub Pages.** Todas las páginas y los JSON de un repositorio público son visibles independientemente del PIN. Los docentes aparecen con inicial y apellido, una seudonimización parcial, no anonimización irreversible. No hay matrículas, nombres de estudiantes, calificaciones ni expedientes. Ninguna interacción registra o persiste datos institucionales.

## Publicación

Descomprimir el ZIP, crear una rama de desarrollo nueva desde `main`, cargar archivos preservando rutas, revisar la solicitud de cambios y fusionar **solo con aprobación**. No modificar `main` directamente. Ejecutar localmente con `python3 -m http.server 8000` desde la raíz, visitar `/`, `/personal-docente/` y `/estudiantes/`.

## Estado

`assets/horario-aprobado.json` conserva su estado original **BASE_DE_REVISION_NO_APROBADA**. La selección de un grupo no prueba inscripción del estudiante; es consulta pública informativa.

---

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
