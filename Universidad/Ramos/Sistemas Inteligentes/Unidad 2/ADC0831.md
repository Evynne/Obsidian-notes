- **Resolución**: 8 bits (0-255)
- **Vref típico**: 5V
- **Resolución con 5V**: 19.61 mV
- **Interface**: Serial (3-wire)


| **Pin 1** | **Pin 2** | **Pin 3** | **Pin 4** | **Pin 5** | **Pin 6**   | **Pin 7** | **Pin 8** |
| :-------: | :-------: | --------- | --------- | --------- | ----------- | --------- | --------- |
|    /CS    |    Vin    | Vref      | GND       | Vout      | CLK (Clock) | Vcc (+5V) | /INTR     |
## **Fórmulas Clave**

### **1. Conversión Valor Digital → Voltaje**
$$Vout(V) = (valor_digital × Vref) ÷ 255$$
### **2. Para Vref = 5V:**
$$Vout(V) = valor_digital × 5 ÷ 255$$
### **3. Resolución con Vref = 5V:**
$$Resolución = 5V ÷ 255 ≈ 19.61 mV$$