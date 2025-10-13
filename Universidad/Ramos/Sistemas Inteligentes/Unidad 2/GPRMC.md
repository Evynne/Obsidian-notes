El **GPRMC** (Recommended Minimum Specific GNSS Data) es una sentencia NMEA 0183 para datos GPS.

## **Estructura GPRMC**
Ej: $GPRMC,hhmmss.sss,A,llll.llll,a,yyyyy.yyyy,a,xxx.xxx,xxx.xxx,ddmmyy,,,a*hh

| Campo          | Ejemplo    | Descripción                  |
| -------------- | ---------- | ---------------------------- |
| **$GPRMC**     | -          | Cabecera                     |
| **hhmmss.sss** | 125045.000 | Hora UTC (12:50:45)          |
| **A/V**        | A          | Estado: A=válido, V=inválido |
| **llll.llll**  | 3321.1234  | Latitud (33°21.1234')        |
| **N/S**        | N          | Hemisferio: N=norte, S=sur   |
| **yyyyy.yyyy** | 11706.5432 | Longitud (117°06.5432')      |
| **E/W**        | W          | Este/Oeste: E=este, W=oeste  |
| xxx.xxx        | 2.5        | Velocidad (nudos)            |
| xxx.xxx        | 45.0       | Rumbo (grados)               |
| **ddmmyy**     | 150123     | Fecha (15/01/2023)           |
| ***hh**        | *6A        | Checksum                     |

## **INTERPRETACIÓN CAMPO POR CAMPO**

### **1. Hora UTC: `hhmmss.sss`**
**Formato**: `125045.000`
	**Conversión**:
	Horas = 12
	Minutos = 50
	Segundos = 45
**Resultado**: 12:50:45 UTC

### **2. Estado: `A` o `V`**
- **`A`** = Data válida ✓
- **`V`** = Data inválida ✗ (sin fix GPS)
### **3. Latitud: `llll.llll,a`**
**Ejemplo**: `3321.1234,N`
	**Conversión**:
	Grados = 33 (2 primeros digitos)
	Minutos = 21.1234
	Latitud_decimal = 33 + (21.1234 / 60) = 33.352056°
**Hemisfério**: `N` = Norte, `S` = Sur

### **4. Longitud: `yyyyy.yyyy,a`**
**Ejemplo**: `11706.5432,W`
**Conversión**:
	Grados = 117 (3 primeros digitos)
	Minutos = 6.5432
	Longitud_decimal = 117 + (6.5432 / 60) = 117.109053°

### **5. Velocidad: `xxx.xxx`**
**Unidad**: Nudos (knots)  
**Ejemplo**: `2.5` nudos  
**Conversión a km/h**:
	km/h = 2.5 × 1.852 = 4.63 km/h

### **6. Rumbo: `xxx.xxx`**
**Unidad**: Grados (0-359.9)  
**Ejemplo**: `45.0` = 45° desde el Norte verdadero

### **7. Fecha: `ddmmyy`**
**Formato**: `150123`  
**Conversión**:
	Día = 15
	Mes = 01  
	Año = 2023

### **Velocidad a Diferentes Unidades:**
km/h = nudos × 1.852
m/s = nudos × 0.51444
mph = nudos × 1.15078

##  **VALORES ESPECIALES/INVÁLIDOS**
- **Velocidad = 0.000**: Vehículo detenido
- **Rumbo = 0.000**: Sin dirección definida
- **Estado = V**: Sin señal GPS
- **Campos vacíos**: Datos no disponibles