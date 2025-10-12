**Sensor SDS018**: Detecta material particulado entre **2,5µm** y **10µm** con una resolución de **0,3µg/m³**.  Su rango de operación es de **0,0 a 999,9µg/m³**. Posee un tamaño de **59×45×20mm**.

## Estructura de la Trama
- **Longitud total**: 10 bytes
- **Formato**: Little-Endian para valores numéricos (contrario al PMS7003)
- **Cabecera fija**: 0xAA
- **Fin de trama**: 0xAB


| Posición | Nombre                   | Contenido/Propósito                  | Ejemplo (Hex) |
| -------- | ------------------------ | ------------------------------------ | ------------- |
| 0        | Cabecera (Header)        | Inicio del mensaje                   | AA            |
| 1        | Comando                  | Tipo de dato (lectura de partículas) | C0            |
| 2        | PM2.5 - Byte bajo (Low)  | Parte baja del valor de PM2.5        | 2C            |
| 3        | PM2.5 - Byte alto (High) | Parte alta del valor de PM2.5        | 01            |
| 4        | PM10 - Byte bajo (Low)   | Parte baja del valor de PM10         | 90            |
| 5        | PM10 - Byte alto (High)  | Parte alta del valor de PM10         | 01            |
| 6        | ID - Byte bajo           | Identificador único (parte baja)     | 12            |
| 7        | ID - Byte alto           | Identificador único (parte alta)     | 34            |
| 8        | Checksum                 | Suma de los bytes del 2 al 7         | FE            |
| 9        | Fin de la trama (Tail)   | Final del mensaje                    | AB            |

### Ejemplo de Trama Completa

| AA  | C0  | 2C  | 01  | 90  | 01  | 12  | 34  | FE  | AB  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
## Fórmulas y Cálculos

**Para PM2.5 y PM10**:
$$Valor_Entero = (HighByte × 256) + LowByte$$
$$Concentración (µg/m³) = \frac{Valor_Entero}{10}$$
### Cálculo de Checksum

Checksum = Byte[2] + Byte[3] + Byte[4] + Byte[5] + Byte[6] + Byte[7]

El checksum debe coincidir con el byte en la posición 8.

### Ejemplo Práctico: De Concentración a Bytes

Invertir proceso:

**Problema**: Si la concentración de PM2.5 es 85 µg/m³, ¿Cuáles serían los valores HighByte y LowByte?

Solución:             85 x 10 = 850

HighByte = $\frac{850}{256} = 3$     (parte entera)
LowByte = 850 % 256 = 82     (resto)         

**Verificación**:
- Cálculo del módulo: 850 ÷ 256 = 3,3203
- Parte entera: 3
- 850 - (256 × 3) = 850 - 768 = 82

**Resultado**: HighByte = 3, LowByte = 82