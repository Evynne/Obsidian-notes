El **BWT61CL** es un **sensor de ángulo de inclinación** de alta precisión que mide **inclinación en 2 ejes** (X e Y) usando tecnología MEMS.

### **Formato de Trama:**

AA 51 AXH AXL AYH AYL AZH AZL SUM

## **Estructura de la Trama (11 bytes)**

| Byte | Nombre | Descripción               |
| ---- | ------ | ------------------------- |
| 0    | HEADER | 0xAA (cabecera fija)      |
| 1    | CMD    | 0x51 (comando de lectura) |
| 2    | AXH    | Aceleración X High byte   |
| 3    | AXL    | Aceleración X Low byte    |
| 4    | AYH    | Aceleración Y High byte   |
| 5    | AYL    | Aceleración Y Low byte    |
| 6    | AZH    | Aceleración Z High byte   |
| 7    | AZL    | Aceleración Z Low byte    |
| 8    | TH     | Temperatura High byte     |
| 9    | TL     | Temperatura Low byte      |
| 10   | SUM    | Checksum                  |
## **Fórmulas de Conversión**

### **1. Conversión de Aceleración a g's**
$$valor_{16bits} = (AXH × 256) + AXL$$
$$Aceleración(g) = (valor_16_bits × 16) ÷ 32768$$
### **2. Conversión a Ángulo de Inclinación**
$$Ángulo(°) = arcsen(AceleraciónEje)$$
arcsen = asin
### **3. Para ángulos pequeños (<30°):**
$$Ángulo_X(°) ≈ Aceleración_X × 90$$
$$Ángulo_Y(°) ≈ Aceleración_Y × 90$$
### **4. Conversión de Temperatura**
$$Temperatura(°C) = (valor_{16bits} × 200) ÷ 32768 - 50$$

## **Cálculo de Checksum**
$$CHECKSUM = (AXL + AXH + AYL + AYH + AZL + AZH + TL + TH) & 0xFF$$