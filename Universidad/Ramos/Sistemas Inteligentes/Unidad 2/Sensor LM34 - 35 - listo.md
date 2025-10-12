## Sensor LM35 (Escala Celsius)

### Especificaciones Técnicas
- **Rango de medición:** -55°C a +150°
- **Salida:** 10 mV por cada grado Celsius
- **Precisión:** ±0.5°C a 25°C
- **Alimentación:** 4V a 30V

### Principio de Funcionamiento
El LM35 está calibrado para dar una salida de **10 mV por cada grado Celsius**:
- **0°C** → 0 mV
- **+25°C** → +250 mV
- **-10°C** → -100 mV

## **Fórmulas Fundamentales:**


#### Conversión Directa Voltaje-Temperatura
$$V_{out}(mV) = 10 \times T(°C)$$
$$T(°C) = \frac{V_{out}(mV)}{10} = V_{out}(V) \times 100$$
#### Conversión a Fahrenheit

$$T(°F) = (T(°C) \times \frac{9}{5}) + 32$$
$$V_{out}(mV) = ((T(°F) - 32) \times \frac{5}{9}) \times 10$$
#### Resumen de Fórmulas con ADC

| Configuración | Fórmula                                            | Variables típicas     |
| ------------- | -------------------------------------------------- | --------------------- |
| Directo       | $T(°C) = \frac{ADC × Vref}{Res} × 100$             | Res = 1024, Vref = 5V |
| Con Offset    | $T(°C) = (\frac{ADC × Vref}{Res} - Voffset) × 100$ | Voffset = 2.5V        |

## ¿Qué es la Resolución del ADC?

| Tipo de ADC                  | Bits    | Resolución (niveles) | Fórmula    |
| ---------------------------- | ------- | -------------------- | ---------- |
| Arduino estándar             | 10 bits | **1024**             | 2¹⁰ = 1024 |
| Microcontroladores avanzados | 12 bits | **4096**             | 2¹² = 4096 |
| Sistemas simples             | 8 bits  | **256**              | 2⁸ = 256   |
| ADC0831                      | 8 bits  | **256**              | 2⁸ = 256   |
## ¿Por qué usamos la Resolución en la fórmula?

Para convertir el **valor digital** del ADC a **voltaje real**:

$$Voltaje = \frac{Valor_{ADC} \times V_{ref}}{Resolución}$$
## Sensor LM34 (Escala Fahrenheit)

### Especificaciones Técnicas
- **Rango de medición:** -50°F a +300°F (-45°C a +149°C)
- **Salida:** 10 mV por cada grado Fahrenheit
- **Alimentación:** 4V a 30V

### Principio de Funcionamiento

El LM34 está calibrado para dar una salida de **10 mV por cada grado Fahrenheit**:
- **+70°F** → 700 mV (0.70V)
- **+100°F** → 1000 mV (1.00V)
- **+32°F** → 320 mV (0.32V)
### Fórmulas Fundamentales

#### Conversión Directa Voltaje-Temperatura
$$V_{out}(mV) = 10 \times T(°F)$$
$$T(°F) = \frac{V_{out}(mV)}{10}$$
#### Conversión a Celsius

$$T(°C) = (T(°F) - 32) \times \frac{5}{9}$$
$$V_{out}(mV) = (T(°C) \times 18) + 320$$
### Configuración con ADC0831 (8 bits)

**Voltaje de entrada al ADC:**
$$V_{adc} = \frac{ValorDigital \times V_{ref}}{255}$$
**Temperatura desde valor digital:**
$$T(°F) = \frac{ValorDigital \times V_{ref} \times 1000}{255 \times 10}$$
 **Resolución del sistema:**
 
Resolución = (V_ref × 1000) / (255 × 10) ≈ 1.96°F por bit