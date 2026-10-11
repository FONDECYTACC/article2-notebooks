# 06: diagnosticos ejecutados; decision pendiente
Fecha: 2026-10-04T19:45:20.002973-03:00
Estado: `investigator_review_required`. Celda: `cox-ph-tests-and-checkpoint`. Firma pendiente: `4bbfd50cae16`. Ninguna discrepancia de esta ejecucion fue aceptada automaticamente.
## 1. Que cambio y donde
Las seis cifras contrastadas de los modelos Full de eTable 10 cambian al redondeo de dos decimales. Son estadisticos chi-cuadrado del diagnostico de riesgos proporcionales (NPH); no son C-index, IBS ni precision predictiva. Las restantes filas SHAP de eTable 10 corresponden a etapas posteriores y no se han reproducido aqui.
| Desenlace / termino | Previo (Word) | Nuevo | Diferencia | Clasificacion |
|---|---:|---:|---:|---|
| Readmision / Global | 281,07 | 279,20 | -1,87 | Sustancial |
| Readmision / Egreso por incumplimiento / indeterminado | 60,65 | 60,66 | 0,01 | Sustancial |
| Readmision / Derivacion judicial | 43,08 | 43,01 | -0,07 | Sustancial |
| Mortalidad / Global | 178,78 | 180,14 | 1,36 | Sustancial |
| Mortalidad / Egreso por incumplimiento / indeterminado | 82,43 | 82,96 | 0,53 | Sustancial |
| Mortalidad / Diagnostico fisico (any_phys_dx) | 15,15 | 14,68 | -0,47 | Sustancial |
La comparacion usa directamente el Word indicado en config.yml y los resultados nuevos de R. Las seis p nuevas siguen por debajo de 0,001: conservan la categoria publicada de p y la evidencia de NPH en esas filas. No se infiere que todas las otras pruebas o las decisiones posteriores sean equivalentes.
## 2. Causa verificada
El mismo codigo, aplicado primero a la base antigua, reprodujo las seis cifras al redondeo publicado y el VIF de referencia: 13.036482851125, referencia 13.036483. Las diferencias residuales son triviales y estan enumeradas en control_ph de 06_cox_diagnostics_execution.json.
La comparacion de los ajustes antiguos y nuevos guardados confirma la misma muestra de 70.521 personas, tiempos e indicadores de evento, formulas, nombres de columnas y estratos. Cambian 15.308 celdas de la matriz codificada reducida en cada desenlace; este numero no representa participantes. El control de procedencia del notebook tambien confirma cero cambios en valores originalmente observados de las variables comprobadas. La diferencia surge al usar las nuevas bases imputadas de desarrollo. Este control no separa el efecto de cada detalle de la nueva imputacion frente a la variacion entre imputaciones.
## 3. Implicacion
En estas seis filas se mantiene la evidencia que motivo la correccion original de NPH. La decision original de colinealidad tambien se conserva: solo evaluacindelprocesoteraputico_logro_minimo supera VIF 10 en ambos modelos completos nuevos. El VIF mostrado es 13.0349 para readmision y 13.2006 para mortalidad. AICc y D1 de los modelos completo/reducido quedaron visibles en el notebook.
Todavia no se calcularon C-index, IBS, desempeno en holdout, figuras NPH nuevas ni ajustes finales estratificados. No se afirma que el modelo preferido o las cifras predictivas sigan iguales. Word permanece intacto.
## 4. Dos caminos
A. Recomendado: aceptar estas seis cifras nuevas como fuentes del pipeline, conservar el metodo original de NPH en la primera imputacion y continuar con las figuras y ajustes ya preparados. Estimacion actualizada: 3-5 minutos reutilizando los modelos guardados; cero nuevas imputaciones, tuning, SHAP o bootstrap. Las fuentes actualizadas quedan fuera del Word.
B. Antes de aceptar, comparar con mas detalle los residuos y los predictores cuyas imputaciones cambiaron, usando los ajustes guardados de la primera imputacion. Estimacion: 10-20 minutos para una auditoria acotada. No implica repetir imputacion ni ampliar NPH a cinco imputaciones. Si surge otro cambio sustancial, vuelve a requerir decision.
Se solicita la eleccion por la regla 6 del investigador: cambia una cifra al redondeo publicado, incluso cuando la interpretacion de estas pruebas se mantiene.
## Ejecucion y archivos
Tiempo medido: 88.860 segundos (1.48 minutos). Pico R: 1.763 GiB. Hilos nativos: 2; un trabajador. Se ajustaron 4 modelos de control y 20 modelos completos/reducidos (dos desenlaces, cinco imputaciones). No se ejecutaron remuestreos.
Se reutilizaron los datos preparados y la Tabla 1 aceptada. Se guardaron 24 ajustes, un objeto de asociaciones y la comparacion CSV. El informe completo es 06_cox_diagnostics_execution.json. La celda final ordinaria no se alcanzo por la pausa; este inventario proviene de una captura R del estado real despues de la detencion. Session info se ejecuto despues de la pausa.
| Archivo escrito en outputs | Bytes |
|---|---:|
| `outputs/objects/cox_historical_readmission_full_2026-10-04_1f699706bddf.rds` | 5155388 |
| `outputs/objects/cox_historical_readmission_reduced_2026-10-04_1f699706bddf.rds` | 5113081 |
| `outputs/objects/cox_historical_death_full_2026-10-04_1f699706bddf.rds` | 5123164 |
| `outputs/objects/cox_historical_death_reduced_2026-10-04_1f699706bddf.rds` | 5070071 |
| `outputs/objects/cox_predictor_associations_2026-10-04_1f699706bddf.rds` | 3718 |
| `outputs/objects/cox_readmission_full_imp1_2026-10-04_1f699706bddf.rds` | 5155984 |
| `outputs/objects/cox_readmission_full_imp2_2026-10-04_1f699706bddf.rds` | 1627745 |
| `outputs/objects/cox_readmission_full_imp3_2026-10-04_1f699706bddf.rds` | 1627067 |
| `outputs/objects/cox_readmission_full_imp4_2026-10-04_1f699706bddf.rds` | 1627076 |
| `outputs/objects/cox_readmission_full_imp5_2026-10-04_1f699706bddf.rds` | 1627696 |
| `outputs/objects/cox_death_full_imp1_2026-10-04_1f699706bddf.rds` | 5119359 |
| `outputs/objects/cox_death_full_imp2_2026-10-04_1f699706bddf.rds` | 1612974 |
| `outputs/objects/cox_death_full_imp3_2026-10-04_1f699706bddf.rds` | 1612201 |
| `outputs/objects/cox_death_full_imp4_2026-10-04_1f699706bddf.rds` | 1612561 |
| `outputs/objects/cox_death_full_imp5_2026-10-04_1f699706bddf.rds` | 1612433 |
| `outputs/objects/cox_readmission_reduced_imp1_2026-10-04_1f699706bddf.rds` | 5110585 |
| `outputs/objects/cox_readmission_reduced_imp2_2026-10-04_1f699706bddf.rds` | 1627091 |
| `outputs/objects/cox_readmission_reduced_imp3_2026-10-04_1f699706bddf.rds` | 1626963 |
| `outputs/objects/cox_readmission_reduced_imp4_2026-10-04_1f699706bddf.rds` | 1626673 |
| `outputs/objects/cox_readmission_reduced_imp5_2026-10-04_1f699706bddf.rds` | 1627136 |
| `outputs/objects/cox_death_reduced_imp1_2026-10-04_1f699706bddf.rds` | 5075098 |
| `outputs/objects/cox_death_reduced_imp2_2026-10-04_1f699706bddf.rds` | 1612301 |
| `outputs/objects/cox_death_reduced_imp3_2026-10-04_1f699706bddf.rds` | 1612335 |
| `outputs/objects/cox_death_reduced_imp4_2026-10-04_1f699706bddf.rds` | 1611673 |
| `outputs/objects/cox_death_reduced_imp5_2026-10-04_1f699706bddf.rds` | 1612416 |
| `outputs/tables/eTable10_full_PH_comparison_2026-10-04_1f699706bddf.csv` | 785 |


