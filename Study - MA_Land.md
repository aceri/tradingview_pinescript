![Chart with most important Medium Averages appearing when close](https://i.imgur.com/MpCap9s.png)

* Study MA_Land
* Based on 4H displays the most usual MAs (30,50,100,200) for all the timeframes from 30m to Yearly. It displays those above actual price acting as resistance of below acting as support under optional percents. It can also hide above/below another percent.

```

//@version=3
study("MA-Land",overlay=true)
SupRes_SMA(instr,p,sup_pct,res_pct,out_pct)=>instr/sma(instr,p)>1 and instr/sma(instr,p)<(1+sup_pct/1000)?1:instr/sma(instr,p)<1 and instr/sma(instr,p)>(1-sup_pct/1000)?2:instr/sma(instr,p)>(1+out_pct/1000) or sma(instr,p)/instr>(1+out_pct/1000)?4:3
SupRes_SMA_Col(instr,p,sup_pct,res_pct,out_pct)=>SupRes_SMA(instr,p,sup_pct,res_pct,out_pct)==1?green:SupRes_SMA(instr,p,sup_pct,res_pct,out_pct)==2?red:SupRes_SMA(instr,p,sup_pct,res_pct,out_pct)==3?gray:na

SupRes_SMAB(instr,p,sup_pct,res_pct,out_pct)=>instr/ema(instr,p)>1 and instr/ema(instr,p)<(1+sup_pct/1000)?1:instr/ema(instr,p)<1 and instr/ema(instr,p)>(1-sup_pct/1000)?2:instr/ema(instr,p)>(1+out_pct/1000) or ema(instr,p)/instr>(1+out_pct/1000)?4:3
SupRes_SMA_ColB(instr,p,sup_pct,res_pct,out_pct)=>SupRes_SMAB(instr,p,sup_pct,res_pct,out_pct)==1?aqua:SupRes_SMAB(instr,p,sup_pct,res_pct,out_pct)==2?orange:SupRes_SMAB(instr,p,sup_pct,res_pct,out_pct)==3?gray:na

lin(lw)=>
    valor=round(log(lw))
    valor

sup_pct=input(title="Support %",type=integer,defval=200,minval=0,maxval=1000)
res_pct=input(title="Resistance %",type=integer,defval=200,minval=0,maxval=1000)
out_pct=input(title="Out of view %",type=integer,defval=200,minval=0,maxval=1000)
instr=close

plot(sma(instr,30),"MA_4H_30",color=SupRes_SMA_Col(instr,30,sup_pct,res_pct,out_pct),linewidth=0.5)
plot(sma(instr,50),"MA_4H_50",color=SupRes_SMA_Col(instr,50,sup_pct,res_pct,out_pct),linewidth=1)
plot(sma(instr,100),"MA_4H_100",color=SupRes_SMA_Col(instr,100,sup_pct,res_pct,out_pct),linewidth=1)
plot(sma(instr,200),"MA_4H_200",color=SupRes_SMA_Col(instr,200,sup_pct,res_pct,out_pct),linewidth=1)

plot(sma(instr,300),"MA_6H_200",color=SupRes_SMA_Col(instr,300,sup_pct,res_pct,out_pct),linewidth=3)
plot(sma(instr,45*2),"MA_12H_30",color=SupRes_SMA_Col(instr,45*2,sup_pct,res_pct,out_pct),linewidth=0.5)
plot(sma(instr,75*2),"MA_12H_50",color=SupRes_SMA_Col(instr,75*2,sup_pct,res_pct,out_pct),linewidth=1)
plot(sma(instr,150*2),"MA_12H_100",color=SupRes_SMA_Col(instr,150*2,sup_pct,res_pct,out_pct),linewidth=2)
plot(sma(instr,300*2),"MA_12H_200",color=SupRes_SMA_Col(instr,300*2,sup_pct,res_pct,out_pct),linewidth=3)

plot(sma(instr,75*2*2),"MA_1D_50",color=SupRes_SMA_Col(instr,75*2*2,sup_pct,res_pct,out_pct),linewidth=1)
plot(sma(instr,150*2*2),"MA_1D_100",color=SupRes_SMA_Col(instr,150*2*2,sup_pct,res_pct,out_pct),linewidth=2)
plot(sma(instr,300*2*2),"MA_1D_200",color=SupRes_SMA_Col(instr,300*2*2,sup_pct,res_pct,out_pct),linewidth=2)

plot(sma(instr,45*2*2*3),"MA_3D_30",color=SupRes_SMA_Col(instr,45*2*2*3,sup_pct,res_pct,out_pct),linewidth=2)
plot(sma(instr,75*2*2*3),"MA_3D_50",color=SupRes_SMA_Col(instr,75*2*2*3,sup_pct,res_pct,out_pct),linewidth=2)
plot(sma(instr,150*2*2*3),"MA_3D_100",color=SupRes_SMA_Col(instr,150*2*2*3,sup_pct,res_pct,out_pct),linewidth=2)
plot(sma(instr,300*2*2*3),"MA_3D_200",color=SupRes_SMA_Col(instr,300*2*2*3,sup_pct,res_pct,out_pct),linewidth=3)

plot(sma(instr,75*2*2*7),"MA_1W_50",color=SupRes_SMA_Col(instr,75*2*2*7,sup_pct,res_pct,out_pct),linewidth=2)
plot(sma(instr,150*2*2*7),"MA_1W_100",color=SupRes_SMA_Col(instr,150*2*2*7,sup_pct,res_pct,out_pct),linewidth=4)

plot(sma(instr,1*365*6),"MA_1Y_1",color=SupRes_SMA_Col(instr,1*365*6,sup_pct,res_pct,out_pct),linewidth=5)
plot(sma(instr,2*365*6),"MA_1Y_2",color=SupRes_SMA_Col(instr,2*365*6,sup_pct,res_pct,out_pct),linewidth=5)

```
