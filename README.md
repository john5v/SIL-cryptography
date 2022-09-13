# SIL-cryptography
SIL cryptography base upon multiplication inverse modulo

    

   **Problem**
   major problem in inverse modulo base cryptography, key recovery
   
   **solution**   
        we know multiplicate inverse thoream
        a*b = l (mod d)
        
        we have three value a,b and l ( ignore  d)
        we know two value than easily get third value

        but if we have only one value you cant get left two parameter
        (pigeon problem) 



## SIL  Eq 
                  b =       l/a  
        SIL1  eq: c = (m*u+v)/(m*y+z) 
        SIL2  eq: c = (v-m*z)/(m*y-u)   //reverse of SIL1 eq 

**Note**: devision represent multiplicate inverse modulo 


## theory 
        multiplication inverse thoream 
        a*b = l (mod d)      
        d belong to finite field Z10
        d = 10^n    (n number of digit) 
        0 < a < d 
        0 < b < d
        gcd(a,d)= 1 

        l reblace by m*u+v 
        a replace by m*y+z
        b replace by c 

        put a, b and l in eq  a*b =l         
        (m*y+z)*c = m*u+v 
        
        so we write 
        c = m*u+v/m*y+z 



   **NOTE**: if you study more read cyclic group, ring, field and number theory 

## variable last digit table 
   fix last digit in each variable make **gcd(a,d)**  and **gcd(b,d)** always be 1
   
     var :   last digit    
     u :     0             
     v :     1        
     y :     1        
     z :     0        
     m :    1        
 we chose 1 and 0 because that suitable for both  binary(Z2) and decimal(Z10) 


## 3LE (3 layer encryption)  
SIL1 eq  two major draw back first **partial match** and  second **next digit**



        layer
        1.  b = m*u+v/m*y+z 
        2.  b = reverse((b-1)/10) *10+1
        3.  c = v-b*z/b*y-u
        
        3LE design 
        * we design same function for encraption and decraption 
        * use 8 key, 4 key by first layer, 4 key by third layer 

   ###  3LE mathod overcome two major issue 
   1. partial match

            example:  
                key u = 35790, v = 12351, y = 98761, z = 65810
                    
                //--------------------------------encrapt use sil1 eq 
                m1 = 75311
                c1 = (m1*u + v)/(m1*y + z)
                c1 = 12761

                m2 = 94311
                c2 = (m1*u + v)/(m1*y + z)
                c2 = 43761

                both cipher partial match 
                c1 = 12 761
                c2 = 43 761
                
                //--------------------------------encrapt use D3LE    //D for decimal 
                c1 = D3LE(7531,[3579,1235,9876,6581],4)
                c1 = 55861

                c2 = D3LE(9431,[3579,1235,9876,6581],4)
                c2 = 40131

                c1 and c2 no  partial match 

   2. next digit   
            use SIL1 cipher
             c1 = 12 761
            c2 = 43 761
                         in c1 next digit 0 to 9 
            
            
            
  

 ## block cipher 
 **encraption**: c = 3LE(m,k,n)
 
 **decraption**: m = 3LE(c,k,n) 
     
   m msg,  c cipher,  n number of digit and     k keys 

    
   
  ### pain text attack 
   **NOTE**: this attack base upon SIL1 eq 

            assume key: u,v,y and z 
            assume msg: m1 and m2 

            put in sil1 eq and get
            m1*u+v/m1*y+z   = c1    eq1
            m2*u+v/m1*y+z  = c2   eq2

            eq1 and eq2 
            c2 - c1 = (m2*u+v/m2*y+z) - (m1*u+v/m1*y+z)

            solve it 
            y*(c2*m2-c1*m1) + z*(c2-c1) = u*(m2-m1)
 at least require two key to get left  two key 
        
### liner analysis attack, relative key attack and relative plain text attack
this type attack work on SIL1-eq that why we use 3LE  method in symmetric encraption 

  ###  SP-network attack
  this type of attack made for SP-network so not work on  multiplicate inverse modulo
  ### Brute force 
  this attack work, how much time require depand upon key length and key config 