## Decision accepted (2026-10-04T20:01:31.740246-03:00)
Option A was explicitly accepted for signature 4bbfd50cae16. The initial pending status above is historical. Follow the original sequential stratification decisions; see 06_cox_decisions.md. Figures and final Full-Cox fits are authorized, with unchanged sample and formulas. No Word changes.


## Diagnosticos completados; desempeno pendiente (2026-10-04T20:14:05.249700-03:00)
Se completo la opcion A respetando el orden original: estratos por modalidad, reduccion de colinealidad, diagnostico NPH en la primera imputacion, graficos y un nuevo estrato de egreso por incumplimiento/indeterminado. Se comprobaron los diez ajustes estratificados: 70.521 personas, 63 coeficientes y exactamente los dos estratos previstos. any_phys_dx, derivacion judicial y egreso administrativo por otras razones permanecen como coeficientes en estos modelos Full. Las comparaciones D1 auxiliares conservan los estratos originales y no se interpretan como pruebas del beneficio de estratificar.
La continuacion cientifica duro 72.334 segundos, con pico R 2.017 GiB, dos hilos y 20 nuevos ajustes; reutilizo los 24 ajustes previos. La verificacion de presentacion duro 39.375 segundos, pico R 1.484 GiB, cero ajustes nuevos. Las seis cifras NPH aceptadas son exactamente iguales a las del checkpoint. Las advertencias de interpolacion 'collapsing to unique x values' siguen visibles; no hubo errores de ejecucion.
Se corrigieron etiquetas cortadas y limites de dibujo de dos celdas graficas, conservando los datos y calculos. Los 47 objetos numericos se comprobaron identicos al reutilizarlos con firma 714a6937a159; los anteriores se mantienen como historial. Notebook 1622996 bytes; HTML 3850551 bytes. HTML renderizado sin ejecutar, codigo plegado, tablas con scroll, Session info y manifiesto final verificados.
Quedan pendientes C-index, IBS, CV, bootstrap y calibracion. Los motores exploratorios historicos siguen desactivados y requieren resolver su control de version/fuente numerica y su costo antes de ejecutarse. Este checkpoint no declara terminado el pipeline ni la evaluacion predictiva. No hubo modificaciones de Word ni del notebook original.
Fuentes vigentes: [eTable 10](../outputs/tables/eTable10_full_PH_comparison_2026-10-04_714a6937a159.csv), [eFigure 3A](../outputs/figures/eFigure3_panelA_full_PH_2026-10-04_714a6937a159.png), [eFigure 4A](../outputs/figures/eFigure4_panelA_full_PH_2026-10-04_714a6937a159.png). Inventario completo: 06_cox_completion_check.json.
