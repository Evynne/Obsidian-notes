**Sensor PMS5003ST**: Detecta material particulado entre **0.3µm** y **10µm** con una resolución de **1µg/m³** para partículas y **0.01mg/m³** para formaldehyde. Opera en dos modos de comunicación: **activo** y **pasivo**, e integra medición de **formaldehyde**, **temperatura** y **humedad**. Su rango máximo de operación para PM2.5 es **≥1000µg/m³**. Posee un tamaño compacto de **50×38×21mm**.

## Estructura de la Trama - Modo Activo (40 bytes)

- **Longitud total**: 40 bytes
- **Formato**: Todos los valores de 16 bits en **Big-Endian** (High Byte primero)
- **Cabecera fija**: 0x42 0x4D ("BM" en ASCII)
- **Baud rate**: 9600 bps, 1 stop bit, sin paridad


| Posición | Nombre       | Descripción                    | Unidad   |
| -------- | ------------ | ------------------------------ | -------- |
| 0-1      | Start Frame  | 0x42 0x4D (Fixed)              | -        |
| 2-3      | Frame Length | 0x00 0x28 (40 bytes)           | -        |
| 4-5      | Data1        | PM1.0 CF=1                     | µg/m³    |
| 6-7      | Data2        | PM2.5 CF=1                     | µg/m³    |
| 8-9      | Data3        | PM10 CF=1                      | µg/m³    |
| 10-11    | Data4        | PM1.0 ATM                      | µg/m³    |
| 12-13    | Data5        | PM2.5 ATM                      | µg/m³    |
| 14-15    | Data6        | PM10 ATM                       | µg/m³    |
| 16-17    | Data7        | Partículas >0.3µm en 0.1L      | unidades |
| 18-19    | Data8        | Partículas >0.5µm en 0.1L      | unidades |
| 20-21    | Data9        | Partículas >1.0µm en 0.1L      | unidades |
| 22-23    | Data10       | Partículas >2.5µm en 0.1L      | unidades |
| 24-25    | Data11       | Partículas >5.0µm en 0.1L      | unidades |
| 26-27    | Data12       | Partículas >10.0µm en 0.1L     | unidades |
| 28-29    | Data13       | Formaldehyde = Valor/1000      | mg/m³    |
| 30-31    | Data14       | Temperatura = Valor(signed)/10 | ℃        |
| 32-33    | Data15       | Humedad = Valor/10             | %        |
| 34-35    | Data16       | Reservado                      | -        |
| 36-37    | Data17       | Versión \| Código Error        | -        |
| 38-39    | Checksum     | Verificación                   | -        |
### Conversiones Específicas

- **Formaldehido**: 

	**Paso 1: Obtener el Valor Decimal de Data13**
$$Data13decimal = (Data13_High × 256) + Data13_Low$$
	**Paso 2: Aplicar la Fórmula de Conversión** 
$$HCHO(mg/m³) = \frac{Data13decimal}{1000}$$
- **Temperatura**: $$Temp(℃) = \frac{Data14(signed)}{10}$$
- **Humedad**: $$Hum(porcentaje) = \frac{Data15}{10}$$
### Cálculo de Checksum

$$Checksum = Suma(Byte[0] + Byte[1] + ... + Byte[37])$$

# Comandos del Sensor PMS5003ST - Modo Pasivo

## Estructura de Comandos (Host → Sensor)
El sensor PMS5003ST utiliza una **trama de 7 bytes** para los comandos en modo pasivo:

| Byte | Nombre        | Valor       | Descripción                     |
| ---- | ------------- | ----------- | ------------------------------- |
| 0    | Start Byte 1  | 0x42        | Cabecera fija                   |
| 1    | Start Byte 2  | 0x4D        | Cabecera fija                   |
| 2    | **Command**   | **0xE1-E4** | **BYTE DE COMANDO**             |
| 3    | Data High     | 0x00-0xFF   | Dato alto (generalmente 0x00)   |
| 4    | Data Low      | 0x00-0xFF   | Dato bajo (depende del comando) |
| 5    | Checksum High | Calculado   | Byte alto del checksum          |
| 6    | Checksum Low  | Calculado   | Byte bajo del checksum          |
|      |               |             |                                 |
## **BYTE DE COMANDO - Definiciones**

### **1. Comando: 

| Operación       | Command  | DATAH | DATAL | Función                |
| --------------- | -------- | ----- | ----- | ---------------------- |
| **Lectura**     | **0xE2** | 0x00  | 0x00  | Obtener datos actuales |
| **Modo Pasivo** | 0xE1     | 0x00  | 0x00  | Configurar modo pasivo |
| **Modo Activo** | 0xE1     | 0x00  | 0x01  | Configurar modo activo |
| **Sleep**       | 0xE4     | 0x00  | 0x00  | Entrar en bajo consumo |
| **Wake-up**     | 0xE4     | 0x00  | 0x01  | Salir de sleep mode    |

## **Cálculo de CHECKSUM para Comandos**

$$checksum = byte[0] + byte[1] + byte[2] + byte[3] + byte[4]$$