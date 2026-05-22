# Arquitectura de Computadores - Unidad 8  
## Post-Contenido 2: Operaciones con Cadenas y Aritmética en NASM

### Ingeniería de Sistemas - 2026

Estudiante: Sebastian Jose Padilla Escalante

---

## Descripción del laboratorio

Este laboratorio implementa en lenguaje ensamblador NASM (ejecutado en DOSBox) diferentes operaciones aritméticas avanzadas en modo real de 16 bits, incluyendo:

- Aritmética de precisión múltiple de 32 bits usando `ADC` y `SBB`
- Operaciones BCD empaquetado utilizando `DAA` y `DAS`
- Construcción de una mini calculadora de enteros usando `MUL` y `DIV`
- Conversión entre ASCII y valores binarios
- Verificación de resultados mediante checkpoints en DOSBox

---

## Objetivos

- Comprender el manejo del acarreo (CF) y el préstamo en operaciones de precisión múltiple.
- Implementar suma y resta de números de 32 bits usando registros de 16 bits.
- Aplicar correcciones BCD con instrucciones `DAA` y `DAS`.
- Diseñar una calculadora básica utilizando multiplicación y división en ensamblador.
- Manejar entrada y salida de datos mediante interrupciones `INT 21h`.

---

## Requisitos

### Software
- DOSBox 0.74 o superior
- NASM instalado y configurado

### Conocimientos previos
- Flags CF y OF
- Representación en complemento a 2
- BCD empaquetado
- Uso de interrupciones DOS (`INT 21h`, `INT 10h`)

---

## Estructura del proyecto


Padilla-post2-u8/
│
├── post2.asm ; Aritmética de 32 bits con ADC y SBB
├── post2b.asm ; Operaciones BCD con DAA y DAS
├── post2c.asm ; Mini calculadora con MUL y DIV
├── capturas/ ; Evidencias de ejecución en DOSBox
└── README.md ; Documentación del laboratorio


---

## Parte 1: Aritmética de 32 bits (ADC y SBB)

Se implementa la suma y resta de números de 32 bits utilizando dos registros de 16 bits:

- Parte baja: AX
- Parte alta: DX

### Suma de 32 bits
- Se usa `ADD` para la parte baja
- Se usa `ADC` para propagar el carry a la parte alta

Resultado esperado:
- `DX:AX = 0003:0000`

### Resta de 32 bits
- Se usa `SUB` para la parte baja
- Se usa `SBB` para propagar el borrow

Resultado esperado:
- `DX:AX = 0001:FFFF`

---

## Parte 2: Aritmética BCD (DAA y DAS)

Se trabaja con números en formato BCD empaquetado.

### Suma BCD
Ejemplo:
- 47 + 38 = 85

Sin `DAA` el resultado es incorrecto (7Fh), pero con `DAA` se ajusta correctamente a 85h.

### Resta BCD
Ejemplo:
- 73 - 28 = 45
- 20 - 01 = 19

`DAS` ajusta automáticamente el resultado cuando el valor binario no es válido como BCD.

---

## Parte 3: Mini calculadora (MUL y DIV)

La calculadora permite:

- Ingresar dos dígitos (0–9)
- Seleccionar operación (* o /)
- Mostrar el resultado en decimal ASCII

### Operaciones implementadas
- Multiplicación usando `MUL`
- División usando `DIV`
- Conversión ASCII ↔ binario
- Conversión binario ↔ decimal (subrutina con DIV)

### Casos de prueba
- 7 * 8 = 56
- 9 / 3 = 3
- División por cero → mensaje de error

---

## Compilación y ejecución


nasm -f bin post2.asm -o post2.com
nasm -f bin post2b.asm -o post2b.com
nasm -f bin post2c.asm -o post2c.com

En DOSBox:

post2.com
post2b.com
post2c.com
Checkpoints de verificación
Suma 32 bits correcta con ADC
Resta 32 bits correcta con SBB
Ajuste BCD correcto con DAA
Ajuste BCD correcto con DAS
Calculadora funcional con MUL y DIV
Evidencias

Las capturas de pantalla de ejecución en DOSBox se encuentran en la carpeta:

/capturas

Incluyen:

Resultado de suma 32 bits
Resultado de resta 32 bits
Suma BCD con DAA
Resta BCD con DAS
Ejecución de la calculadora
