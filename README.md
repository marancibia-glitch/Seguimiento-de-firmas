# Seguimiento de Firmas de Contratos

Panel de control de los contratos emitidos semanal y mensualmente, para que cada
responsable persiga las firmas pendientes de su personal. Meta: 100% de firmas.

Publicado con GitHub Pages: **https://marancibia-glitch.github.io/Seguimiento-de-firmas/**

## Advertencia sobre los datos

**Esta página es pública y no tiene contraseña.** GitHub Pages no permite ponerle una:
sirve archivos estáticos y el sitio es accesible para cualquiera que tenga la dirección.

El archivo `datos.json` lleva todos los registros, **incluidos RUT, teléfono particular y
correo personal**. Esas tres columnas no se muestran en pantalla, pero se obtienen abriendo
`datos.json` directamente o exportando el CSV.

Consecuencia práctica: **no difundas la dirección fuera de la empresa.** Se añadió
`noindex` y `robots.txt` para que los buscadores no lo indexen, pero eso no impide el
acceso a quien tenga el enlace.

Si en algún momento se necesita control de acceso real, hay que volver a un servidor
(la versión con clave está en el repositorio privado `Seguimiento-Firmas`).

## Cómo se actualizan los datos

**Solo, cada mañana.** Un script en Google Apps Script busca el correo diario
"BUK | Seguimiento de Firmas", extrae el Excel adjunto, lo convierte a `datos.json` y lo
sube a este repositorio. GitHub Pages republica y el panel queda al día. Corre en la nube
de Google, así que funciona con el computador apagado.

El panel muestra abajo la fecha de la última actualización.

La configuración de todo eso está en `automatizacion/` (fuera de este repositorio).

**Si la actualización falla,** el panel conserva los datos anteriores — nunca queda en
blanco — y llega un correo de aviso.

**Botón ⟳ Actualizar panel:** vuelve a leer los datos publicados sin recargar la página.
Sirve para traer lo último si el panel quedó abierto desde antes de la actualización de la
mañana. Si ya estabas al día, lo dice.

No hay carga manual de archivos: los datos los publica la automatización.

## Exportar a Excel

El botón **⬇ Exportar a Excel (filtrado)** descarga lo que estés viendo en la tabla, con
los filtros aplicados, en un `.xlsx`.

El archivo reproduce **las mismas 20 columnas del reporte de BUK, en el mismo orden**,
incluida la columna `Responsable` que se agregó al final el 24/08/2026. Así sirve igual que
el archivo de origen.

Se genera sin librerías externas (un `.xlsx` es un ZIP con XML), para no cargar los 875 KB
que pesaba la librería de Excel frente a los 95 KB de todo el panel.

## Enlaces por responsable

Añadiendo `?viewer=<Nombre Supervisor>` a la dirección, el panel muestra solo el personal
de esa persona y agrupa el cumplimiento por cliente:

```
https://marancibia-glitch.github.io/Seguimiento-de-firmas/?viewer=Romina%20Alvarez
```

El nombre debe coincidir con la columna "Nombre Supervisor". Si no coincide, aparece
"Enlace no válido".

**Esto no restringe el acceso.** Es una comodidad para que cada responsable entre directo
a lo suyo. Todos los registros siguen dentro de la página, así que cualquiera puede ver el
total quitando el parámetro.

## Cómo se calcula el cumplimiento

`firmados / (firmados + no firmados)`. Los registros "No Requiere Firma" quedan fuera del
denominador para que no alteren el porcentaje.

Semáforo: verde ≥ 90% · amarillo 75–89% · rojo < 75%.

## Contactos y correos

El botón **✉ Contactos y correo** guarda el correo y el enlace de cada responsable y arma
un mensaje de recordatorio. Se guarda en el `localStorage` del navegador, así que solo
existe en el equipo donde lo escribas y no viaja con la página.

## Estructura

| Archivo | Para qué |
|---|---|
| `index.html` | El panel: interfaz y cálculos (95 KB) |
| `datos.json` | Los datos. Es el único archivo que reescribe la actualización diaria |
| `robots.txt` | Pide a los buscadores que no indexen |
| `.nojekyll` | Evita que GitHub Pages procese el sitio con Jekyll |

Los datos van aparte del panel a propósito: así la actualización diaria solo reescribe un
archivo de datos en vez de regenerar el HTML completo.
