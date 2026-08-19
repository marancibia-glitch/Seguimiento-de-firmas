# Seguimiento de Firmas de Contratos

Panel de control de los contratos emitidos semanal y mensualmente, para que cada
responsable persiga las firmas pendientes de su personal. Meta: 100% de firmas.

Publicado con GitHub Pages: **https://marancibia-glitch.github.io/Seguimiento-de-firmas/**

## Advertencia sobre los datos

**Esta página es pública y no tiene contraseña.** GitHub Pages no permite ponerle una:
sirve archivos estáticos y el sitio es accesible para cualquiera que tenga la dirección.

El archivo `index.html` lleva los 692 registros incrustados, **incluidos RUT, teléfono
particular y correo personal**. Esas tres columnas no se muestran en pantalla, pero están
dentro de la página: se obtienen leyendo el código fuente o exportando el CSV.

Consecuencia práctica: **no difundas la dirección fuera de la empresa.** Se añadió
`noindex` y `robots.txt` para que los buscadores no lo indexen, pero eso no impide el
acceso a quien tenga el enlace.

Si en algún momento se necesita control de acceso real, hay que volver a un servidor
(la versión con clave está en el repositorio privado `Seguimiento-Firmas`).

## Cómo actualizar los datos

La fuente es `BBDD.xlsx`, hoja "Reporte Firma Contratos", con el encabezado en la fila 6.

**Para una revisión rápida solo tuya:** abre el panel y usa el botón
**⬆ Cargar reporte actualizado (.xlsx)**. Se recalcula todo al instante, pero el cambio
vive únicamente en tu navegador y desaparece al recargar. Nadie más lo ve.

**Para actualizar lo que ve todo el mundo:** hay que regenerar `index.html` con los datos
nuevos y subir el commit. Con GitHub Desktop: cambias el archivo, escribes un mensaje de
commit y pulsas **Push origin**. GitHub Pages republica solo en un par de minutos.

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
| `index.html` | El panel completo, autocontenido (datos + librería de lectura de Excel) |
| `robots.txt` | Pide a los buscadores que no indexen |
| `.nojekyll` | Evita que GitHub Pages procese el sitio con Jekyll |
