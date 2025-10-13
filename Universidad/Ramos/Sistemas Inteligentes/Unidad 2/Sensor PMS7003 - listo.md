Sensor PMS7003: Detecta material particulado entre $1,0um$ y $10um$ con una resolución de $0,3ug/m^3$ en dos modos de operaciones: estándar y atmosférico. Además obtiene un histograma de partículas de diámetros de $0,3 um$, $0,5um$, $1,0um$, $2,5um$ $5,0um$ y $10um$. Su rango de operación es de $999,9ug/m^3$. Posee un tamaño de $48x37x12mm$  

## Estructura de la Trama

- **Longitud total**: 32 bytes
- **Formato**: Todos los valores de 16 bits en **Big-Endian** (High Byte primero)
- **Cabecera fija**: 0x42 0x4D ("BM" en ASCII)

| Posición | Nombre            | Descripción                                       | Unidad   |
| -------- | ----------------- | ------------------------------------------------- | -------- |
| 0        | Start Frame 1     | Cabecera inicial (siempre 0x42)                   | -        |
| 1        | Start Frame 2     | Cabecera inicial (siempre 0x4D)                   | -        |
| 2        | Frame Length High | Longitud alta del frame (siempre 0x00)            | -        |
| 3        | Frame Length Low  | Longitud baja del frame (28 bytes) (siempre 0x1C) | -        |
| 4-5      | Data1 High - Low  | PM1.0 CF=1 (partículas estándar)                  | µg/m³    |
| 6-7      | Data2 High - Low  | PM2.5 CF=1  (partículas estándar)                 | µg/m³    |
| 8-9      | Data3 High - Low  | PM10.0 CF=1 (partículas estándar)                 | µg/m³    |
| 10-11    | Data4 High - Low  | PM1.0 ATM  (ambiente)                             | µg/m³    |
| 12-13    | Data5 High - Low  | PM2.5 ATM  (ambiente)                             | µg/m³    |
| 14-15    | Data6 High - Low  | PM10.0 ATM  (ambiente)                            | µg/m³    |
| 16-17    | Data7 High - Low  | Partículas >0.3µm Conteo en 0.1 litro de aire     | unidades |
| 18-19    | Data8 High - Low  | Partículas >0.5µm Conteo en 0.1 litro de aire     | unidades |
| 20-21    | Data9 High - Low  | Partículas >1.0µm Conteo en 0.1 litro de aire     | unidades |
| 22-23    | Data10 High - Low | Partículas >2.5µm Conteo en 0.1 litro de aire     | unidades |
| 24-25    | Data11 High - Low | Partículas >5.0µm Conteo en 0.1 litro de aire     | unidades |
| 26-27    | Data12 High - Low | Partículas >10.0µm Conteo en 0.1 litro de aire    | unidades |
| 28-29    | Data13 High - Low | Versión - High Byte \| Código Error - Low Byte    | -        |
| 30       | Checksum - High   | Byte alto del checksum                            | -        |
| 31       | Checksum - Low    |   Byte bajo del checksum                          | -        |

## Información de Versión y Errores

### Versión - High Byte (Byte 28)

**Propósito**: Indicar la versión del firmware del sensor.

| Valor | Version | Significado            |
| ----- | ------- | ---------------------- |
| 0x01  | V1.x    | Versión inicial        |
| 0x02  | V2.x    | Versiones posteriores  |
| 0x03  | V3.x    | Versiones actualizadas |

### Código de Error - Low Byte (Byte 29)

**Propósito**: Indica el estado de funcionamiento interno del sensor.

| Valores | Codigo | Significado          | Accion                     |
| ------- | ------ | -------------------- | -------------------------- |
| 0x00    | 0      | **NINGÚN ERROR**     | Todo normal                |
| 0x01    | 1      | Error de láser       | Verificar alimentación     |
| 0x02    | 2      | Error de ventilador  | Verificar 5V y corriente   |
| 0x03    | 3      | Error de sensor      | Posible falla hardware     |
| 0x04    | 4      | Error de memoria     | Resetear sensor            |
| 0x05    | 5      | Error de calibración |   Re-calibrar o reemplazar |

## Fórmulas y Cálculos

### Conversión de Valores

**Para todos los campos de 16 bits** (concentraciones y conteos de partículas):
$$Valor = HighByte \times 256) + LowByte$$

### Cálculo de Checksum

**Fórmula**:
$$Checksum = Suma(Byte[0] + Byte[1] + ... + Byte [29])$$
**Verificación**:
- Calcular la suma de los bytes 0 al 29
- Comparar con el valor de 16 bits formado por los bytes 30-31
- Si coinciden, la trama es válida

### Ejemplo: Partículas >0.3µm

$$Partículas >0.3μm = (HighByte × 256) + LowByte = X * partículas/0.1L$$
## Notas Adicionales

- **Modos de Operación**:
    - **CF=1 (Estándar)**: Datos corregidos por factor de calibración de fábrica
    - **ATM (Ambiente)**: Datos bajo condiciones ambientales normales
    
- **Histograma de Partículas**: Proporciona conteos para partículas mayores a: 0,3µm, 0,5µm, 1,0µm, 2,5µm, 5,0µm y 10,0µm