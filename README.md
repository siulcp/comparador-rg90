# Manual de Uso - Comparador de Planillas RG 90 DNIT Paraguay

Herramienta para comparar dos planillas Excel y detectar diferencias entre los comprobantes cargados en **Marangatu** y los registrados en tu **sistema contable**.

---

## ¿Qué hace?

Compara dos planillas y muestra tres resultados:

- **Solo en Marangatu:** comprobantes que están en Marangatu pero no en tu contabilidad.
- **Solo en Sistema Contable:** comprobantes que están en tu contabilidad pero no en Marangatu.
- **Discrepancias:** comprobantes que están en ambas planillas pero con diferencias en el **monto** o en la **fecha**.

---

## Cómo usarlo

### 1. Preparar las planillas
Exportá desde Marangatu el listado de compras o ventas del período. Hacé lo mismo desde tu sistema contable. Ambas deben estar en formato `.xlsx`, `.xls` o `.csv`, con una fila de encabezados en la primera fila.

### 2. Subir los archivos
Abrí la página en tu navegador. Vas a ver dos recuadros:
- Izquierda: **Planilla Marangatu**
- Derecha: **Planilla Sistema Contable**

Arrastrá cada archivo sobre su recuadro, o hacé clic para seleccionarlo desde tu equipo.

### 3. Mapear las columnas
Una vez cargados los archivos, aparecen cuatro listas desplegables. Seleccioná a qué columna de tus planillas corresponde cada campo:

- **N° Factura** (obligatorio)
- **RUC** (obligatorio)
- **Fecha** (recomendado)
- **Monto** (recomendado)

El sistema intenta auto-detectarlas según el nombre, pero verificá que la asignación sea correcta.

> Las columnas pueden tener nombres distintos en cada planilla; se mapean por separado.

### 4. Comparar
Hacé clic en **"🔍 Comparar"**. Los resultados aparecen abajo divididos en tres paneles.

---

## Cómo interpreta los datos

**Clave de comparación:** cada comprobante se identifica por la combinación **N° Factura + RUC**. Si esa combinación coincide en ambas planillas, se considera el mismo comprobante.

**Normalización automática:**
- **RUC:** elimina puntos, guiones y espacios. `80012345-6` y `800123456` se consideran iguales.
- **N° Factura:** elimina espacios al inicio/final.
- **Monto:** interpreta separadores de miles y decimales. `1.500.000,00` y `1500000` se consideran iguales.
- **Fecha:** se compara como texto. Ambas planillas deben usar el mismo formato.

**Lógica:**
- Si la clave **no existe** en la otra planilla → aparece como "Solo en..." la planilla correspondiente.
- Si la clave **existe** en ambas → se comparan monto y fecha. Si coinciden, no aparece. Si difieren, va a **Discrepancias**.

---

## Consideraciones para la RG 90

- **Montos con IVA incluido:** Marangatu declara los montos gravados con IVA incluido. Si tu sistema contable guarda los importes sin IVA, todas las facturas aparecerán como discrepancia. Verificá que ambas fuentes usen el mismo criterio.
- **Formato de fechas:** si una planilla usa `dd/mm/aaaa` y la otra `aaaa-mm-dd` o número de serie de Excel, se marcarán como discrepancias aunque la fecha sea la misma. Formateá ambas al mismo estilo antes de subir.
- **RUC con dígito verificador:** el sistema no valida el dígito verificador, solo compara el número normalizado.
- **Duplicados:** si hay facturas repetidas (mismo N° Factura + RUC), solo se conserva el último registro.
- **Comprobantes anulados:** si aparecen en una planilla pero no en la otra, se mostrarán como diferencias. Filtrálos antes de comparar si no querés verlos.

---

## Privacidad

Todo el procesamiento se realiza **en tu navegador**. Los archivos **no se suben a ningún servidor**, no se guardan y se eliminan al cerrar o recargar la página.

---

## Requisitos

- Navegador moderno (Chrome, Edge, Firefox, Safari).
- Conexión a internet solo la primera vez para cargar la librería SheetJS.
