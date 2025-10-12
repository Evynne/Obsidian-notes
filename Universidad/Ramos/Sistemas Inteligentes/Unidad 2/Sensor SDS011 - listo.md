##### SensorSDS011

Es similar al sensor SDS018 pero con un protocolo de comandos de configuración mas robusto. Detecta material particulado entre $1,0um$ y 10um con una resolución de $0,3 ug/m^3$. Su rango de operación es de 0,0 a $999,9 ug/m^3$. Posee un tamaño de $71x7023mm$

## Estructura de la Trama de datos (10 bytes):
- **Longitud total**: 10 bytes
- **Endianness**: Little-Endian (LSB primero)
- **Cabecera fija**: **0xAA 0xC0**
- **Tail fijo**: **0xAB** (al final de la trama)

| Posicion | Nombre                    | Descripcion                                                                                                           |
| -------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 0        | Cabecera (head)           | Marca el inicio del paquete. Siempre el valor fijo 0xAA.                                                              |
| 1        | Comando / Tipo de mensaje | Identifica el tipo de comando o respuesta. **0xC0** (datos)                                                           |
| 2        | $PM2.5$ LowByte           | Byte LSB de la medicion de $PM2.5$ (en decimas de $ug/m^3$)                                                           |
| 3        | $PM2.5$ HighByte          | Byte MSB de la medicion de PM2.5                                                                                      |
| 4        | PM10 LowByte              | LSB del valor PM10 (en decimas de $ug/m^3$)                                                                           |
| 5        | PM10 HighByte             | MSB del valor PM10                                                                                                    |
| 6        | ID Byte 1                 | Primer byte del numero de identificación único del sensor (Útil cuando se usan varios sensores en red)                |
| 7        | ID Byte 2                 | Segundo byte del ID del sensor. El ID completo es (ID2 << 8) + ID1                                                    |
| 8        | Checksum                  | Byte de verificación de integridad. Se calcula como:  <br>$Checksum = (DATA2 + DATA3 + DATA4 + DATA5 + DATA6 + DATA7) |
| 9        | Fin de la trama (Tail)    | Marca el **fin del paquete**. Siempre es 0xAB.                                                                        |

Estructura temporal del ciclo PWM:
### **Fórmula General:**

$$Concentración (µg/m³) = 1000 × \frac{T_{high}}{T_{medida}}$$
$$T_{medida} = 1000_{ms}$$
### **Cálculo de T_high:**
$$Thigh_{ms} = \frac{Concentración}{1000} × T_{medida}$$ 
## **Estructura de la Trama de COMANDOS (19 bytes)**
### **Formato Comandos:**
- **Longitud total**: 19 bytes
- **Cabecera fija**: **0xAA 0xB4**
- **Tail fijo**: **0xAB**


| Byte | Nombre       | Descripción              |
| ---- | ------------ | ------------------------ |
| 0    | Head         | Siempre 0xAA             |
| 1    | Command Head | Siempre 0xB4             |
| 2    | Command      | Tipo de comando          |
| 3-15 | Data 1-13    | Parámetros               |
| 16   | ID Byte 1    | ID sensor (0xFF = todos) |
| 17   | ID Byte 2    | ID sensor (0xFF = todos) |
| 18   | Checksum     | Verificación             |
| 19   | Tail         | Siempre 0xAB             |

### **Comandos Principales:**

| Comando              | Valor (Byte2) | Descripción                | Data1                                                      |
| -------------------- | ------------- | -------------------------- | ---------------------------------------------------------- |
| **Modo Trabajo**     | 0x01          | Configurar modo base       | 0x00 = Modo consulta, 0x1 = Modo ACTIVO (Envia automatico) |
| **Modo Reporte**     | 0x02          | Activar/desactivar reporte | 0x01=ON, 0x00=OFF                                          |
| **Solicitar Dato**   | 0x04          | Pedir lectura inmediata    | 0x00                                                       |
| **Modo Dormir**      | 0x06          | Activar/Desactivar Sleep   | 0x01=SLEEP, 0x00=WAKE                                      |
| **Obtener Firmware** | 0x07          | Versión de firmware        | 0x00                                                       |
| **Periodo Trabajo**  | 0x08          | Configurar intervalo       | **0x01=activar**. **DATA7=minutos (0x00-0x1E)**<br>        |

### **CÁLCULO DE CHECKSUM**
### Para TRAMA DE DATOS (10 bytes):
$$Checksum = (DATA[2] + DATA[3] + DATA[4] + DATA[5] + DATA[6] + DATA[7])$$

### Para TRAMA DE COMANDOS (19 bytes):
$$Checksum = (COMMAND + DATA1 + DATA2 + ... + DATA13 + ID1 + ID2)$$
### **CÁLCULO DE CONSUMO ENERGÉTICO**

### En modo activo:
$$Energía = 5V × 100mA = 0.5W$$
$$Consumo_{promedio} = (0.5W × 1s + 0.02W × (tiempo - 1s)) / tiempo en segundos
                 ≈ 0.021W$$
### En modo sleep:
$$Energía = 5V × 4mA = 0.02W (25 veces menos)$$
### **CÁLCULO DE RESOLUCIÓN (10 bytes)**
$$Resolución = \frac{999.9_{µg/m³}}{(2^{16} - 1)}$$

## **CONCENTRACIÓN PM**
$$PM(µg/m³) = \frac{[(High × 256) + Low]}{10}$$
## **ID SENSOR**
$$ID = (ID2 \times 256) + ID1$$