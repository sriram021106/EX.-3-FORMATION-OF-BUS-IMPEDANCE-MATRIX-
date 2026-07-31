# EX.-3-FORMATION-OF-BUS-IMPEDANCE-MATRIX-
# AIM: 
To write a computer program to form Bus Impedance matrix Z, given the impedances 
of a power network and their connectivity.

# SOFTWARE REQUIRED: 
Mat Lab Software. 

# ALGORITHM: 
```
Step wise procedure to build “Z” Matrix. 
Step 1 : 
Start with a partial network composed only of those elements connected directly to reference 
node. Let the number of these elements be r.  The corresponding bus impedance matrix Z(1) is 
of dimension r x r and is diagonal with the impedance values of the elements appearing on 
the diagonal.  This process is equivalent to the repeated use of Rule 1. 
Zm  
Where Z is the impedance matrix of partial Network. 
Step 2: 
Add a new element which brings a new node and modify z(1) using Rule 2. 
Zm  
Where Zi is the ith Column of Z 
Zi T  is the transpose of Zi 
Zii  is the iith element of Z 
Step 3 : 
Add a new element connected between existing nodes i and j using Rule 3.  Continue until all 
the elements are connected.
```
Program:
```
clc;  
clear all;  
close all 
%      From     To      R+jX        Identi 
ldata=[ 0         1        1.2j           0 
            0         2        1.5j           0 
            1         2        0.2j           1 
  1     3        0.3j           0 
  2     3        0.15j    1] 
FB=ldata(:,1); TB=ldata(:,2); ZB=ldata(:,3); 
LI=ldata(:,4); nbr=length(FB); nbus=max(max(FB),max(TB)); 
%RULE-1 
for I=1:nbr 
if FB(I)==0 |TB(I)==0 
        K=max(FB(I),TB(I)); 
        Zbus(K,K)=ZB(I); 
    end; 
end; 
%RULE-2 
for I=1:nbr; 
    if FB(I)>0 & TB(I)>0 
        if LI(I)==0 
            Zbus(:,TB(I))=Zbus(:,FB(I)); 
            Zbus(TB(I),:)=Zbus(FB(I),:); 
            Zbus(TB(I),TB(I))=ZB(I)+Zbus(TB(I),TB(I)); 
        end; 
    end; 
end; 
%RULE-3 
for I=1:nbr; 
    if FB(I)>0 & TB(I)>0
if LI(I)==1 
DelZ=Zbus(:,TB(I))-Zbus(:,FB(I)); 
ZLL=ZB(I)+Zbus(TB(I),TB(I))+Zbus(FB(I),FB(I))-2*Zbus(FB(I),TB(I)); 
P=DelZ*DelZ.'/(ZLL); 
Zbus=Zbus-P; 
end; 
end; 
end; 
ZBUS=Zbus
```
# OUTPUT:

<img width="1087" height="552" alt="image" src="https://github.com/user-attachments/assets/eaafded8-f922-4249-8e7d-6af3dd4867fc" />


# RESULT: 
Bus impedance Matrix for the given network is formed using Mat Lab program and 
verified the calculated values with the output result.
