# Indicadores: definiciones y cálculo

Calcula siempre sobre los cierres devueltos por `get_price_history`. Indica el periodo y la fecha del último dato.

## Medias móviles
- **SMA n** = media de los últimos n cierres.
- **EMA n**: `EMA_t = cierre_t × k + EMA_{t-1} × (1 − k)`, con `k = 2 / (n + 1)`, semilla = SMA n.
- Lectura: precio > SMA50 > SMA200 → tendencia alcista; al revés → bajista. Cruce SMA50/SMA200 = cruce dorado / de la muerte.

## RSI 14 (Wilder)
1. Cambios diarios: ganancias G y pérdidas P (en valor absoluto).
2. Primera media: promedio simple de 14 periodos.
3. Siguientes: `media_t = (media_{t-1} × 13 + valor_t) / 14`.
4. `RS = mediaG / mediaP`; `RSI = 100 − 100 / (1 + RS)`.
- > 70 sobrecompra, < 30 sobreventa. En tendencia fuerte puede mantenerse en extremos.

## ATR 14
- `TR = max(alto − bajo, |alto − cierre_prev|, |bajo − cierre_prev|)`.
- ATR = suavizado de Wilder de TR (14).
- Uso: stops a 1,5–2 × ATR; ATR% = ATR / precio para comparar volatilidad.

## MACD (12, 26, 9)
- MACD = EMA12 − EMA26; señal = EMA9 del MACD; histograma = MACD − señal.

## Bandas de Bollinger (20, 2)
- Media = SMA20; bandas = media ± 2 × desviación estándar (20).

## Soportes y resistencias
- Swing high: máximo mayor que los 3–5 máximos a cada lado; swing low análogo.
- Agrupa niveles a menos de ~0,5 × ATR entre sí; más toques = nivel más fuerte.

## Rendimiento y riesgo
- Rentabilidad periodo = `cierre_final / cierre_inicial − 1`.
- Volatilidad anualizada = desviación estándar de rendimientos diarios × √252.
- Drawdown máximo = mayor caída desde un máximo previo.

## Dimensionamiento
- Riesgo fijo fraccional: `cantidad = floor(capital × riesgo% / |entrada − stop|)`.
- Topes: nominal ≤ 20 % del capital; no superar liquidez/margen disponible.
- Futuros: riesgo por contrato = |entrada − stop| × multiplicador.
- Opciones compradas: riesgo máx. = prima × multiplicador × contratos.
