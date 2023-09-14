Trabajo final Seccion A: Ciencia de Datos: Modelos Predictivos I
================
Ing. José Ricardo Rojas Lima
2023-09-14

## INTRODUCCIÓN

Como sabemos la oferta monetaria es la cantidad de dinero circulante en
una economia en un periodo determinado. La importancia de estudiar este
indicador radica en su impacto en la economía de México, y por
consiguiente en la economia personal. como sabemos una de las
consecuencias de la oferta monetaria es el impacto que se refleja
directamente en las tasas de interes. Si hay un exceso de dinero en el
mercado, las tasas de interes pueden bajar, lo que impulsa el gasto y la
inversión. La escasez de dinero puede llevar a incremento en las tasas
de interes lo que podría desalentar el gasto e impulsar el ahorro e
invertir en instrumentos financieros por rendimientos altos.

Por otra parte seria interesante analizar las exportaciones, ya que este
indicador impacta directamente en la demanda de la moneda local, si un
pais aumenta las exportaciones, es probable que la demanda de su moneda
tambien aumente, lo que puede llevar a un fortalecimiento de la moneda
local en los mercados de divisas. Un tipo de cambio más fuerte puede
influir en la oferta monetaria al afectar la cantidad de moneda local en
circulación en el país.

En el siguiente documento se analizara el crecimiento de las tasas
oferta monetaria (1989-2023) y las exportaciones(1993-2023) en Mexico,
mediante modelos de regresion lineal, en especifico se aplicara un
Modelo de tasa de crecimiento relativa compuesta.

## Modelo de regresión lineal de la oferta monetaria

En el siguiente gráfico podemos observar el crecimiento de la oferta
monetaria con respecto del tiempo.

``` r
plot(tsbase[,"OM_TOTAL"],
     xlab = "Periodo (1988 - 2023",
     ylab = "Oferta monetaria")
```

![](Trabajo_final_Seccion_A_files/figure-gfm/Grafica%20Oferta%20Monetaria-1.png)<!-- -->

Se aplica el modelo a la variable OM_TOTAL(Oferta Monetaria) y agregamos
la variable “trend”, esta permite que el modelo capture y modele el
efecto general de cambio en el tiempo.

``` r
tasa <- tslm(log(OM_TOTAL) ~ trend, data = tsbase) 
summary(tasa)
```

    ## 
    ## Call:
    ## tslm(formula = log(OM_TOTAL) ~ trend, data = tsbase)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -0.86236 -0.36580 -0.00192  0.36943  0.70501 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 1.361e+01  3.852e-02  353.25   <2e-16 ***
    ## trend       1.397e-02  1.609e-04   86.87   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.3912 on 412 degrees of freedom
    ## Multiple R-squared:  0.9482, Adjusted R-squared:  0.9481 
    ## F-statistic:  7546 on 1 and 412 DF,  p-value: < 2.2e-16

Tomando en cuenta los resultados, nos interesa conocer cual es la tasa
de crecimiento relativa compuesta, para esto se toma el beta de la
variable “trend”.

Para el periodo 1988 - 2023 es de :

``` r
(exp(0.01397)-1)*100
```

    ## [1] 1.406804

Entonces en promedio la oferta monetaria mes a mes se ha incrementado a
razon de 1.4%

## Modelo de regresión lineal Exportaciones

Se realiza gráfica de las exportaciones a traves del tiempo.

``` r
plot(tsbase_Exp[,"E_Totales"],
     xlab = "Periodo (1993 - 2023)",
     ylab = "Exportaciones")
```

![](Trabajo_final_Seccion_A_files/figure-gfm/Grafica%20Exportaciones-1.png)<!-- -->

Se aplica el modelo a la variable E_TOTALES(Exportaciones) y agregamos
la variable “trend”, permitiendo que capture y modele el efecto general
de cambio en el tiempo.

``` r
tasa <- tslm(log(E_Totales) ~ trend , data = tsbase_Exp) 
summary(tasa)
```

    ## 
    ## Call:
    ## tslm(formula = log(E_Totales) ~ trend, data = tsbase_Exp)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -0.91505 -0.09306  0.01598  0.13772  0.36058 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 1.568e+01  1.981e-02  791.56   <2e-16 ***
    ## trend       5.922e-03  9.380e-05   63.13   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.1888 on 363 degrees of freedom
    ## Multiple R-squared:  0.9165, Adjusted R-squared:  0.9163 
    ## F-statistic:  3986 on 1 and 363 DF,  p-value: < 2.2e-16

De igual manera nos interesa conocer la tasa de crecimiento relativa
compuesta, para esto se toma el beta de la variable “trend”.

Para el periodo 1993 - 2023 es de :

``` r
(exp(.005922)-1)*100
```

    ## [1] 0.593957

Entonces en promedio las exportaciones mes a mes se ha incrementado a
razón de 0.5939 %
