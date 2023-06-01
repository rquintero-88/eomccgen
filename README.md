
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
{KroneckerDelta[h1,h3]KroneckerDelta[o1,q2]KroneckerDelta[p2,q1]KroneckerDelta[p3,q3]KroneckerDelta[q4,v1],-KroneckerDelta[h1,h3]KroneckerDelta[o1,q2]KroneckerDelta[p2,q1]KroneckerDelta[p3,q4]KroneckerDelta[q3,v1],-KroneckerDelta[h1,h3]KroneckerDelta[o1,q1]KroneckerDelta[p2,q2]KroneckerDelta[p3,q3]KroneckerDelta[q4,v1],KroneckerDelta[h1,h3]KroneckerDelta[o1,q1]KroneckerDelta[p2,q2]KroneckerDelta[p3,q4]KroneckerDelta[q3,v1],-KroneckerDelta[h1,q3]KroneckerDelta[h3,q1]KroneckerDelta[o1,q2]KroneckerDelta[p2,p3]KroneckerDelta[q4,v1],
KroneckerDelta[h1,q3]KroneckerDelta[h3,q2]KroneckerDelta[o1,q1]KroneckerDelta[p2,p3]KroneckerDelta[q4,v1],KroneckerDelta[h1,q4]KroneckerDelta[h3,q1]KroneckerDelta[o1,q2]KroneckerDelta[p2,p3]KroneckerDelta[q3,v1],-KroneckerDelta[h1,q4]KroneckerDelta[h3,q2]KroneckerDelta[o1,q1]KroneckerDelta[p2,p3]KroneckerDelta[q3,v1],-KroneckerDelta[h1,o1]KroneckerDelta[h3,q2]KroneckerDelta[p2,q1]KroneckerDelta[p3,q3]KroneckerDelta[q4,v1],KroneckerDelta[h1,o1]KroneckerDelta[h3,q2]KroneckerDelta[p2,q1]KroneckerDelta[p3,q4]KroneckerDelta[q3,v1],
KroneckerDelta[h1,o1]KroneckerDelta[h3,q1]KroneckerDelta[p2,q2]KroneckerDelta[p3,q3]KroneckerDelta[q4,v1],-KroneckerDelta[h1,o1]KroneckerDelta[h3,q1]KroneckerDelta[p2,q2]KroneckerDelta[p3,q4]KroneckerDelta[q3,v1],KroneckerDelta[h1,q3]KroneckerDelta[h3,q1]KroneckerDelta[o1,q2]KroneckerDelta[p2,v1]KroneckerDelta[p3,q4],-KroneckerDelta[h1,q3]KroneckerDelta[h3,q2]KroneckerDelta[o1,q1]KroneckerDelta[p2,v1]KroneckerDelta[p3,q4],-KroneckerDelta[h1,q4]KroneckerDelta[h3,q1]KroneckerDelta[o1,q2]KroneckerDelta[p2,v1]KroneckerDelta[p3,q3],
KroneckerDelta[h1,q4]KroneckerDelta[h3,q2]KroneckerDelta[o1,q1]KroneckerDelta[p2,v1]KroneckerDelta[p3,q3]}
```

### CC with doubles (CCD)

To generate the CCD energy and amplitude equations, one must define the following input

Input:

```mathematica
ClusterOperator = {{"2h2p"}};
EOMOperator = {{"0h0p"}};
CCgen[ClusterOperator,EOMOperator]
```

Output:

```mathematica
'CC Energy'
{1/4 ERI[[o1,o2,v1,v2]] t2[[o1,o2,v1,v2]]}
'CC Amplitude equations'
{-ERI[[p2,p1,h1,h2]]-F[[p2,v1]] t2[[h1,h2,v1,p1]]+F[[p1,v1]] t2[[h1,h2,v1,p2]]-1/2 ERI[[p2,p1,v1,v2]] t2[[h1,h2,v1,v2]]-F[[o1,h2]] t2[[o1,h1,p2,p1]]+ERI[[o1,p2,v1,h2]] t2[[o1,h1,v1,p1]]-ERI[[o1,p1,v1,h2]] t2[[o1,h1,v1,p2]]+F[[o1,h1]] t2[[o1,h2,p2,p1]]-ERI[[o1,p2,v1,h1]] t2[[o1,h2,v1,p1]]+ERI[[o1,p1,v1,h1]] 
t2[[o1,h2,v1,p2]]-1/2 ERI[[o1,o2,h1,h2]] t2[[o1,o2,p2,p1]]-1/4 ERI[[o1,o2,v1,v2]] t2[[h1,h2,v1,v2]] t2[[o1,o2,p2,p1]]-1/2 ERI[[o1,o2,v1,v2]] t2[[h1,h2,v2,p2]] t2[[o1,o2,v1,p1]]+1/2 ERI[[o1,o2,v1,v2]] t2[[h1,h2,v2,p1]] t2[[o1,o2,v1,p2]]-1/2 ERI[[o1,o2,v1,v2]] t2[[o1,h2,v1,v2]] t2[[o2,h1,p2,p1]]+ERI[[o1,o2,v1,v2]] t2[[o1,h2,v1,p2]] 
t2[[o2,h1,v2,p1]]+1/2 ERI[[o1,o2,v1,v2]] t2[[o1,h1,v1,v2]] t2[[o2,h2,p2,p1]]-ERI[[o1,o2,v1,v2]] t2[[o1,h1,v1,p2]] t2[[o2,h2,v2,p1]]}
```

### IP-EOM-CC with singles and doubles (IP-EOM-CCSD)


In this example, the IP-EOM-CCSD equations are generated thanks to the following input

Input:

```mathematica
ClusterOperator = {{"1h1p"}, {"2h2p"}};
EOMOperator = {{"1h0p"}, {"2h1p"}};
EOMCCgen[ClusterOperator, EOMOperator]
```
Output:

```mathematica

