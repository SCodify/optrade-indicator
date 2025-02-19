# Documentación de `OPTRADE analysis`

### Introducción

El script **"Análisis OPTRADE con Promedio"** es una herramienta diseñada para traders que buscan analizar múltiples indicadores técnicos en un solo panel, proporcionando señales claras y fáciles de interpretar. Este script está desarrollado en **Pine Script**, el lenguaje de programación utilizado en la plataforma **TradingView**.

El objetivo principal de este script es ofrecer una visión consolidada de varios indicadores clave, como el **SMA50**, **RSI**, **MACD**, **Bandas de Bollinger**, **Estocástico**, **Volumen**, e **Ichimoku Cloud**, junto con cálculos de **Take Profit (TP)** y **Stop Loss (SL)** basados en el **ATR (Average True Range)**. Además, se ha implementado una funcionalidad avanzada que permite al usuario especificar la cantidad de velas a promediar para suavizar las señales y reducir el ruido.

### Características Principales

#### 1. **Configuración Personalizable**
El script incluye varias opciones de configuración que permiten adaptarlo a diferentes estrategias de trading:
- **Tipo de Activo**: Se puede seleccionar entre activos criptográficos ("Crypto") u otros activos ("Otros"), lo que ajusta automáticamente los umbrales de algunos indicadores.
- **Multiplicadores TP y SL**: Permite personalizar los niveles de Take Profit y Stop Loss basados en el ATR.
- **Invertir TP y SL**: Una opción para invertir los niveles de TP y SL según las necesidades del trader.
- **Precio Dinámico o Manual**: El usuario puede elegir entre usar el precio de cierre actual o ingresar un precio manual para los cálculos.

#### 2. **Promedio de Velas**
Una característica destacada es la posibilidad de especificar la cantidad de velas a promediar (`avgCandles`). Esto permite:
- Suavizar las señales de los indicadores.
- Reducir el impacto del ruido en mercados volátiles.
- Mejorar la precisión de las señales generadas.

#### 3. **Indicadores Incluidos**
El script analiza los siguientes indicadores técnicos:
- **SMA50**: Evalúa si el precio está por encima o por debajo de la media móvil simple de 50 períodos.
- **RSI**: Identifica condiciones de sobrecompra y sobreventa.
- **MACD**: Detecta cruces alcistas o bajistas entre la línea MACD y la señal.
- **Bandas de Bollinger**: Determina si el precio está cerca de la banda superior, inferior o en el medio.
- **Estocástico**: Evalúa condiciones de sobrecompra y sobreventa.
- **Volumen**: Analiza si el volumen está aumentando, disminuyendo o en niveles neutrales.
- **Ichimoku Cloud**: Evalúa la posición del precio respecto a la nube (por encima, por debajo o dentro).

#### 4. **Interfaz Visual**
El script genera una tabla en la esquina inferior derecha del gráfico, donde se muestran los resultados de cada indicador. Las señales se representan con emojis para facilitar su interpretación:
- 🟢: Señal alcista.
- 🔴: Señal bajista.
- 🟡: Neutral.

---

### Ejemplo de Uso

#### Configuración del Script
Para utilizar el script, simplemente añádelo a tu gráfico en TradingView. Puedes personalizarlo mediante los siguientes parámetros:

```
//@version=5
indicator("Análisis OPTRADE con Promedio", overlay=true, max_labels_count=500)

// Configuración de entrada
int avgCandles = input.int(1, "Cantidad de Velas para Promedio", minval=1)
float tpAtrMultiplier = input.float(1.0, "Multiplicador TP ATR", minval=0.1, step=0.1)
float slAtrMultiplier = input.float(1.0, "Multiplicador SL ATR", minval=0.1, step=0.1)
```

#### Interpretación de Resultados
Por ejemplo, si el RSI promediado está por encima del umbral de sobrecompra (75 para criptomonedas), el script mostrará un emoji 🔴 en la columna correspondiente, indicando una posible señal de venta.

---

### Desarrollo Técnico

#### Función `avgValue`
El corazón del script es la función `avgValue`, que calcula el promedio de los últimos `avgCandles` valores de un indicador. Aquí está su implementación:

```
avgValue(values) =>
    ta.sma(values, avgCandles)
```

Esta función utiliza la función `ta.sma()` de Pine Script para calcular el promedio móvil simple de los valores proporcionados.

#### Ejemplo de Cálculo de RSI Promediado
El RSI se calcula de la siguiente manera:

```
rsi = ta.rsi(close, 14)
avg_rsi = avgValue(rsi)
cond_rsi = avg_rsi >= rsiThreshold ? "Sobrecompra" : avg_rsi <= 30 ? "Sobreventa" : "Neutral"
```

Aquí, el RSI se promedia utilizando la función `avgValue`, y luego se evalúa si está en sobrecompra, sobreventa o en niveles neutrales.

>### Conclusión
>
>El script **"Análisis OPTRADE con Promedio"** es una herramienta poderosa para traders que desean simplificar el análisis técnico y tomar decisiones informadas. Al combinar múltiples indicadores en una interfaz visual clara y permitir la personalización de parámetros clave, este script se convierte en un recurso valioso para cualquier estrategia de trading.