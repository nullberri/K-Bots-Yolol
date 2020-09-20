Chip 1 thrust converter:
```
j=100 goto 5
x=:o>0 y=(abs :o)>j :f=x*(y*:m+(1-y)*:o/j*:m)  goto3-x+(1-:r+:nt)*2
h=abs :o x=:o<0 y=h>j :b=x*(y*:n+(1-y)*h/j*:n) gotox+2+(1-:r+:nt)*2
goto 13
goto 13
goto 13
goto 13
goto 13
goto 13
goto 13
goto 13
goto 13
:f=0 :b=0
goto (:r>0)+1+(1-:r)*13
```


chip 2 pid:
```
pe=0 l=999 goto :r+1
:e=:in-:sp :de=pe-:e :o=((:Kp*:e)+(:Kd*:de)) :nt=:in>l pe=:e goto:r*+1
```

chip 3 status:
```
a="\nApproaching" b="\nArrived" d="\nNO TARGET" h="\nTGT: " 
j="\nDelta: " g="\nFWD: " k="\nOFFLINE" i="BK: "

if 1-:r then :msg=k goto 4 end 
if :r*:in>999 then :msg=d end e=:e-(:e-:e%1)
if :r*:in<999 then :msg=h+:sp+j+e+g+:f+i+:b end goto 4
```


Memory filter Input

| left memory chip  | right memory chip   | notes|
|---|---|---|
| RangeFinderDistance | in | distance to target |
| ApproachRange  | sp  | the distance you want to arrive at |
| ApproachEnabled | r | is the system enabled |
| MaxFwdThrust  | m | max forward thrust the system can use, suggest 20 |
| Kd  | kd | the derivative value, this number is multipled by the speed your arriving at, it should be less than kp|
| Kp  | kp | the proportional value, the higher the number the fast you arrive, but if your a heavy ship you will have a lot of momentum |
| MaxBkThrust  | n  | max backward thrust, suggest 500 as this will guarentee max backing thrust when ever its needed |


Memory filter output

| left memory chip  | right memory chip   | notes |
|---|---|---|
| f | fcuForward | |
| msg  | _Approach | this can be anything, its just name of the panel where it can display its status| 
| b  | fcuBackward | |
| de |  | |
| e  |  | | 
| o  |  | | 
| h  |   | | 
| nt | | | 


once installed to tune the approacher pick a max thrust your comfortable with, suggest 20,
then set the KP to 5, Kd to 0, appraochRange to 50 back up your ship 100m and hit approach.
Raise or lower your Kp value until the maximum you over shoot is about 10m
Start raising your Kd value untill you arrive just shy of your approach range.

for refrence my 800mv hualer uses 
3.92 Kp
3.71 Kd
MaxThrust 20

and it tends to need me to goose the throttle a little if i don't have much mommentum as i get get down to my approach range.

![approacher module](https://raw.githubusercontent.com/nullberri/K-Bots-Yolol/master/images/approacher.png)
