El TMP36 es un sensor de temperatura analógico fabricado por Analog Devices, Su función es medir la temperatura ambiente y entregar un voltaje proporcional a la temperatura.
A diferencia de un termómetro tradicional (con mercurio o resistencias variables), este sensor utiliza un transistor de silicio interno que cambia su voltaje (Vbe) con la temperatura.

- **Escala**: 10 mV/°C
- **A 0°C**: 500 mV
- **Rango**: -40°C a +125°C
- **Precisión**: ±2°C

Como mide la temperatura

La relación entre voltaje de salida (Vout) y la temperatura (°C) es lineal:
$$T(°C)=\frac{Vout(mV)-500}{10}$$
$$T(°C) = (Vout(V) - 0.5) × 100$$
Importante: el voltaje de salida tiene que ser en milivoltios (1V = 1000mV)

### Ejemplo de Temperatura (°C) a Voltaje:
$$Vout = \frac{45}{100} + 0.5 = 0.95V$$
Temperatura con arduino (10 bits)
$$T(°C) = ( (valor_{ADC} × 5000 ÷ 1024) - 500 ) ÷ 10$$