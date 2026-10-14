# Simulador de Absorción · notas de mantenimiento

## Hecho (octubre 2026)
- **Excel sin internet**: si el proxy bloquea SheetJS (CDN), el simulador usa un lector/escritor de .xlsx propio
  (bloque `MiniXLSX` en el HTML). Ahora el CDN carga en segundo plano y ya no traba la apertura de la página.
- **Nada se pierde al cerrar**: las líneas del Simulador y del escenario en pantalla se guardan solas como borrador
  (`localStorage` → `absorcion-borrador`). Si hay cambios que no guardaste con *Guardar*, aparece "● sin guardar", y antes de pisarlos te pide confirmación.
- **Revisión antes de actualizar rutas**: antes de reemplazar la base muestra qué cambia (códigos nuevos o que desaparecen,
  cambios de hs y $ por lote, celdas con texto, tasas en 0, impacto en el escenario). Ahora también se puede volver a subir el mismo archivo.
- **Detalle de una línea**: clic en "Hs / lote" muestra el cálculo operación por operación (horas de MO y de máquina por separado).

Las claves de `localStorage` existentes (`absorcion-escenarios`, `absorcion-rutas`), el formato de la plantilla
y el cálculo no cambiaron.

## Pendientes (ordenadas por impacto / esfuerzo)
3. **Rutas viejas pisan a las nuevas**: si alguien te manda un "simulador actualizado" y ya tenías rutas cargadas
   en tu navegador, se siguen usando las tuyas (solo cambia el texto de la cabecera). Conviene avisar y preguntar cuáles usar.
4. **Base 2026 / 2027 editable en pantalla**: hoy está fija en el código (`DATA.base`). Habría que hacerla editable
   y que viaje con "Guardar simulador actualizado".
5. **Exportar el comparativo del escenario** a Excel o PDF para mandarlo.

## Para revisar con el dueño del cálculo (no se tocó)
- Las horas suman los centros de mano de obra (`-MO`) **y** los de máquina o sala. Si corren en paralelo, el total está inflado
  (en promedio, ~58 % de las horas por lote son de centros -MO).
- El $ es Σ (horas de cada operación × Tasa STD del centro), no (Cs MO Std + Cs CF Std) × lote.
