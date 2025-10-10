### **Sensor LM35 (Escala Celsius)**

- **Rango de medición:** **-55°C a +150°C**
    
- **Cómo funciona:** El LM35 está calibrado para dar una salida de **10 mV por cada grado Celsius**.
    
    - A **0°C**, la salida es **0 mV**.
        
    - A **+25°C**, la salida es **+250 mV**.
        
    - A **-10°C**, la salida es **-100 mV**.


## **Fórmulas Fundamentales por Sensor**
##### Caso Básico (Solo Temperaturas Positivas > 2°C)
$$T(°C) = \frac{V_{out}}{0.010} = V_{out} \times 100$$
##### **Caso General (Incluye Temperaturas Negativas):**

**Cuando usas alimentación dual (±V):**
$$T(°C) = V_{out} \times 100$$
**Cuando usas offset con alimentación simple:**
$$T(°C) = (V_{leído} - V_{offset}) \times 100$$

## **Resumen de Fórmulas con ADC**

| Configuracion |                                                |     |
| ------------- | ---------------------------------------------- | --- |
| Directo       | $T = \frac{ADC × Vref}{Res} × 100$             |     |
| Con Offset    | $T = (\frac{ADC × Vref}{Res} - Voffset) × 100$ |     |

## **¿Qué es la Resolución del ADC?**


| Tipo de ADC                  | Bits    | Resolución (niveles) | Fórmula    |
| ---------------------------- | ------- | -------------------- | ---------- |
| Arduino estándar             | 10 bits | **1024**             | 2¹⁰ = 1024 |
| Microcontroladores avanzados | 12 bits | **4096**             | 2¹² = 4096 |
| Sistemas simples             | 8 bits  | **256**              | 2⁸ = 256   |