'Many-body terms'

\[Chi]1[[h3,h1]]==-F[[h3,h1]]-F[[h3,v1]] t1[[h1,v1]]+t1[[o1,v1]] ERI[[h3,o1,v1,h1]]+t1[[h1,v2]] t1[[o1,v1]] ERI[[h3,o1,v1,v2]]+1/2 ERI[[h3,o1,v1,v2]] t2[[o1,h1,v1,v2]]
\[Chi]1[[h4,p3]]==F[[h4,p3]]-t1[[o1,v1]] ERI[[h4,o1,v1,p3]]
\[Chi]2[[h4,h3,h1,p3]]==ERI[[h4,h3,h1,p3]]+t1[[h1,v1]] ERI[[h4,h3,v1,p3]]
\[Chi]2[[h3,p1,h1,h2]]==t1[[o1,p1]] ERI[[h3,o1,h1,h2]]-t1[[h2,v1]] t1[[o1,p1]] ERI[[h3,o1,v1,h1]]+t1[[h1,v1]] t1[[o1,p1]] ERI[[h3,o1,v1,h2]]+t1[[h1,v1]] t1[[h2,v2]] t1[[o1,p1]] ERI[[h3,o1,v1,v2]]-ERI[[h3,p1,h1,h2]]+t1[[h2,v1]] ERI[[h3,p1,v1,h1]]-t1[[h1,v1]] ERI[[h3,p1,v1,h2]]-t1[[h1,v1]] t1[[h2,v2]] ERI[[h3,p1,v1,v2]]-F[[h3,v1]] t2[[h1,h2,v1,p1]]+1/2 t1[[o1,p1]] ERI[[h3,o1,v1,v2]] t2[[h1,h2,v1,v2]]-1/2 ERI[[h3,p1,v1,v2]] t2[[h1,h2,v1,v2]]+t1[[o1,v1]] ERI[[h3,o1,v1,v2]] t2[[h1,h2,v2,p1]]-ERI[[h3,o1,v1,h2]] t2[[o1,h1,v1,p1]]+t1[[h2,v1]] ERI[[h3,o1,v1,v2]] t2[[o1,h1,v2,p1]]+ERI[[h3,o1,v1,h1]] t2[[o1,h2,v1,p1]]-t1[[h1,v1]] ERI[[h3,o1,v1,v2]] t2[[o1,h2,v2,p1]]
\[Chi]1[[p1,p3]]==F[[p1,p3]]-F[[o1,p3]] t1[[o1,p1]]-t1[[o1,v1]] t1[[o2,p1]] ERI[[o1,o2,v1,p3]]+t1[[o1,v1]] ERI[[o1,p1,v1,p3]]-1/2 ERI[[o1,o2,v1,p3]] t2[[o1,o2,v1,p1]]
\[Chi]2[[h4,h3,h1,h2]]==-ERI[[h4,h3,h1,h2]]+t1[[h2,v1]] ERI[[h4,h3,v1,h1]]-t1[[h1,v1]] ERI[[h4,h3,v1,h2]]-t1[[h1,v1]] t1[[h2,v2]] ERI[[h4,h3,v1,v2]]-1/2 ERI[[h4,h3,v1,v2]] t2[[h1,h2,v1,v2]]
\[Chi]2[[h4,p1,h2,p3]]==t1[[o1,p1]] ERI[[h4,o1,h2,p3]]+t1[[h2,v1]] t1[[o1,p1]] ERI[[h4,o1,v1,p3]]-ERI[[h4,p1,h2,p3]]-t1[[h2,v1]] ERI[[h4,p1,v1,p3]]-ERI[[h4,o1,v1,p3]] t2[[o1,h2,v1,p1]]
\[Chi]3[[h4,h3,p1,h1,h2,p3]]==ERI[[h4,h3,v1,p3]] t2[[h1,h2,v1,p1]]

