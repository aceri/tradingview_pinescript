Study - RSI Divergences. Normalized.

![RSI Divergences](https://i.imgur.com/Rd6eopp.png)

```

study("RSI Divergences h", overlay=false)

norm(a,b,c)=>c*((a-lowest(a,b))/(highest(a,b)-lowest(a,b)))
slope(a,b)=>(linreg(a,b,0)-linreg(a,b,0)[b])/b
smooth(a,b)=>linreg(linreg(linreg(a,b,0),b*2,0),b*9,0)
nvel(a,b)=>norm((a-a[b])/b,b*5,100)

Multiplier=input(2.5,title="Multiplier",minval=1,maxval=2)
RSIPeriod=input(14,title="RSI Period",minval=2,maxval=500,type=integer)
NP=input(500,title="Normalization Period",minval=4,maxval=500,type=integer)
S=input(3,title="Smoothing",minval=3,maxval=50,type=integer)

c=norm(close,NP,100)

r=rsi(c,RSIPeriod)

OB=50+(Multiplier*stdev(r,RSIPeriod))
OS=50-(Multiplier*stdev(r,RSIPeriod))

dv1=linreg(r,RSIPeriod*1,0)/linreg(c,RSIPeriod*1,0)*25
dv2=linreg(r,RSIPeriod*2,0)/linreg(c,RSIPeriod*2,0)*25
dv3=linreg(r,RSIPeriod*3,0)/linreg(c,RSIPeriod*3,0)*25
dvx=norm(dv1+dv2+dv3,50,100)

ratio=smooth(r,S)/smooth(c,S)

sr=smooth(r,S)
sc=smooth(c,S)

plot(100,color=dvx>50?#aaaaaa:#666666,style=area,transp=50,linewidth=1)
plot(nvel(ratio,RSIPeriod),color=gray,style=areabr,transp=60,linewidth=1)
plot(100,color=dvx>50?#aaaaaa:#666666,style=area,transp=80,linewidth=1)

plot(70,color=gray,style=line,transp=70)
plot(72,color=#343434,style=line,transp=70,linewidth=1)
plot(30,color=gray,style=line,transp=70)
plot(32,color=#343434,style=line,transp=70,linewidth=1)



plot(sr+1,color=#c4c494,style=line,transp=0,linewidth=1)
plot(sr-1,color=#101010,style=line,transp=0,linewidth=1)
plot(sr,color=orange,style=line,transp=0,linewidth=2)
plot(sc+1,color=#949494,style=line,transp=0,linewidth=1)
plot(sc-1,color=#101010,style=line,transp=0,linewidth=1)
plot(sc,color=white,style=line,transp=0,linewidth=2)

```
