**Sensor SDS018**: Detecta material particulado entre 2.5um y 10um con una resolución  de $0.3 ug/m^3$. Su rango de operación es de 0.0 a 999.9 $ug/m^3$. Posee un tamaño de 59x45x20mm. Ver figura 1.b, Mayores detalles en 

**Estructura general de la trama**


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

Trama ej: 

| AA  | C0  | 2C  | 01  | 90  | 01  | 12  | 34  | FE  | AB  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

**Formulas**

Conversión de datos a concentración:

PM2.5 ($ug/m^3$) = $\frac{(HighByte x 256) + LowByte}{10}$

PM10 ($ug/m^3$) = $\frac{(HighByte x 256) + LowByte}{10}$

Checksum (verificación de datos):

Checksum = DATA1+DATA2+...+DATA6

Invertir proceso:

Si la concentración de PM2.5 es 85 μg/m³, ¿cuáles serían los 
	valores HighByte y LowByte que enviaría el sensor?

Solución:             85 x 10 = 850

HighByte = 850 / 256 = 3
LowByte = 850 % 256 = 82             

calcular modulo:    $\frac{850}{256}$ = 3,3203
parte entera: 3
850 - (256 + 3) = 82