'EOM-CC matrix in terms of many-body terms'

{{-\[Chi]1[[h3, h1]], -KroneckerDelta[h1, h4] \[Chi]1[[h3, p3]] + 
  KroneckerDelta[h1, h3] \[Chi][[h4, p3]] + \[Chi][[h4, h3, h1, p3]]},
 {-\[Chi]2[[h3, p1, h2, h1]], -KroneckerDelta[h2, h4] KroneckerDelta[p1, p3] \[Chi]1[[h3, h1]] + KroneckerDelta[h1, h4] KroneckerDelta[p1, p3] \[Chi]1[[h3, h2]] + KroneckerDelta[h2, h3] KroneckerDelta[p1, p3] \[Chi]2[[h4, h1]] - KroneckerDelta[h1, h3] KroneckerDelta[p1, p3] \[Chi]1[[h4, h2]] - KroneckerDelta[h1, h4] KroneckerDelta[h2, h3] \[Chi]1[[p1,  p3]] + KroneckerDelta[h1, h3] KroneckerDelta[h2, h4] \[Chi]1[[p1, p3]]
    - KroneckerDelta[h2, h4] \[Chi]2[[h3, p1, h1, p3]] + KroneckerDelta[h1, h4] \[Chi]2[[h3, p1, h2, p3]] + KroneckerDelta[p1, p3] \[Chi]2[[h4, h3, h2, h1]] +  KroneckerDelta[h2, h3] \[Chi]2[[h4, p1, h1, p3]] - KroneckerDelta[h1, h3] \[Chi]2[[h4, p1, h2, p3]] + \[Chi]3[[h4, h3,  p1, h2, h1, p3]]} }
```


### Single block of DEA-EOM-CCSD in terms of many-body terms.

It is possible to generate a single block as follows:

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

\[Chi]2[[h5,p1,h2,h3]]==t1[[o1,p1]] ERI[[h5,o1,h2,h3]]-t1[[h3,v1]] t1[[o1,p1]] ERI[[h5,o1,v1,h2]]+t1[[h2,v1]] t1[[o1,p1]] ERI[[h5,o1,v1,h3]]+t1[[h2,v1]] t1[[h3,v2]] t1[[o1,p1]] ERI[[h5,o1,v1,v2]]-ERI[[h5,p1,h2,h3]]+t1[[h3,v1]] ERI[[h5,p1,v1,h2]]-t1[[h2,v1]] ERI[[h5,p1,v1,h3]]-t1[[h2,v1]] t1[[h3,v2]] ERI[[h5,p1,v1,v2]]-F[[h5,v1]] t2[[h2,h3,v1,p1]]+1/2 t1[[o1,p1]] ERI[[h5,o1,v1,v2]] t2[[h2,h3,v1,v2]]-1/2 ERI[[h5,p1,v1,v2]] t2[[h2,h3,v1,v2]]+t1[[o1,v1]] ERI[[h5,o1,v1,v2]] t2[[h2,h3,v2,p1]]-ERI[[h5,o1,v1,h3]] t2[[o1,h2,v1,p1]]+t1[[h3,v1]] ERI[[h5,o1,v1,v2]] t2[[o1,h2,v2,p1]]+ERI[[h5,o1,v1,h2]] t2[[o1,h3,v1,p1]]-t1[[h2,v1]] ERI[[h5,o1,v1,v2]] t2[[o1,h3,v2,p1]]
\[Chi]3[[h5,h4,h3,p1,h1,h2]]==ERI[[h5,h4,v1,h3]] t2[[h1,h2,v1,p1]]-t1[[h3,v1]] ERI[[h5,h4,v1,v2]] t2[[h1,h2,v2,p1]]-ERI[[h5,h4,v1,h2]] t2[[h1,h3,v1,p1]]+t1[[h2,v1]] ERI[[h5,h4,v1,v2]] t2[[h1,h3,v2,p1]]+ERI[[h5,h4,v1,h1]] t2[[h2,h3,v1,p1]]-t1[[h1,v1]] ERI[[h5,h4,v1,v2]] t2[[h2,h3,v2,p1]]

'Block (2,1)'

KroneckerDelta[h3,h5]\[Chi]2[[h4,p1,h2,h1]]+KroneckerDelta[h2,h5]\[Chi]2[[h4,p1,h3,h1]]+KroneckerDelta[h1,h5]\[Chi]2[[h4,p1,h3,h2]]-KroneckerDelta[h3,h4]\[Chi]2[[h5,p1,h2,h1]]-
KroneckerDelta[h2,h4]\[Chi]2[[h5,p1,h3,h1]]-KroneckerDelta[h1,h4]\[Chi]2[[h5,p1,h3,h2]]-\[Chi]3[[h5,h4,p1,h3,h2,h1]]

```

