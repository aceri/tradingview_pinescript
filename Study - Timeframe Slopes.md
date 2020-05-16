Timeframe Slopes:

![Timeframe Slopes](https://i.imgur.com/ShsAN7V.png)

And its performance:

![Timeframe Slopes Performance](https://i.imgur.com/ImSEw3G.png)




```

strategy("Timeframe Slopes",overlay=false)
c=input(close)

p1=input(30,title="First Slope Period 1h", type=integer, minval=2,maxval=600)
p2=input(90,title="Second Slope Period 4h", type=integer, minval=2, maxval=600)
p3=input(360, title="Third Slope Period 12h", type=integer, minval=2,maxval=840)
p4=input(720, title="Fourth Slope Period 24h", type=integer, minval=2,maxval=1680)


slope(a,b)=>(linreg(a,b,0)-linreg(a,b,0)[b])/b

w1=1.5
w2=1.25
w3=0.75
w4=0.5

s1 = (slope(c,p1) + slope(c,p1/2))/2 * w1
s2 = (slope(c,p2) + slope(c,p2/2))/2 * w2
s3 = (slope(c,p3) + slope(c,p3/2))/2 * w3
s4 = (slope(c,p4) + slope(c,p4/2))/2 * w4
sx = (s1+s2+s4+s4)/(w1+w2+w3+w4)*2


plot(s1,color=s1>s1[1]?white:s1<s1[1]?orange:na,style=line,linewidth=1)
plot(s2,color=s2>s2[1]?white:s2<s2[1]?orange:na,style=line,linewidth=2)
plot(s3,color=s3>s3[1]?white:s3<s3[1]?orange:na,style=line,linewidth=3)
plot(s4,color=s4>s4[1]?white:s4<s4[1]?orange:na,style=line,linewidth=4)
plot(sx,color=sx>sx[1]?green:red,style=line,linewidth=4)

strategy.entry("enter long", true, 1000, when = sx>sx[1]) // enter long by market if current open great then previous high
strategy.entry("enter short", false, 1000, when = sx<sx[1]) // enter short by market if current open less then previous low

```
