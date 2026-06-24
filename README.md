# movimiento_browniano-
# Análisis de Procesos Estocásticos: Caminatas Aleatorias y Valoración de Opciones

## Resumen Ejecutivo

Este proyecto constituye una implementación integral en R para el análisis de **procesos estocásticos**, con aplicaciones específicas en modelado financiero. El desarrollo incluye:

- Análisis de caminatas aleatorias y verificación de propiedades de martingalas
- Implementación de procesos reescalados y estudio de convergencia
- Modelado de precios de activos mediante procesos geométricos
- Sistemas de valoración de opciones utilizando métodos Monte Carlo y Black-Scholes

El código original, desarrollado en Python (Jupyter Notebook), ha sido migrado integralmente a R utilizando RMarkdown para garantizar reproducibilidad y documentación exhaustiva.

## Objetivos del Análisis

1. **Verificar la propiedad de martingala** en caminatas aleatorias mediante ajuste de probabilidad p*
2. **Analizar procesos reescalados** $W^{(r)}$ para diferentes parámetros de escala
3. **Modelar evolución de precios** utilizando procesos estocásticos exponenciales
4. **Comparar metodologías de valoración** de opciones (numérica vs analítica)
5. **Validar convergencia estadística** de simulaciones Monte Carlo

## Estructura del Proyecto

```
.
├── README.md                                    # Documentación principal
├── Mov Browniano & Black-Scholes.Rmd            # Análisis principal en RMarkdown
├── Mov Browniano & Black-Scholes.html          # Reporte renderizado en HTML
├── Procesos_Estocásticos.pdf                    # Parte teórica
```

## Instrucciones de Implementación

### Prerrequisitos del Sistema

- R (versión 4.0 o superior)
- RStudio (entorno recomendado)
- Paquetes de R requeridos:

```r
install.packages(c(
  "ggplot2",      # Visualización de datos
  "gridExtra",    # Composición de gráficos
  "dplyr",        # Manipulación de datos
  "knitr",        # Generación de reportes
  "rmarkdown"     # Documentos dinámicos
))
```

### Procedimiento de Instalación

1. **Clonar el repositorio:**

```bash
git clone https://github.com/JohnSalmoran/Movimiento_Browniano
cd Movimiento_Browniano
```

2. **Abrir el documento RMarkdown:**

```r
# En entorno RStudio
file.edit("Mov Browniano & Black-Scholes.Rmd")
```

3. **Generar el reporte final:**

```r
# Opción 1: Interfaz RStudio - Seleccionar "Knit"
# Opción 2: Consola de R
rmarkdown::render("Mov Browniano & Black-Scholes.Rmd")
```

## Marco Metodológico

### Ejercicio 1: Caminatas Aleatorias y Propiedades de Martingalas

#### 1a. Caminata Aleatoria Fundamental
- Cálculo de probabilidad p* para garantizar propiedad de martingala
- Generación de caminata original S_k
- Proceso ajustado Z_k (martingala)
- Análisis comparativo mediante visualización

**Parámetros de configuración:**
- a = 1.1 (incremento positivo)
- b = -0.1 (incremento negativo)
- α = 0.04 (tasa libre de riesgo)
- N = 100 (número de iteraciones)

#### 1b. Procesos Reescalados
- Generación de $W^(r)$ para múltiples valores de r
- Interpolación lineal de procesos
- Análisis de convergencia en función de r

**Valores de r analizados:** 10, 20, 50

#### 1c. Modelado de Procesos de Precios
- Modelado exponencial: S(t) = S₀ · exp(-αt + W^(r)(t))
- Evolución temporal de precios
- S₀ = 110 (valor inicial)

#### 1d. Análisis Multidimensional
- Múltiples configuraciones de N y r
- Validación numérica de parámetros
- Comparación de trayectorias estocásticas

**Configuraciones evaluadas:**
```
N = 500:  r ∈ {50, 100, 250}
N = 1000: r ∈ {100, 200, 500}
N = 5000: r ∈ {500, 1000, 2500}
```

### Ejercicio 2: Valoración de Instrumentos Derivados

#### 2a. Comparación Metodológica: Monte Carlo vs Black-Scholes

**Parámetros del instrumento:**
- S₀ = 110 (precio subyacente)
- K = 113 (precio de ejercicio)
- r = 0.04 (tasa libre de riesgo)
- T = 1 (horizonte temporal)
- σ = √(2α) (parámetro de volatilidad)

