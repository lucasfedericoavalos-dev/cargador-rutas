# Simulador de Absorción · notas de mantenimiento

## Hecho (octubre 2026)
1. **Excel sin internet**: si el proxy bloquea SheetJS (CDN), el simulador usa un lector/escritor de .xlsx propio
   (bloque `MiniXLSX` en el HTML). El CDN carga en segundo plano y ya no traba la apertura.
2. **Nada se pierde al cerrar**: el Simulador y el escenario en pantalla se guardan solos como borrador
   (`absorcion-borrador`). Si hay cambios sin guardar, aparece "● sin guardar", y antes de pisarlos te pide confirmación.
3. **Revisión antes de actualizar rutas**: muestra qué cambia antes de aplicar. Se puede volver a subir el mismo archivo.
4. **Detalle de una línea**: clic en "Hs / lote" muestra el cálculo operación por operación.
5. **Solapa Bases**: las bases por planta y los nombres "2026" / "2027 PEA" se editan en pantalla
   (`absorcion-bases`) y viajan dentro del archivo con "Guardar simulador actualizado".
6. **Aviso de datos distintos**: si abrís un simulador que trae rutas o bases distintas a las guardadas en tu
   navegador, te pregunta con cuáles seguir (antes ganaban siempre las del navegador, sin avisar).
7. **Informe del escenario**: botón "Informe Excel" (resumen, líneas y horas por centro) y "Imprimir / PDF".
8. Arreglos chicos: confirmación al borrar un escenario o al pisar uno con el mismo nombre; el escenario de ejemplo
   ya no reaparece si lo borrás; "Guardar simulador actualizado" genera un archivo limpio (antes copiaba las filas
   en pantalla y podía dar un error al abrirlo).

No cambiaron el cálculo, el formato de la plantilla de rutas ni las claves `absorcion-escenarios` / `absorcion-rutas`
(solo se les agregó un campo).

## Pendiente (a propósito; cambia cómo se leen los números cargados)
- Carga masiva: "1.5" se lee como 15 (se toma el punto como separador de miles), y un CSV con coma decimal se corre de columna.

## Para revisar con el dueño del cálculo (no se tocó)
- Las horas suman los centros de mano de obra (`-MO`) **y** los de máquina o sala. Si corren en paralelo, el total está inflado
  (en promedio, ~58 % de las horas por lote son de centros -MO).
- El $ es Σ (horas de cada operación × Tasa STD del centro), no (Cs MO Std + Cs CF Std) × lote.
