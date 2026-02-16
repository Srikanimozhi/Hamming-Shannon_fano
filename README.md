# Huffman-Shannon_fano
# Aim:
Consider a discrete memoryless source with symbols and statistics {0.125, 0.0625, 0.25, 0.0625, 0.125, 0.125, 0.25} for its output. 
Apply the Huffman and Shannon-Fano to this source. 
Show that by drawing the tree diagram, and 
Calculate the average code word length, entropy, variance, redundancy, and efficiency.
# Tools Required:

# Program:
```asm
import heapq, math

p=[0.125,0.0625,0.25,0.0625,0.125,0.125,0.25]
s=['A','B','C','D','E','F','G']
d=list(zip(s,p))

# Huffman
h=[[w,[x,""]] for x,w in d]; heapq.heapify(h)
while len(h)>1:
    l,r=heapq.heappop(h),heapq.heappop(h)
    for i in l[1:]: i[1]='0'+i[1]
    for i in r[1:]: i[1]='1'+i[1]
    heapq.heappush(h,[l[0]+r[0]]+l[1:]+r[1:])
hf=dict(h[0][1:])

# Shannon-Fano
sf={}
def f(d,c=""):
    if len(d)==1: sf[d[0][0]]=c; return
    t=sum(x[1] for x in d); s1=0
    for i in range(len(d)):
        s1+=d[i][1]
        if s1>=t/2: break
    f(d[:i+1],c+'0'); f(d[i+1:],c+'1')
f(sorted(d,key=lambda x:x[1],reverse=True))

# Common Calculations
H=sum(pi*math.log2(1/pi) for pi in p)

def result(code,name):
    L=sum(p[i]*len(code[s[i]]) for i in range(len(p)))
    eff=H/L; red=1-eff
    var=sum(p[i]*(len(code[s[i]])-L)**2 for i in range(len(p)))
    print("\n",name)
    print("Average Length =",round(L,3))
    print("Efficiency =",round(eff,3))
    print("Redundancy =",round(red,3))
    print("Variance =",round(var,3))

print("Entropy =",round(H,3))

print("\nHuffman Codes:",hf)
result(hf,"Huffman Performance")

print("\nShannon-Fano Codes:",sf)
result(sf,"Shannon-Fano Performance")

```asm

#Calculation:
```
Compare the manually calculated value and the observed practical value.
```
# Output
```

<img width="1058" height="382" alt="image" src="https://github.com/user-attachments/assets/f909a83f-1157-4d49-ab30-11d48eb26b90" />

``` 
# Results:
```
Write the conclusion
```
