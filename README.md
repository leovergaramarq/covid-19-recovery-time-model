# Covid-19 Recovery Time Predictive Model

A supervised predictive Machine Learning model is implemented to predict the recovery time in Covid-19 infections. Particularly, a Linear Regression model is used. The model has been trained with $18,000$% cases of infections in Colombia that subsequently recovered from the disease. The used source dataset is [Casos positivos de COVID-19 en Colombia](https://www.datos.gov.co/Salud-y-Protecci-n-Social/Casos-positivos-de-COVID-19-en-Colombia-/gt2j-8ykr/data), from Datos Abiertos Colombia. See the full [Jupyter Notebook](https://github.com/leovergaramarq/covid-19-recovery-time-model/blob/main/model.ipynb) with the implementation.

## Dataset

|fecha reporte web|ID de caso  |Fecha de notificación|Código DIVIPOLA departamento|Nombre departamento|Código DIVIPOLA municipio|Nombre municipio|Edad|Unidad de medida de edad|Sexo|Tipo de contagio|Ubicación del caso|Estado|Código ISO del país|Nombre del país|Recuperado|Fecha de inicio de síntomas|Fecha de muerte|Fecha de diagnóstico|Fecha de recuperación|Tipo de recuperación|Pertenencia étnica|Nombre del grupo étnico|
|-----------------|------------|---------------------|----------------------------|-------------------|-------------------------|----------------|----|------------------------|----|----------------|------------------|------|-------------------|---------------|----------|---------------------------|---------------|--------------------|---------------------|--------------------|------------------|-----------------------|
|2022-02-09 00:00:00|5992708     |2022-01-21 00:00:00  |25                          |CUNDINAMARCA       |25754                    |SOACHA          |15  |1                       |M   |Comunitaria     |Casa              |Leve  |                   |               |Recuperado|2022-01-17 00:00:00        |               |2022-02-01 00:00:00 |2022-02-10 00:00:00  |Tiempo              |6                 |                       |
|2022-02-09 00:00:00|5992709     |2022-01-21 00:00:00  |66                          |RISARALDA          |66001                    |PEREIRA         |67  |1                       |M   |Comunitaria     |Casa              |Leve  |                   |               |Recuperado|2022-01-17 00:00:00        |               |2022-02-01 00:00:00 |2022-02-10 00:00:00  |Tiempo              |6                 |                       |
|2022-02-09 00:00:00|5992710     |2022-01-21 00:00:00  |15                          |BOYACA             |15001                    |TUNJA           |32  |1                       |F   |Relacionado     |Casa              |Leve  |                   |               |Recuperado|2022-01-17 00:00:00        |               |2022-02-01 00:00:00 |2022-02-10 00:00:00  |Tiempo              |6                 |                       |
|2022-02-09 00:00:00|5992711     |2022-01-21 00:00:00  |17                          |CALDAS             |17001                    |MANIZALES       |11  |1                       |F   |Comunitaria     |Casa              |Leve  |                   |               |Recuperado|2022-01-17 00:00:00        |               |2022-02-01 00:00:00 |2022-02-10 00:00:00  |Tiempo              |6                 |                       |

<img src="https://github.com/user-attachments/assets/40c0e4b1-db94-4f2d-a5df-1db8e4f20c87">

## Methodology

### Model

A Machine Learning Model is presented, aimed to predict the Recovery Time in Covid-19 cases. The chosen model is the Linear Regression, which is ideal, given the continuous nature of the variable of interest.

The model attempts to predict the Recovery Time in days, given the next input variables:

* Edad (age in years)
* Sex
  * S_F (1: female; 0: other)
  * S_M (1: male; 0: other)
* Type of Contagion
  * C_Comunitaria (1: community infection; 0: other)
  * C_Importado (1: imported case; 0: other)
  * C_Relacionado (1: related case; 0: other)
* Case treatment location
  * U_Casa (1: treated at home; 0: other)
  * U_Hospital (1: treated at hospital - not ICU; 0: other)
  * U_Hospital_UCI (1: treated at hospital with ICU; 0: other)
* Case severity
  * E_Grave (1: severe; 0: other)
  * E_Leve (1: slight; 0: other)
  * E_Moderado (1: moderate; 0: other)
* Ethnicity
  * P_Indígena (1: ethnicity indigenous; 0: other)
  * P_Negro (1: ethnicity black; 0: other)
  * P_Otro (1: ethnicity other; 0: other)
  * P_ROM (1: ethnicity ROM; 0: other)

### Hypothesis (Recovery Time vs Case Treatment Location)

* $H_0$: The type of care received (at home, hospital, or ICU) does not significantly affect recovery time.
```math
  H_0 = \beta_{U\_Casa} = \beta_{U\_Hospital} = \beta_{U\_Hospital\_UCI}
```

* $H_1$: The type of care received significantly affects recovery time.
```math
  H_1 = \beta_{U\_Casa} \neq 0 \ \ \lor \ \ \beta_{U\_Hospital} \neq 0 \ \ \lor \ \ \beta_{U\_Hospital\_UCI} \neq 0
```

## Results

### Heatmap of Correlations

<img src="https://github.com/user-attachments/assets/9ffdbc69-4198-4d8f-9c6b-93a86d8b577e">

### Model performance

* The model is not accurate enough when predicting recovery time. However, a mean absolute error of 5.5 days (37.2% respect to the average recovery time) is a good starting point for further analysis with more representative datasets.

<img src="https://github.com/user-attachments/assets/473c06f1-d1e9-4076-97f0-b23519adb2e7">

## Conclusion

* The results suggest that **people treated with ICU recover, in average, 3 days faster than average**, whereas **people treated in hospitals (without ICU) recover, in average, 1.2 days faster than average**. People treated at home have the average recovery time, as they represent a 99.92% of the cases.

* Despite that result, we conclude that the proposed hypotheses $H_0$ and $H_1$ cannot be validated, as the dataset is not representative enough for various Case Treatment Locations.

## Further research

Reach out the [research study](https://www.researchgate.net/publication/380818622_Implementacion_de_Modelo_de_Machine_Learning_para_Estimacion_de_Tiempo_de_Recuperacion_de_Covid-19) (spanish) made along with this analysis for more information.
