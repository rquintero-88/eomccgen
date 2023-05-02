
# eomccgen

**eomccgen** is an algebra package that relies on second quantization and Wick's theorem to compute automatically normal-ordered strings (with respect to the Fermi vacuum) that corresponds to the following objects:

- Second-quantized strings in normal order 
- Coupled-cluster (CC) energy and amplitude equations
- Many-body terms of the similarity-transformed Hamiltonian
- Equation-of-motion coupled-cluster (EOM-CC) equations in terms of many-body terms
- Blocks of the EOM-CC Hamiltonian in terms of the many-body terms
 
## Installation

To use **eomccgen**, you must have [Wolfram Mathematica version 12.3](https://writings.stephenwolfram.com/2021/05/launching-version-12-3-of-wolfram-language-mathematica/) or higher installed on your computer (the program might work with an earlier version but it is guaranteed). Additionally, you may clone the present repository to access the necessary files via the following command:

```
git clone   https://github.com/rquintero-88/eomccgen.git
```

## Get Started!

### Generalized Wick's Theorem

In this example, we evaluate a string of second-quantized operators in normal order using Wick's theorem. 

Input:

```mathematica
SQString = {{SuperDagger[h1], SuperDagger[h2], p2, p1}, {SuperDagger[q1], SuperDagger[q2], q4, q3}, {{SuperDagger[v1], o1}}, {SuperDagger[p3], h3}};
CWick[SQString]
```

Output:

```mathematica
{KroneckerDelta[h1, h3] KroneckerDelta[o1, q2] KroneckerDelta[p2, q1] KroneckerDelta[p3, q3] KroneckerDelta[q4, v1], -KroneckerDelta[h1, h3] KroneckerDelta[o1, q2] KroneckerDelta[ p2, q1] KroneckerDelta[p3, q4] KroneckerDelta[q3, v1], -KroneckerDelta[h1, h3] KroneckerDelta[o1, q1] KroneckerDelta[p2, q2] KroneckerDelta[p3, q3] KroneckerDelta[q4, v1], KroneckerDelta[h1, h3] KroneckerDelta[o1, q1] KroneckerDelta[p2, q2] KroneckerDelta[p3, q4] KroneckerDelta[q3, v1], -KroneckerDelta[h1, q3] KroneckerDelta[h3, q1] KroneckerDelta[o1, q2] KroneckerDelta[p2, p3] KroneckerDelta[q4, v1],
KroneckerDelta[h1, q3] KroneckerDelta[h3, q2] KroneckerDelta[o1, q1] KroneckerDelta[p2, p3] KroneckerDelta[q4, v1], KroneckerDelta[h1, q4] KroneckerDelta[h3, q1] KroneckerDelta[o1, q2] KroneckerDelta[p2, p3] KroneckerDelta[q3, v1], -KroneckerDelta[h1, q4] KroneckerDelta[h3, q2] KroneckerDelta[o1, q1] KroneckerDelta[p2, p3] KroneckerDelta[q3, v1], -KroneckerDelta[h1, o1] KroneckerDelta[h3, q2] KroneckerDelta[p2, q1] KroneckerDelta[p3, q3] KroneckerDelta[q4, v1], KroneckerDelta[h1, o1] KroneckerDelta[h3, q2] KroneckerDelta[p2, q1] KroneckerDelta[p3, q4] KroneckerDelta[q3, v1],
 KroneckerDelta[h1, o1] KroneckerDelta[h3, q1] KroneckerDelta[p2, q2] KroneckerDelta[p3, q3] KroneckerDelta[q4, v1], -KroneckerDelta[h1, o1] KroneckerDelta[h3, q1] KroneckerDelta[p2, q2] KroneckerDelta[p3, q4] KroneckerDelta[q3, v1],  KroneckerDelta[h1, q3] KroneckerDelta[h3, q1] KroneckerDelta[o1, q2] KroneckerDelta[p2, v1] KroneckerDelta[p3, q4], -KroneckerDelta[h1, q3] KroneckerDelta[h3, q2] KroneckerDelta[o1, q1] KroneckerDelta[p2, v1] KroneckerDelta[p3, q4], -KroneckerDelta[h1, q4] KroneckerDelta[h3, q1] KroneckerDelta[o1, q2] KroneckerDelta[p2, v1] KroneckerDelta[p3, q3], 
 KroneckerDelta[h1, q4] KroneckerDelta[h3, q2] KroneckerDelta[o1, q1] KroneckerDelta[p2, v1] KroneckerDelta[p3, q3]}
```

### CC with with singles and doubles (CCD)

To generate the CCD energy and amplitude equations we define the following input

Input:

```mathematica
ClusterOperator = {{"1h1p"}, {"2h2p"}};
EOMOperator = {{"0h0p"}};
CCgen[ClusterOperator, EOMOperator]
```

Output:

```mathematica
'CCD Energy'
{1/4 ERI[[o1,o2,v1,v2]] t2[[o1,o2,v1,v2]]}
'T2 equations'
{-ERI[[p2,p1,h1,h2]]-F[[p2,v1]] t2[[h1,h2,v1,p1]]+F[[p1,v1]] t2[[h1,h2,v1,p2]]-1/2 ERI[[p2,p1,v1,v2]] t2[[h1,h2,v1,v2]]-F[[o1,h2]] t2[[o1,h1,p2,p1]]+ERI[[o1,p2,v1,h2]] t2[[o1,h1,v1,p1]]-ERI[[o1,p1,v1,h2]] t2[[o1,h1,v1,p2]]+F[[o1,h1]] t2[[o1,h2,p2,p1]]-ERI[[o1,p2,v1,h1]] t2[[o1,h2,v1,p1]]+ERI[[o1,p1,v1,h1]] 
t2[[o1,h2,v1,p2]]-1/2 ERI[[o1,o2,h1,h2]] t2[[o1,o2,p2,p1]]-1/4 ERI[[o1,o2,v1,v2]] t2[[h1,h2,v1,v2]] t2[[o1,o2,p2,p1]]-1/2 ERI[[o1,o2,v1,v2]] t2[[h1,h2,v2,p2]] t2[[o1,o2,v1,p1]]+1/2 ERI[[o1,o2,v1,v2]] t2[[h1,h2,v2,p1]] t2[[o1,o2,v1,p2]]-1/2 ERI[[o1,o2,v1,v2]] t2[[o1,h2,v1,v2]] t2[[o2,h1,p2,p1]]+ERI[[o1,o2,v1,v2]] t2[[o1,h2,v1,p2]] 
t2[[o2,h1,v2,p1]]+1/2 ERI[[o1,o2,v1,v2]] t2[[o1,h1,v1,v2]] t2[[o2,h2,p2,p1]]-ERI[[o1,o2,v1,v2]] t2[[o1,h1,v1,p2]] t2[[o2,h2,v2,p1]]}
```

### IP Equation of motion with CC singles and doubles (IP-EOM-CC)


In this example the IP-EOM-CCSD equations are generated thrue the following simple imput
Input:

```mathematica
ClusterOperator = {{"1h1p"}, {"2h2p"}};
EOMOperator = {{"1h0p"}, {"2h1p"}};
EOMCCgen[ClusterOperator, EOMOperator]
```
Output:

```mathematica

'Many-body terms'

\[Chi][[h3,h1]]==-F[[h3,h1]]-F[[h3,v1]] t1[[h1,v1]]+t1[[o1,v1]] ERI[[h3,o1,v1,h1]]+t1[[h1,v2]] t1[[o1,v1]] ERI[[h3,o1,v1,v2]]+1/2 ERI[[h3,o1,v1,v2]] t2[[o1,h1,v1,v2]]
\[Chi][[h4,p3]]==F[[h4,p3]]-t1[[o1,v1]] ERI[[h4,o1,v1,p3]]
\[Chi][[h4,h3,h1,p3]]==ERI[[h4,h3,h1,p3]]+t1[[h1,v1]] ERI[[h4,h3,v1,p3]]
\[Chi][[h3,p1,h1,h2]]==t1[[o1,p1]] ERI[[h3,o1,h1,h2]]-t1[[h2,v1]] t1[[o1,p1]] ERI[[h3,o1,v1,h1]]+t1[[h1,v1]] t1[[o1,p1]] ERI[[h3,o1,v1,h2]]+t1[[h1,v1]] t1[[h2,v2]] t1[[o1,p1]] ERI[[h3,o1,v1,v2]]-ERI[[h3,p1,h1,h2]]+t1[[h2,v1]] ERI[[h3,p1,v1,h1]]-t1[[h1,v1]] ERI[[h3,p1,v1,h2]]-t1[[h1,v1]] t1[[h2,v2]] ERI[[h3,p1,v1,v2]]-F[[h3,v1]] t2[[h1,h2,v1,p1]]+1/2 t1[[o1,p1]] ERI[[h3,o1,v1,v2]] t2[[h1,h2,v1,v2]]-1/2 ERI[[h3,p1,v1,v2]] t2[[h1,h2,v1,v2]]+t1[[o1,v1]] ERI[[h3,o1,v1,v2]] t2[[h1,h2,v2,p1]]-ERI[[h3,o1,v1,h2]] t2[[o1,h1,v1,p1]]+t1[[h2,v1]] ERI[[h3,o1,v1,v2]] t2[[o1,h1,v2,p1]]+ERI[[h3,o1,v1,h1]] t2[[o1,h2,v1,p1]]-t1[[h1,v1]] ERI[[h3,o1,v1,v2]] t2[[o1,h2,v2,p1]]
\[Chi][[p1,p3]]==F[[p1,p3]]-F[[o1,p3]] t1[[o1,p1]]-t1[[o1,v1]] t1[[o2,p1]] ERI[[o1,o2,v1,p3]]+t1[[o1,v1]] ERI[[o1,p1,v1,p3]]-1/2 ERI[[o1,o2,v1,p3]] t2[[o1,o2,v1,p1]]
\[Chi][[h4,h3,h1,h2]]==-ERI[[h4,h3,h1,h2]]+t1[[h2,v1]] ERI[[h4,h3,v1,h1]]-t1[[h1,v1]] ERI[[h4,h3,v1,h2]]-t1[[h1,v1]] t1[[h2,v2]] ERI[[h4,h3,v1,v2]]-1/2 ERI[[h4,h3,v1,v2]] t2[[h1,h2,v1,v2]]
\[Chi][[h4,p1,h2,p3]]==t1[[o1,p1]] ERI[[h4,o1,h2,p3]]+t1[[h2,v1]] t1[[o1,p1]] ERI[[h4,o1,v1,p3]]-ERI[[h4,p1,h2,p3]]-t1[[h2,v1]] ERI[[h4,p1,v1,p3]]-ERI[[h4,o1,v1,p3]] t2[[o1,h2,v1,p1]]
\[Chi][[h4,h3,p1,h1,h2,p3]]==ERI[[h4,h3,v1,p3]] t2[[h1,h2,v1,p1]]

'EOM-CC matrix in terms of many-body terms'

{{-\[Chi][[h3, h1]], -KroneckerDelta[h1, h4] \[Chi][[h3, p3]] + 
  KroneckerDelta[h1, h3] \[Chi][[h4, p3]] + \[Chi][[h4, h3, h1, p3]]},
 {-\[Chi][[h3, p1, h2, h1]], -KroneckerDelta[h2, h4] KroneckerDelta[p1, p3] \[Chi][[h3, h1]] + KroneckerDelta[h1, h4] KroneckerDelta[p1, p3] \[Chi][[h3, h2]] + KroneckerDelta[h2, h3] KroneckerDelta[p1, p3] \[Chi][[h4, h1]] - KroneckerDelta[h1, h3] KroneckerDelta[p1, p3] \[Chi][[h4, h2]] - KroneckerDelta[h1, h4] KroneckerDelta[h2, h3] \[Chi][[p1,  p3]] + KroneckerDelta[h1, h3] KroneckerDelta[h2, h4] \[Chi][[p1, p3]]
    - KroneckerDelta[h2, h4] \[Chi][[h3, p1, h1, p3]] + KroneckerDelta[h1, h4] \[Chi][[h3, p1, h2, p3]] + KroneckerDelta[p1, p3] \[Chi][[h4, h3, h2, h1]] +  KroneckerDelta[h2, h3] \[Chi][[h4, p1, h1, p3]] - KroneckerDelta[h1, h3] \[Chi][[h4, p1, h2, p3]] + \[Chi][[h4, h3,  p1, h2, h1, p3]]} }
```


### Single Blocks of DEA-EOM-CCSD  in  terms of many body terms.

It is possible to generate single blocks 

Input:

```mathematica
ClusterOperator = {{"1h1p"}, {"2h2p"}};
EOMOperator = {{"2h0p"}, {"3h1p"}};
EOMBlock = {2, 1};
EOMCCpBLOCKgen[ClusterOperator, EOMOperator, EOMBlock]
```

Output:

```mathematica

'Many-body terms'

\[Chi][[h5,p1,h2,h3]]==t1[[o1,p1]] ERI[[h5,o1,h2,h3]]-t1[[h3,v1]] t1[[o1,p1]] ERI[[h5,o1,v1,h2]]+t1[[h2,v1]] t1[[o1,p1]] ERI[[h5,o1,v1,h3]]+t1[[h2,v1]] t1[[h3,v2]] t1[[o1,p1]] ERI[[h5,o1,v1,v2]]-ERI[[h5,p1,h2,h3]]+t1[[h3,v1]] ERI[[h5,p1,v1,h2]]-t1[[h2,v1]] ERI[[h5,p1,v1,h3]]-t1[[h2,v1]] t1[[h3,v2]] ERI[[h5,p1,v1,v2]]-F[[h5,v1]] t2[[h2,h3,v1,p1]]+1/2 t1[[o1,p1]] ERI[[h5,o1,v1,v2]] t2[[h2,h3,v1,v2]]-1/2 ERI[[h5,p1,v1,v2]] t2[[h2,h3,v1,v2]]+t1[[o1,v1]] ERI[[h5,o1,v1,v2]] t2[[h2,h3,v2,p1]]-ERI[[h5,o1,v1,h3]] t2[[o1,h2,v1,p1]]+t1[[h3,v1]] ERI[[h5,o1,v1,v2]] t2[[o1,h2,v2,p1]]+ERI[[h5,o1,v1,h2]] t2[[o1,h3,v1,p1]]-t1[[h2,v1]] ERI[[h5,o1,v1,v2]] t2[[o1,h3,v2,p1]]
\[Chi][[h5,h4,h3,p1,h1,h2]]==ERI[[h5,h4,v1,h3]] t2[[h1,h2,v1,p1]]-t1[[h3,v1]] ERI[[h5,h4,v1,v2]] t2[[h1,h2,v2,p1]]-ERI[[h5,h4,v1,h2]] t2[[h1,h3,v1,p1]]+t1[[h2,v1]] ERI[[h5,h4,v1,v2]] t2[[h1,h3,v2,p1]]+ERI[[h5,h4,v1,h1]] t2[[h2,h3,v1,p1]]-t1[[h1,v1]] ERI[[h5,h4,v1,v2]] t2[[h2,h3,v2,p1]]

'Block (2,1)'

KroneckerDelta[h3, h5] \[Chi][[h4, p1, h2, h1]] + KroneckerDelta[h2, h5] \[Chi][[h4, p1, h3, h1]] + KroneckerDelta[h1, h5] \[Chi][[h4, p1, h3, h2]] - KroneckerDelta[h3, h4] \[Chi][[h5, p1, h2, h1]] - 
 KroneckerDelta[h2, h4] \[Chi][[h5, p1, h3, h1]] -  KroneckerDelta[h1, h4] \[Chi][[h5, p1, h3, h2]] - \[Chi][[h5, h4, p1, h3, h2, h1]]

```


### Single Many-body terms using a Hamiltonian.

Input:

```mathematica
ClusterOperator = {{"1h1p"}, {"2h2p"}};
EOMOperator = {{"0h0"}};
ManyBodyOp = {{{p1}, {SuperDagger[p3], SuperDagger[p4], 
     h3}}, {{SuperDagger[h1], p2, p1}, {SuperDagger[p3]}}};
ManyBodyTermsEOM[ClusterOperator, EOMOperator, ManyBodyOp]
```

Output:

```Mathematica

'Many Body Terms'
\[Chi][[h3,p1,p4,p3]]==-t1[[o1,p1]] ERI[[h3,o1,p4,p3]]+ERI[[h3,p1,p4,p3]]
\[Chi][[p2,p1,h1,p3]]==t1[[o1,p2]] t1[[o2,p1]] ERI[[o1,o2,h1,p3]]+t1[[h1,v1]] t1[[o1,p2]] t1[[o2,p1]] ERI[[o1,o2,v1,p3]]-t1[[o1,p2]] ERI[[o1,p1,h1,p3]]-t1[[h1,v1]] t1[[o1,p2]] ERI[[o1,p1,v1,p3]]+t1[[o1,p1]] ERI[[o1,p2,h1,p3]]+t1[[h1,v1]] t1[[o1,p1]] ERI[[o1,p2,v1,p3]]+ERI[[p2,p1,h1,p3]]+t1[[h1,v1]] ERI[[p2,p1,v1,p3]]+F[[o1,p3]] t2[[o1,h1,p2,p1]]-ERI[[o1,p2,v1,p3]] t2[[o1,h1,v1,p1]]+ERI[[o1,p1,v1,p3]] t2[[o1,h1,v1,p2]]+1/2 ERI[[o1,o2,h1,p3]] t2[[o1,o2,p2,p1]]+1/2 t1[[h1,v1]] ERI[[o1,o2,v1,p3]] t2[[o1,o2,p2,p1]]+t1[[o1,v1]] ERI[[o1,o2,v1,p3]] t2[[o2,h1,p2,p1]]-t1[[o1,p2]] ERI[[o1,o2,v1,p3]] t2[[o2,h1,v1,p1]]+t1[[o1,p1]] ERI[[o1,o2,v1,p3]] t2[[o2,h1,v1,p2]]
```

## Convention


### Index Convention.

For the operators belonging to the bra and the ket, we use p1, p2, $\cdots$,h1, h2,  $\cdots$. 
For the particles/holes that play the role of dummy indices in the cluster operator $\hat{T}$ we use o1, o2, $\cdots$, v1,v2 $\cdots$, where the notation of o and v refers to occupied and virtual, respectively.
Finally, for the arbitrary indexes that could be either particle or hole to q1, q2, q3, $\cdots$.



List of variables using in eomccgen


| Description            | Mathematical symbol | Mathematica notation       |
|------------------------|---------------------|----------------------------|
| Fock elements          | $f_{q}^{p}$         | F[[p,q]]                   |
| Two-electon integrals  | $v_{rs}^{pq}$       | ERI[[p,q,r,s]]             |
| Single amplitudes      | $t_{i}^{a}$         | t1[[i,a]]                  |
| Double amplitudes      | $t_{ij}^{ab}$       | t2[[i,j,a,b]]              |
| Triple amplitudes      | $t_{ijk}^{abc}$     | t3[[i,j,k,a,b,c]]          |
| Quadruple amplitudes   | $t_{ijkl}^{abcd}$   | t4[[i,j,k,l,a,b,c,d]]      |
| One-body terms         | $\chi_{q}^{p}$      | $\chi$1[[p,q]]             |
| Two-body terms         | $\chi_{qs}^{pq}$    | $\chi$2[[p,q,r,s]]         |
| Three-body terms       | $\chi_{stu}^{pqr}$  | $\chi$2[[p,q,r,s,t,u]]     |
| Four-body terms        | $\chi_{tuvw}^{pqrs}$| $\chi$3[[p,q,r,s,t,u,v,w]] |


## Citation

```
@misc{rauleomccgen2023,
  title = {eomccgen},
  author = {Quintero-Monsebaiz,Raul  and Loos,Pierre-François},
  year = {2023},
  publisher = {GitHub},
  url={https://github.com/rquintero-88/eomccgen.git}
  }
```


