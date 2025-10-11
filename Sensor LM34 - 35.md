### **Sensor LM35 (Escala Celsius)**

- **Rango de medición:** **-55°C a +150°C**
- **Cómo funciona:** El LM35 está calibrado para dar una salida de **10 mV por cada grado Celsius**.
    - A **0°C**, la salida es **0 mV**.
    - A **+25°C**, la salida es **+250 mV**.
    - A **-10°C**, la salida es **-100 mV**.


## **Fórmulas Fundamentales:**
##### Caso Básico:
$$T(°C) = \frac{V_{out}}{0.010} = V_{out} \times 100$$
### **Conversión Directa:**
$$Vout(mV) = 10 × T(°C)$$
$$T(°C) = \frac{Vout(mV)}{10}$$
### **Conversión a Fahrenheit:**
$$T(°F) = (T(°C) \times \frac{9}{5}) + 32$$
$$Vout(mV) = ((T(°F) - 32) \times \frac{5}{9}) \times 10$$
## **Resumen de Fórmulas con ADC**

| Configuracion | Fórmula con ADC                                    | Variables             |
| ------------- | -------------------------------------------------- | --------------------- |
| Directo       | $T(°C) = \frac{ADC × Vref}{Res} × 100$             | Res = 1024, Vref = 5V |
| Con Offset    | $T(°C) = (\frac{ADC × Vref}{Res} - Voffset) × 100$ | Voffset = 2.5V        |

## **¿Qué es la Resolución del ADC?**

| Tipo de ADC                  | Bits    | Resolución (niveles) | Fórmula    |
| ---------------------------- | ------- | -------------------- | ---------- |
| Arduino estándar             | 10 bits | **1024**             | 2¹⁰ = 1024 |
| Microcontroladores avanzados | 12 bits | **4096**             | 2¹² = 4096 |
| Sistemas simples             | 8 bits  | **256**              | 2⁸ = 256   |
## **¿Por qué usamos la Resolución en la fórmula?**

Para convertir el **valor digital** del ADC a **voltaje real**:

$$Voltaje = \frac{Valor_{ADC} \times V_{ref}}{Resolución}$$

### **Sensor LM34 (Fahrenheit)**

- **Voltaje alimentación:** 4V a 30V
- **Tipo:** Sensor de temperatura analógico de precisión
- **Rango de temperatura:** **-50°F a +300°F** (-45°C a +149°C)
- **El LM34 está calibrado para dar una salida de _10 mV por cada grado Fahrenheit_**
	- +70°F  →  700 mV  (0.70V)
	- +100°F →  1000 mV (1.00V)  
	- +32°F  →  320 mV  (0.32V)
#### **Fórmulas Fundamentales**

 **Relación Voltaje-Temperatura:**
$$Vout(mV) = 10 \times T(°F)$$
$$T(°F) = \frac{Vout(mV)}{10}$$
### **Conversión a Celsius:**

$$T(°C) = (T(°F) - 32) \times \frac {5}{9}$$
$$Vout(mV) = (T(°C) \times 18) + 320$$
### **Fórmulas con ADC0831:**

**Voltaje de entrada al ADC:**
$$Vadc = \frac{(ValorDigital \times Vref)}{255}$$
**Temperatura desde valor digital:**
$$T(°F) = \frac{(ValorDigital \times Vref \times 1000)}{(255 × 10)}$$
 **Resolución del sistema:**
 
Resolución = (V_ref × 1000) / (255 × 10) ≈ 1.96°F por bit