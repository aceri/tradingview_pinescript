
Study - Double Zero Lag Cross Experiment

* Experimenting with 4 ZLEMA Crossovers and multiple logical conditions optimized with a software multiplexor for all possible  conditions & ulcer index

     1. BUY:
            * zEMA1>zEMA2 and zEMA3>zEMA4) and (zEMA1[1]<zEMA2[1] or zEMA3[1]<zEMA4[1])
     2. SELL:
            * zEMA3<zEMA4 and zEMA3[1]>zEMA4[1]




```
study(title="rsh", overlay=true)


SP1=input(14,title="S1")
LP1=input(28,title="L1")
SP2=input(9,title="S1")
LP2=input(19,title="L1")

ema1=ema(close,SP1)
emaema1=ema(close,2*SP1-1)

ema2=ema(close,LP1)
emaema2=ema(close,2*LP1-1)

ema3=ema(close,SP2)
emaema3=ema(close,2*SP2-1)

ema4=ema(close,LP2)
emaema4=ema(close,2*LP2-1)

zEMA1=2*ema1-emaema1
zEMA2=2*ema2-emaema2
zEMA3=2*ema3-emaema3
zEMA4=2*ema4-emaema4


plot((zEMA1>zEMA2 and zEMA3>zEMA4) and (zEMA1[1]<zEMA2[1] or zEMA3[1]<zEMA4[1]) ? close : na, style = circles, linewidth = 4,color=green)
plot(zEMA3<zEMA4 and zEMA3[1]>zEMA4[1] ? close : na, style = circles, linewidth = 4,color=red)

```