**Metodologías implementadas:**

1. **Simulación Monte Carlo:**
   - 100,000 trayectorias simuladas
   - Variables aleatorias lognormales
   - Estimación del valor esperado del payoff

2. **Modelo Black-Scholes:**
   - Solución analítica cerrada
   - Cálculo de parámetros d₁ y d₂
   - Aplicación de función de distribución normal acumulada

3. **Análisis de Convergencia:**
   - Múltiples tamaños muestrales: {100, 500, 1K, 5K, 10K, 50K, 100K}
   - Visualización de convergencia en escala logarítmica
   - Cálculo de error absoluto y relativo

## Resultados Cuantitativos

### Validación Numérica

| Metodología | Valor del Derivativo | Error Relativo |
|-------------|---------------------|----------------|
| Black-Scholes | $13.0189 | - |
| Monte Carlo (100K) | $12.9987 | ~	0.16%% |

### Propiedades Verificadas

Propiedad de martingala para Z_k con p* calculado  
Convergencia de W^(r) a proceso de Wiener  
Convergencia de Monte Carlo a solución analítica  
Consistencia entre metodologías de valoración

## Especificaciones Técnicas

### Funciones Principales

#### Cálculo de Probabilidad Ajustada
```r
calcular_p_estrella(a, b, alpha)
# Retorna: probabilidad ajustada para martingala
```

#### Generación de Caminatas Aleatorias
```r
generar_caminata_aleatoria(N, a, b, alpha)
# Retorna: lista(S_k, Z_k, p_estrella)
```

#### Proceso Reescalado
```r
generar_proceso_reescalado(N, a, b, alpha, r)
# Retorna: data.frame(t, W_r, r)
```

#### Valoración de Derivativos
```r
simulacion_montecarlo(N, semilla)
black_scholes_call()
# Retornan: valor del instrumento
```

## Visualizaciones Generadas

1. **Caminatas Aleatorias:** Comparación S_k vs Z_k
2. **Procesos Reescalados:** W^(r) para múltiples valores de r
3. **Evolución de Precios:** Trayectorias de precios simuladas
4. **Convergencia Monte Carlo:** Error vs tamaño muestral
5. **Comparación Metodológica:** Monte Carlo vs Black-Scholes

## Referencias Teóricas

### Fundamentos Conceptuales

- **Martingala:** Proceso estocástico donde E[X_{n+1} | ℱ_n] = X_n
- **Proceso de Wiener:** Límite de caminatas aleatorias reescaladas
- **Modelo Black-Scholes:** dS = μS dt + σS dW
- **Monte Carlo:** Método numérico basado en muestreo aleatorio

### Formulación Matemática

**Probabilidad p*:**
```
p* = (-(a-b)² + √((a-b)⁴ - 4(a-b)² · 2 · (e^α - 1))) / (-2(a-b)²)
```

**Black-Scholes Call:**
```
C = S₀·N(d₁) - K·e^(-rT)·N(d₂)
d₁ = (ln(S₀/K) + (r + σ²/2)T) / (σ√T)
d₂ = d₁ - σ√T
```

## Resolución de Incidencias

### Incidencia: "NaN en cálculo de p*"
**Causa:** Parámetros incompatibles (a muy pequeño)  
**Solución:** Utilizar a = 1.1 en lugar de a = 0.09


### Advertencia: "p* fuera de rango [0,1]"
**Causa:** Valores de r incompatibles con parámetros  
**Solución:** El código filtra automáticamente estos casos

## Contribuciones al Proyecto

Las contribuciones son bienvenidas siguiendo el protocolo establecido:

1. Realizar fork del proyecto
2. Crear rama para la característica (`git checkout -b feature/nueva-caracteristica`)
3. Commit de cambios (`git commit -m 'Agregar nueva característica'`)
4. Push a la rama (`git push origin feature/nueva-caracteristica`)
5. Abrir Pull Request

## Consideraciones Adicionales

### Diferencias con la Implementación Python Original

- **Sintaxis adaptada** a convenciones de R
- **Visualizaciones mejoradas** con ggplot2
- **Validación robusta** de parámetros numéricos
- **Documentación integrada** con RMarkdown
- **Reproducibilidad** mediante semillas aleatorias


---

**Última actualización:** Noviembre 2025
**Versión:** 1.0.0
