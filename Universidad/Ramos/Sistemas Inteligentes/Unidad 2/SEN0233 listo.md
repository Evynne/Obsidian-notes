El **SEN0233** es un sensor de turbidez que mide la **cantidad de partículas suspendidas** en líquidos usando el principio de dispersión de luz.

## **Fórmulas de Conversión**

### **1. Voltaje a Turbidez (Fórmula Lineal)**
$$Turbidez(NTU) = (VoltajeSalida - VoltajeAguaLimpia) × Pendiente$$

### **2. Fórmula Aproximada para Arduino**
$$Turbidez(NTU) = (4.1 - VoltajeSalida) × 1000$$

### **3. Fórmula con Calibración**
$$Turbidez(NTU) = K × (V_limpio - V_medido)$$

Donde:

- **K** = Factor de calibración (aprox. 1000)
- **V_limpio** = 4.1V (agua destilada)
- **V_medido** = Voltaje leído
## **📝 Ejemplos de Cálculo**

### **Ejemplo 1: Voltaje medido = 3.8V**

Turbidez = (4.1 - 3.8) × 1000 = 0.3 × 1000 = 300 NTU

### **Ejemplo 2: Voltaje medido = 2.0V**

Turbidez = (4.1 - 2.0) × 1000 = 2.1 × 1000 = 2100 NTU

### **Ejemplo 3: Con Arduino (ADC = 614)**

Voltaje = 614 × 5.0 / 1024 = 3.0V
Turbidez = (4.1 - 3.0) × 1000 = 1100 NTU

### **Interpretación:**

- **0-50 NTU**: Agua potable
    
- **50-500 NTU**: Agua tratada/ligeramente turbia
    
- **500+ NTU**: Agua turbia/no tratada