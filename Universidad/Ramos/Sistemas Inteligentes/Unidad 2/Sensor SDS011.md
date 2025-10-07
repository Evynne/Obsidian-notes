##### SensorSDS011

Es similar al sensor anterior pero con un protocolo de comandos de configuración mas robusto. Detecta material particulado entre $1,0um$ y 10um con una resolución de $0,3 ug/m^3$. Su rango de operación es de 0,0 a $999,9 ug/m^3$. Posee un tamaño de $71x7023mm$

Estructura de la trama de datos (10 bytes):

| Posicion | Nombre                    | Descripcion                                                                                                           |
| -------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 0        | Cabecera (head)           | Marca el inicio del paquete. Siempre el valor fijo 0xAA.                                                              |
| 1        | Comando / Tipo de mensaje | Identifica el tipo de comando o respuesta.                                                                            |
| 2        | $PM2.5$ LowByte           | Byte LSB de la medicion de $PM2.5$ (en decimas de $ug/m^3$)                                                           |
| 3        | $PM2.5$ HighByte          | Byte MSB de la medicion de PM2.5                                                                                      |
| 4        | PM10 LowByte              | LSB del valor PM10 (en decimas de $ug/m^3$)                                                                           |
| 5        | PM10 HighByte             | MSB del valor PM10                                                                                                    |
| 6        | ID Byte 1                 | Primer byte del numero de identificación único del sensor (Útil cuando se usan varios sensores en red)                |
| 7        | ID Byte 2                 | Segundo byte del ID del sensor. El ID completo es (ID2 << 8) + ID1                                                    |
| 8        | Checksum                  | Byte de verificación de integridad. Se calcula como:  <br>$Checksum = (DATA2 + DATA3 + DATA4 + DATA5 + DATA6 + DATA7) |
| 9        | Fin de la trama (Tail)    | Marca el **fin del paquete**. Siempre es 0xAB.                                                                        |

Estructura temporal del ciclo PWM:

formula general: Concentración $(ug/^3)$ = $1000x(\frac{Thigh}{Tmedicion)})$ 

Thigh = $\frac{Concentracion}{1000}x1000ms = Concentracion (ms)$ 