# Prime Factorization
```Python


n= int(input())
i= int(2)
a=str()
while i <= n:
    if n% i==0:
        a= a+ str(i) + " "
        n= n/i
    else: i+= 1    
print(a)     
    
    
```
