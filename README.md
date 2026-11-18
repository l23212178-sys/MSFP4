
[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=l23212178-sys/MSFP4)

# Práctica 4 — Modelado y control del sistema endócrino

Repositorio académico de **Modelado de Sistemas Fisiológicos (IBF-1020)**, del programa de **Ingeniería Biomédica** del Tecnológico Nacional de México / Instituto Tecnológico de Tijuana.

La práctica comprende el modelado matemático de un sistema endócrino mediante analogías eléctricas, la comparación entre condiciones de control y caso, el diseño de un controlador PID y la verificación mediante MATLAB, Simulink, Python y resultados experimentales.

**Docente:** Dr. Paul Antonio Valle Trujillo  
**Correo:** paul.valle@tectijuana.edu.mx  
**Departamento:** Ingeniería Eléctrica y Electrónica  
**Institución:** Tecnológico Nacional de México / Instituto Tecnológico de Tijuana  
**Asignatura:** Modelado de Sistemas Fisiológicos  
**Programa:** Ingeniería Biomédica  
**Estudiante:** Osmar Ediel Armenta Medina  
**Número de control:** 23212178  
**Correo institucional:** l23212178@tectijuana.edu.mx  
**Repositorio de la asignatura:** https://github.com/DrPaulValle/MSF-IBF1020  
**Sede:** Tijuana, Baja California, México.

---

<a id="contenido"></a>
## Contenido

