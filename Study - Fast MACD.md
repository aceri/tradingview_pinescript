Study - Fast MACD

![Fast MACD](https://i.imgur.com/FEO0ueT.png)

Using Zero Lag EMAs and Zero Lag DEMAs

```

study(title="FMACD", shorttitle="FMACD")
source = close

zlema(a,b) => 2*ema(a,b)-ema(a,2*b-1)
zldema(a,b)=> 2*zlema(a,b)-zlema(a,2*b-1)
slope(a,b)=>(a-a[b])/b

fastLength = input(13, minval=1), slowLength=input(21,minval=1)
signalLength=input(8,minval=1)
fMA = zldema(source, fastLength)
sMA = zldema(source, slowLength)
fastMA=tan(atan(slope(fMA,fastLength)))
slowMA=tan(atan(slope(sMA,slowLength)))
macd = fastMA - slowMA

signal = zlema(macd, signalLength)
hist = macd - signal
plot(hist, style=histogram, color=gray, linewidth=1)
plot(macd, color=orange, linewidth=1)
plot(signal, color=white, linewidth=1)

plot(cross(zldema(signal,3), zldema(macd,3)) ? signal : na, color=yellow, style = circles, linewidth = 2)
OutputSignal = signal >= macd ? 1 : 0
bgcolor(OutputSignal>0?#565656:black, transp=80)

```