### Single many-body term using a Hamiltonian.

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
\[Chi]2[[h3,p1,p4,p3]]==-t1[[o1,p1]] ERI[[h3,o1,p4,p3]]+ERI[[h3,p1,p4,p3]]
\[Chi]2[[p2,p1,h1,p3]]==t1[[o1,p2]] t1[[o2,p1]] ERI[[o1,o2,h1,p3]]+t1[[h1,v1]] t1[[o1,p2]] t1[[o2,p1]] ERI[[o1,o2,v1,p3]]-t1[[o1,p2]] ERI[[o1,p1,h1,p3]]-t1[[h1,v1]] t1[[o1,p2]] ERI[[o1,p1,v1,p3]]+t1[[o1,p1]] ERI[[o1,p2,h1,p3]]+t1[[h1,v1]] t1[[o1,p1]] ERI[[o1,p2,v1,p3]]+ERI[[p2,p1,h1,p3]]+t1[[h1,v1]] ERI[[p2,p1,v1,p3]]+F[[o1,p3]] t2[[o1,h1,p2,p1]]-ERI[[o1,p2,v1,p3]] t2[[o1,h1,v1,p1]]+ERI[[o1,p1,v1,p3]] t2[[o1,h1,v1,p2]]+1/2 ERI[[o1,o2,h1,p3]] t2[[o1,o2,p2,p1]]+1/2 t1[[h1,v1]] ERI[[o1,o2,v1,p3]] t2[[o1,o2,p2,p1]]+t1[[o1,v1]] ERI[[o1,o2,v1,p3]] t2[[o2,h1,p2,p1]]-t1[[o1,p2]] ERI[[o1,o2,v1,p3]] t2[[o2,h1,v1,p1]]+t1[[o1,p1]] ERI[[o1,o2,v1,p3]] t2[[o2,h1,v1,p2]]
```

## Conventions


### Index Convention

For the operators belonging to the bra and the ket, we use p1, p2, $\cdots$, h1, h2, $\cdots$. 
For the particles/holes that play the role of dummy indices in the cluster operator $\hat{T}$ we use o1, o2, $\cdots$, v1, v2, $\cdots$, where the notations o and v refer to occupied and virtual, respectively.
Finally, for the arbitrary indexes that can be either particle or hole, we use q1, q2, q3, $\cdots$.



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
# eomccnum 

**eomccnum** is a notebook designed to perform Coupled Cluster calculations for both ground state (CCS, CCD, CCSD, etc.) and excited states (EOM-CC) using [Wolfram Mathematica version 12.3](https://writings.stephenwolfram.com/2021/05/launching-version-12-3-of-wolfram-language-mathematica/). It is intended to be used alongside **eomccgen**, where you generate equations in **eomccgen** and then implement them in **eomccnum**. The features of this notebook are the following:


- Implements Coupled Cluster calculations for ground state and excited states.
- Provides three implemented examples: EE-EOM-CCSD, IP-EOM-CCSD, and DEA-EOM-CCSD.
- Requires electronic integrals to be included in the **int** file.  Integrals for H2O, Be, He, and Ne are provided.



## Example: EE-EOM-CCSD H2O in the Basis STO-3G
To calculate the excitation energies of water using the EE-EOM-CCSD method with the basis STO-3G, use the following input:

```Mathematica
eomccnum[10, 7, {{0., 0., -0.06990256}, {0., 0.75753241, 0.51843495}, {0., -0.75753241, 0.51843495}}, {8., 1., 1.}, "h2o.sto-3g", 1, 1.]
```


This input specifies:
- Number of electrons: 10
- Contracted Gaussian: 7
- Molecular coordinates: {{0., 0., -0.06990256}, {0., 0.75753241, 0.51843495}, {0., -0.75753241, 0.51843495}}
- Nuclear charges: {8., 1., 1.}
- File name: "h2o.sto-3g"
- Additional parameters: 1, 1

Ensure that you provide the correct values for each parameter.

For more information and additional examples, refer to the **eomccnum** user manual.