1. [Resumen](#resumen)
2. [Competencia y objetivos](#objetivos)
3. [Relación con el temario](#temario)
4. [Modelo fisiológico y BioRender](#biorender)
5. [Analogía eléctrica y parámetros](#analogia)
6. [Formulación matemática](#modelo)
7. [Análisis de error y estabilidad](#analisis)
8. [Señal de entrada y simulación](#senales)
9. [MATLAB, Simulink y Simscape](#matlab)
10. [Control PID y lazo cerrado](#pid)
11. [Reproducción en Python](#python)
12. [Resultados y evidencia experimental](#resultados)
13. [Verificación cruzada](#verificacion)
14. [Estructura del repositorio](#estructura)
15. [Requisitos y reproducción](#requisitos)
16. [Conclusiones](#conclusiones)
17. [Referencias](#referencias)

---

<a id="resumen"></a>
## Resumen

Esta práctica tiene como finalidad analizar y modelar el comportamiento dinámico del sistema endócrino mediante un circuito eléctrico equivalente de segundo orden. Se consideran dos condiciones: un sistema de control que representa una respuesta de referencia y un caso alterado.

Se utilizan resistencias, capacitancia e inductancia para representar procesos de transporte, almacenamiento y respuesta de una señal hormonal. A partir de las leyes de Kirchhoff se obtiene la función de transferencia del sistema, permitiendo analizar su estabilidad y comportamiento temporal.

Posteriormente, se implementa un controlador PID para reducir la diferencia entre la respuesta del caso y la condición de control. Los resultados se obtienen mediante MATLAB/Simulink y Python, complementándose con una representación fisiológica desarrollada en BioRender y evidencia experimental mediante osciloscopio.

**Palabras clave:** sistema endócrino; homeostasis; hipertiroidismo; analogía eléctrica; circuito RLC; función de transferencia; PID; MATLAB; Simulink; Simscape Electrical; Python; BioRender.

[Volver al contenido](#contenido)

---

<a id="objetivos"></a>
## Competencia y objetivos

### Competencia a desarrollar

Modelar sistemas fisiológicos mediante analogías eléctricas, ecuaciones diferenciales y funciones de transferencia, analizando su comportamiento dinámico y aplicando estrategias de control para mejorar su respuesta.

### Objetivo general

Modelar y comparar las respuestas de un sistema endócrino bajo condiciones de control y caso, implementando un controlador PID que permita aproximar la respuesta alterada a la condición de referencia.

### Objetivos específicos

- Identificar las variables de entrada y salida del sistema.
- Establecer la analogía eléctrica del sistema endócrino.
- Obtener las ecuaciones diferenciales y funciones de transferencia.
- Analizar el error estacionario y la estabilidad.
- Simular el sistema mediante MATLAB y Simulink.
- Implementar un controlador PID.
- Reproducir los resultados utilizando Python.
- Comparar las simulaciones con la evidencia experimental.

[Volver al contenido](#contenido)

---

<a id="temario"></a>
## Relación con el temario

| Unidad | Contenido aplicado |
|---|---|
| I. Sistemas de control retroalimentados | Lazo abierto, lazo cerrado, respuesta temporal, error y estabilidad |
| II. Modelado matemático | Analogía eléctrica, leyes de Kirchhoff y funciones de transferencia |
| III. Controladores | Diseño y evaluación de un controlador PID |

[Volver al contenido](#contenido)

---

<a id="biorender"></a>
## Modelo fisiológico y BioRender

El sistema endócrino regula diversas funciones fisiológicas mediante la secreción de hormonas y su interacción con órganos y tejidos.

Para esta práctica se realizó una representación gráfica en BioRender, considerando dos condiciones:

- **Control:** sistema endócrino en homeostasis.
- **Caso:** representación ilustrativa de hipertiroidismo.

### Diagrama desarrollado en BioRender

<p align="center">
  <img src="imagenes/biorender.png" alt="Sistema endocrino en BioRender" width="850">
</p>

**Figura 1.** Representación del sistema endócrino en homeostasis y del caso de hipertiroidismo, incluyendo la analogía eléctrica y las variables Ve(t), Fe(t), Vs(t), Fs(t), R1, R2, C y L.

[Consultar BioRender original en PDF](Biorender%20%28sistema%20endocrino%29.pdf)

La representación anatómica es ilustrativa. El modelo eléctrico es una simplificación matemática y no constituye una validación clínica específica del hipertiroidismo.

[Volver al contenido](#contenido)

---

<a id="analogia"></a>
## Analogía eléctrica y parámetros

El sistema se representa mediante un circuito compuesto por dos resistencias, una capacitancia y una inductancia.

La fuente Ve(t) se conecta en serie con R1. Posteriormente se encuentra el nodo Vs(t), con una rama capacitiva C conectada a tierra y otra rama compuesta por L y R2 en serie.

| Variable | Interpretación |
|---|---|
| Ve(t) | Estímulo de entrada |
| Fe(t) | Flujo de secreción hormonal |
| R1 | Resistencia al transporte |
| C | Almacenamiento de la señal hormonal |
| L | Inercia o retardo de respuesta |
| R2 | Utilización o eliminación de la señal |
| Fs(t) | Flujo asociado con la respuesta |
| Vs(t) | Señal de salida del sistema |

### Parámetros utilizados

| Parámetro | Control | Caso |
|---|---:|---:|
| R1 | 1 kΩ | 1 kΩ |
| L | 100 mH | 100 mH |
| C | 1 µF | 1000 µF |
| R2 | 100 kΩ | 1 kΩ |

Los parámetros corresponden a los utilizados en el programa Python de la práctica.

[Volver al contenido](#contenido)

---

<a id="modelo"></a>
## Formulación matemática

### Ecuaciones integro-diferenciales

Aplicando las leyes de Kirchhoff:

$$
F_e(t)=C\frac{dV_s(t)}{dt}+F_s(t)
$$

$$
V_e(t)=R_1F_e(t)+V_s(t)
$$

$$
V_s(t)=L\frac{dF_s(t)}{dt}+R_2F_s(t)
$$

Despejando las derivadas:

$$
\frac{dV_s}{dt}=
\frac{1}{C}
\left(
\frac{V_e-V_s}{R_1}-F_s
\right)
$$

$$
\frac{dF_s}{dt}=
\frac{V_s-R_2F_s}{L}
$$

### Función de transferencia general

Aplicando la transformada de Laplace con condiciones iniciales nulas:

$$
\boxed{
G(s)=\frac{V_s(s)}{V_e(s)}
=
\frac{Ls+R_2}
{CLR_1s^2+(CR_1R_2+L)s+(R_1+R_2)}
}
$$

El numerador contiene el término **Ls + R2**, mientras que el denominador es de segundo orden.

### Función de transferencia del sistema control

$$
G_{control}(s)=
\frac{0.1s+100000}
{0.0001s^2+100.0001s+101000}
$$

### Función de transferencia del caso

$$
G_{caso}(s)=
\frac{0.1s+1000}
{0.1s^2+1000.1s+2000}
$$

[Volver al contenido](#contenido)

---

<a id="analisis"></a>
## Análisis de error y estabilidad

### Error en estado estacionario

Para una entrada escalón unitario, el valor final de una planta estable se determina mediante:

$$
V_s(\infty)=G(0)
$$

Para el sistema control:

$$
V_{s,control}(\infty)=
\frac{100000}{101000}
\approx0.9901
$$

Para el caso:

$$
V_{s,caso}(\infty)=
\frac{1000}{2000}=0.5
$$

Por lo tanto, los errores estacionarios en lazo abierto son:

$$
e_{ss,control}\approx0.0099
$$

$$
e_{ss,caso}=0.5
$$

### Análisis de estabilidad

Los polos del sistema se obtienen a partir del denominador:

$$
CLR_1s^2+(CR_1R_2+L)s+(R_1+R_2)=0
$$

Las condiciones control y caso presentan polos con parte real negativa, por lo que las plantas analizadas son estables.

Sin embargo, sus diferentes parámetros producen variaciones en el tiempo de respuesta y en el valor estacionario.

[Volver al contenido](#contenido)

---

<a id="senales"></a>
## Señal de entrada y condiciones de simulación

Se utiliza una señal escalón unitario para observar el comportamiento temporal de las condiciones control y caso.

| Parámetro | Valor |
|---|---|
| Tiempo inicial | 0 s |
| Tiempo final | 10 s |
| Paso temporal en Python | 0.001 s |
| Solver MATLAB | ode15s |
| Paso máximo Simulink | 1e-3 s |
| Entrada | Escalón unitario |

La señal permite comparar el tiempo de respuesta, el valor estacionario y el efecto del controlador PID.

[Volver al contenido](#contenido)

---

<a id="matlab"></a>
## Implementación en MATLAB, Simulink y Simscape

La simulación se realizó mediante el cuaderno computacional MATLAB y el modelo de Simulink.

### Código de simulación

```matlab
clc; clear; close all; warning('off','all')

open_system('sistema')

parameters.StopTime = '10';
parameters.Solver = 'ode15s';
parameters.MaxStep = '1e-3';

x = sim('sistema',parameters);

plotsignals(x.control,x.CE,x.PID,x.Ve,'Caso')
```

El código ejecuta el modelo y recupera las señales correspondientes a la condición control, caso, tratamiento PID y entrada.

El archivo del modelo se proporciona como `sistema(3).slx`. Para ejecutar el cuaderno sin modificar las llamadas, debe utilizarse una copia denominada `sistema.slx`.

### Resultados obtenidos en MATLAB

<p align="center">
  <img src="imagenes/matlab.png" alt="Resultados MATLAB" width="850">
</p>

**Figura 2.** Respuestas de las condiciones control, caso y tratamiento PID obtenidas mediante MATLAB.

[Consultar gráfica original](grafica%20cuadernillo.pdf)

[Consultar cuaderno MATLAB](Armenta23212178.pdf)

[Volver al contenido](#contenido)

---

<a id="pid"></a>
## Control PID y lazo cerrado

Para corregir la respuesta del caso se implementó un controlador PID con retroalimentación negativa.

La señal de error se define como:

$$
e(t)=V_{s,control}(t)-V_{s,caso}(t)
$$

El controlador PID ideal se expresa mediante:

$$
K(s)=k_P+\frac{k_I}{s}+k_Ds
$$

### Ganancias del controlador

| Parámetro | Valor |
|---|---:|
| kP | 13209.9564 |
| kI | 32316525.9285 |
| kD | 0.18118 |

### Implementación del PID en Python

```python
kP,kI,kD = 13209.9564,32316525.9285,0.18118

Cr = 1E-6
Re = 1/(Cr*kI)
Rr = kP*Re
Ce = kD/Rr

numPID = [Re*Rr*Ce*Cr,Re*Ce+Rr*Cr,1]
denPID = [Re*Cr,0]

PID = ctrl.tf(numPID,denPID)

sysPID = ctrl.feedback(
    ctrl.series(PID,sysCaso),
    1,
    sign=-1
)
```

La implementación permite estudiar el comportamiento de la condición alterada al aplicar un controlador con retroalimentación.

En el programa Python, la respuesta del sistema control se utiliza como referencia para la simulación del tratamiento PID.

[Volver al contenido](#contenido)

---

<a id="python"></a>
## Reproducción en Python

Para verificar los resultados obtenidos mediante MATLAB se desarrolló una simulación adicional utilizando Python.

Se emplearon las bibliotecas:

- NumPy
- Matplotlib
- Python Control Systems Library

### Función de transferencia implementada

```python
def sis(C, R2, nombre):
    R1, L = 1E3,100E-3

    num = [L, R2]

    den = [
        C*L*R1,
        C*R1*R2+L,
        R1+R2
    ]

    sys = ctrl.tf(num, den)

    print(f"Función de transferencia {nombre}: {sys}\n")

    return sys

sysControl = sis(1E-6,100E3,"Control")

sysCaso = sis(1000E-6,1E3,"Caso")
```

### Resultados obtenidos en Python

<p align="center">
  <img src="imagenes/python.png" alt="Resultados Python" width="850">
</p>

**Figura 3.** Comparación de la señal de entrada, sistema control, caso y tratamiento PID obtenida mediante Python.

[Consultar gráfica original](grafica%20python.pdf)

[Volver al contenido](#contenido)

---

<a id="resultados"></a>
## Resultados y evidencia experimental

### Comparación de resultados

Las simulaciones permiten identificar diferencias entre la respuesta de referencia y la condición alterada.

| Sistema | Comportamiento |
|---|---|
| Entrada | Escalón unitario |
| Control | Respuesta rápida con valor final cercano a 0.99 |
| Caso | Respuesta más lenta con valor final cercano a 0.50 |
| Tratamiento PID | Aproximación de la respuesta alterada a la referencia |

La diferencia principal entre las condiciones estudiadas se encuentra en la rapidez de respuesta y el valor estacionario.

### Evidencia experimental mediante osciloscopio

<p align="center">
  <img src="imagenes/osciloscopio.png" alt="Captura del osciloscopio" width="850">
</p>

**Figura 4.** Respuesta experimental registrada mediante osciloscopio OWON.

En la captura se observa una transición de entrada y una respuesta de salida gradual.

Las mediciones visibles son:

| Parámetro | Valor |
|---|---:|
| Canal 1, Vpp | 1.080 V |
| Canal 2, Vpp | 520.0 mV |

[Consultar captura original](Screenshot%20osciloscopio.pdf)

Los resultados experimentales muestran cualitativamente el comportamiento dinámico del sistema modelado.

[Volver al contenido](#contenido)

---

<a id="verificacion"></a>
## Verificación cruzada

Los resultados se analizaron mediante diferentes herramientas de simulación y medición.

**MATLAB/Simulink:** permitió ejecutar el modelo y visualizar las respuestas de control, caso y tratamiento PID.

**Python:** permitió reproducir las funciones de transferencia y comparar las respuestas mediante una segunda herramienta computacional.

**BioRender:** facilitó la representación visual de la analogía entre el sistema fisiológico y el circuito eléctrico.

**Osciloscopio:** proporcionó evidencia experimental de la respuesta temporal del sistema.

Las simulaciones presentan concordancia cualitativa en la separación entre las condiciones control y caso, así como en el efecto del controlador.

[Volver al contenido](#contenido)

---

<a id="estructura"></a>
## Estructura del repositorio

```text
Practica4_Endocrino/
├── README.md
├── Armenta23212178.mlx
├── Armenta23212178.pdf
├── sistema(3).slx
├── codigo.py
├── Biorender (sistema endocrino).pdf
├── grafica cuadernillo.pdf
├── grafica python.pdf
├── Screenshot osciloscopio.pdf
└── imagenes/
    ├── biorender.png
    ├── matlab.png
    ├── python.png
    └── osciloscopio.png
```

Las imágenes se encuentran vinculadas mediante rutas relativas para que se visualicen directamente en GitHub.

[Volver al contenido](#contenido)

---

<a id="requisitos"></a>
## Requisitos y reproducción

### Software utilizado

- MATLAB
- Simulink
- Simscape Electrical, cuando corresponda al modelo
- Python 3
- NumPy
- Matplotlib
- Python Control Systems Library
- BioRender

### Instalación de bibliotecas Python

```bash
python -m pip install numpy matplotlib control
```

### Procedimiento de reproducción

1. Descargar los archivos del repositorio.
2. Abrir el modelo de Simulink.
3. Ejecutar el cuaderno MATLAB.
4. Verificar las respuestas de control, caso y tratamiento PID.
5. Ejecutar el programa `codigo.py`.
6. Comparar las gráficas obtenidas.
7. Revisar el diagrama BioRender y la evidencia experimental.

[Volver al contenido](#contenido)

---

<a id="conclusiones"></a>
## Conclusiones

El modelado del sistema endócrino mediante una analogía eléctrica permitió analizar su comportamiento dinámico a partir de un sistema de segundo orden.

Las modificaciones de resistencia y capacitancia produjeron diferencias en el tiempo de respuesta y en el valor estacionario de las condiciones control y caso.

La implementación del controlador PID permitió aproximar la respuesta del sistema alterado a la condición de referencia, mostrando la utilidad de la retroalimentación para mejorar el comportamiento del modelo.

Las simulaciones desarrolladas en MATLAB y Python facilitaron la comparación de resultados, mientras que el diagrama BioRender y las mediciones del osciloscopio complementaron la interpretación fisiológica y experimental.

La práctica permitió integrar conocimientos de modelado matemático, sistemas de control, programación y análisis de señales aplicados a la Ingeniería Biomédica.

[Volver al contenido](#contenido)

---

<a id="referencias"></a>
## Referencias

1. Valle Trujillo, P. A. (2026). *Modelado de Sistemas Fisiológicos (IBF-1020)*. Apartado 5.6: Modelado y control del sistema endócrino. Instituto Tecnológico de Tijuana.

2. Valle Trujillo, P. A. *README de referencia: Práctica 0 — Modelo de mecánica pulmonar de segundo orden*. Material proporcionado por el docente.

3. Armenta Medina, O. E. *Armenta23212178.mlx*, *codigo.py*, *sistema(3).slx*, resultados gráficos, evidencia de osciloscopio y diagrama BioRender.

4. Repositorio de la asignatura: https://github.com/DrPaulValle/MSF-IBF1020

[Volver al contenido](#contenido)
