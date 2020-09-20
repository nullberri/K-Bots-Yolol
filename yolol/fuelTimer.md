You need atleast one FuelChamber renamed to Fuel and FuelMax and one NetworkGasStoredResouce to Gas and MaxGas
and atleast 1 battery named Battery


//percent output
```
e="ERROR" ok="OK" mb="\nBat  "  n="\n"
fuel=(:Fuel/:MaxFuel)*100 fuel-=fuel%1 bp=:Battery/100 bp-=bp%1
gas=:Gas/:MaxGas*100 gas-=gas%1 pe=(c<1)*(bp<50)+c*(bp<89) ge=gas<10
fe=fuel<10 c=fe+ge+pe if c then s=e :err++ else s=ok end
:power=s+mb+bp+"%\nFuel "+fuel+"%\n"+:ftime+"\nGas "+gas+"%\n"+:gTime
goto 1
```


// HH:MM ouput
```
g=:Gas h="h" s="m" 
f=:Fuel  t=0 tsec=5 tmax=tsec*5    tS=3600/tsec
t++ x/=t<tmax goto 3
gH=g/(g-:Gas)/tS gm=(gh%1)*60 gh-=gh%1 gm-=gm%1 gO=""+gH+h+gM+s
fh=f/(f-:Fuel)/tS fm=(fh%1)*60 fh-=fh%1 fm-=fm%1 fO=""+fH+h+fM+s
:gTime=gO :fTime=fO goto 1
```
