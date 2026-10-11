# 08 terminado: comparaciones completas
**Acción siguiente: revisar este cierre antes del siguiente notebook. Lectura: dos minutos.**
Estado comprobado: 2026-10-09T22:40:40-03:00.

1. **Ya no falta c+f ni eTable 12.** La calibración tiene sus 360 comparaciones; eTable 12 tiene las 84 filas por horizonte del manuscrito, con el método real indicado en cada fila. Se guardaron las 500 remuestras que faltaban.
2. **Se conservan b/e.** b es SHAP readmisión, sin interacciones, con estratos por modalidad y egreso. e es SHAP mortalidad, sin interacciones, con estratos por modalidad y comorbilidad física. Full mortalidad sigue disponible para compararlo; no se cambia su papel automáticamente.
3. **El control pasó.** Las 300 comparaciones de calibración que ya existían quedaron iguales. Los 53 trabajos anteriores de bootstrap quedaron intactos. No se omitieron participantes. La verificación independiente reconstruyó las cifras e intervalos desde los objetos guardados.
4. **Costo real de este cierre:** 31.08 minutos; pico R muestreado 17.17 GiB; seis procesos de un hilo. Fueron 37 celdas sin errores, 1.000 ajustes Cox para la calibración faltante y un trabajo nuevo de 500 remuestras. No se repitieron imputación, tuning ni TreeSHAP.

## Qué añade la calibración que faltaba

ICI mide el error de calibración: menor es mejor. La comparación completa deja menor ICI para b que para c en los cuatro horizontes. e también conserva menor ICI que f. Las otras métricas están en el notebook; no todas tienen que ordenar los modelos igual.

| Desenlace | Meses | Sin interacciones | Con interacciones |
|---|---:|---:|---:|
| Readmisión b/c | 6 | 0.006795 | 0.006949 |
| Readmisión b/c | 12 | 0.007799 | 0.007907 |
| Readmisión b/c | 36 | 0.009193 | 0.009380 |
| Readmisión b/c | 60 | 0.009506 | 0.009776 |
| Mortalidad e/f | 6 | 0.001675 | 0.001738 |
| Mortalidad e/f | 12 | 0.002614 | 0.002655 |
| Mortalidad e/f | 36 | 0.006429 | 0.006536 |
| Mortalidad e/f | 60 | 0.008816 | 0.009411 |

Son promedios de las veinte repeticiones, no intervalos bootstrap. Esto no aporta un motivo nuevo para cambiar las decisiones b/e. No demuestra que los modelos sean equivalentes.

## Diferencias frente al manuscrito: quedan visibles

1. **Qué cambió:** en eTable 12, 42 de 84 diferencias puntuales y 73 de 84 intervalos cambian al redondeo publicado. Las otras diferencias puntuales e intervalos se clasifican como triviales. No son otros tantos cambios de modelo.
2. **Ejemplo sustancial según tu regla:** Full readmisión menos c a 60 meses pasa de -0.000007 a +0.000001 en IBS. Cambia el signo; el nuevo valor sin redondear es +0.0000006830. La magnitud sigue siendo pequeña y no basta para promover las interacciones.
3. **Causa comprobada y límite:** la tabla nueva usa las predicciones del pipeline limpio y conserva las definiciones de cálculo originales. El generador de las remuestras también difiere del barrido histórico. [FALTA] separar cuánto aporta cada cambio previo. No se atribuye todo a la imputación.
4. **Cómo corregirlo:** A) conservar b/e y usar estas fuentes al revisar manualmente el suplemento, unos 10–15 minutos de lectura; B) añadir un estudio para aislar cada cambio, con costo de ejecución aún no medido. Recomendación: A. No se ejecutó B ni se modificó el Word.

[Tabla completa: antes, ahora y clasificación](../outputs/tables/eTable12_historical_complete_pairwise_2026-10-09_d15bfd971719.csv). [Control independiente](08_etable12_independent_verification.json).

## Qué significa cerrado

Este notebook terminó sus comparaciones solicitadas. El bootstrap conserva las predicciones guardadas: no repite toda la construcción del modelo. Los intervalos son por comparación; no corrigen toda la exploración previa. La imputación de development sigue siendo anterior a sus particiones internas, como se decidió y documentó. La calibración conserva el método original 20×5×5, sin añadir bootstrap por persona.

La nota histórica de eTable 12 debe distinguir las filas que censuran la muerte de las que la tratan como evento competidor. Las CIF históricas y las de primera transición quedan separadas. [Fuentes y explicación](08_etable12_source_audit.md).

La rama DeepSurv limpia y la evaluación posterior del holdout siguen fuera de este cierre. No se afirma que todo el pipeline ni su ejecución en una máquina limpia estén terminados.

## Archivos y trazabilidad

Se registraron 128 archivos escritos; el notebook termina con sus rutas relativas y tamaños. Los modelos y las matrices grandes quedan fuera del notebook. Su tamaño comprobado es 3.50 MiB.

| Elemento | Celda de 08 | Archivo relativo al proyecto |
|---|---|---|
| eTable 12: todas las comparaciones originales | p225-complete-historical-etable12 | outputs/tables/eTable12_historical_complete_pairwise_2026-10-09_d15bfd971719.csv |
| eTable 12: estimaciones IBS adicionales e intervalos | p225-complete-historical-etable12 | outputs/tables/eTable12_historical_complete_by_model_2026-10-09_d15bfd971719.csv |
| Calibración conjunta c+f | p225-prepare-joint-cf-calibration | outputs/objects/perf08_cal_aj_c_f_2026-10-09_ff0998e7f195.rds |
| 360 diferencias ICI/ECE/E:O, objeto calibration_pairwise | p225-paired-calibration-comparisons; p225-save-preparation-record | outputs/objects/pred225_preparation_2026-10-09_3d29285bc2d8.rds |
| Session info | p225-session-info | outputs/objects/SessionInfo_08_2026-10-09_223551_3d29285bc2d8.txt |

[Registro de ejecución](08_joint_cf_execution.json). [Verificación final](08_complete_verification.json). [Notebook](../notebooks/08_prediction225_converted_mod.ipynb). [HTML](../notebooks/08_prediction225_converted_mod.html).
