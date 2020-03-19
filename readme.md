# asap

ASAP: Code for active sampling in pairwise comparison experiments.

If using the code please cite:

[1]  A. Mikhailiuk, C. Wilmot M. Perez-Ortiz, D. Yue and R. K. Mantiuk, “”, arxive, 2019. Accessible at 

The active sampling package includes:

* two versions of the algorithm: (i) ASAP - an accurate version with full posterior update; (ii) ASAP-approx. - version with an online posterior update for reduced computation cost;
* ASAP and ASAP-approx. both in python and matlab;
* ASAP and ASAP-approx. with support for batch and sequential modes
* Pytorch-GPU implementation of ASAP for large scale experiments;
* matlab implementation of 9 commonly used sampling strategies.

** Usage

ASAP and ASAP-approx return either a pair or a batch of pairs with the highest expected information gain. By default batch mode is used.

Both python and matlab code use run_asap(M) function to produce pairs to be compared. Where M is a pairwise comparison matrix (NxN), with each element M[ii][jj] - the number of times condition ii was selected over condition jj in comparisons performed so far.

run_asap(M) function returns an either a ((N-1)x2) array of indeces ii jj of elements to be compared, or a single pair maximising information gain. Note that the output might be different from the one given below due to the use of selective expected information gain evaluation.

Python:

```
# import asap from the file
import asap_cpu
import numpy as np

# Matrix with pairwise comparisons
M = np.array([[0,1,2,3,1],
              [1,0,2,3,1],
              [1,2,0,3,1],
              [1,2,3,0,1],
              [1,2,3,1,0]])
              
N = np.shape(M)[0]

# Create an object of class passing the number of conditions
asap = asap_cpu.ASAP(N)

# Run active sampling algorithm on the matrix of comaprisons
pairs_to_compare = asap.run_asap(M)

# Calling print
print(pairs_to_compare)

Output: 

[[0 4]
 [2 4]
 [0 1]
 [0 3]]

```

Matlab:


```
% Create matrix with pairwise comparisons
M = [0,1,2,3,1;
     1,0,2,3,1;
     1,2,0,3,1;
     1,2,3,0,1;
     1,2,3,1,0];
              
% Run active sampling
pairs_to_compare = run_asap(M, 'mst');

% Calling print
display(pairs_to_compare)

Output: 

pairs_to_compare =

     1     5
     1     2
     1     3
     1     4

```


## Literature

We also include the code for the compared in the paper methods. If using any, please also cite the original paper:

Swiss-system:


Quicksort:
L.  Maystre  and  M.  Grossglauser,  “Just  sort  it!  A  simple  and  effective approach  to  active  preference  learning,”  in Proceedings  of  the 34th International Conference on Machine Learning, vol. 70.   PMLR, 06–11Aug 2017, pp. 2344–2353.

Adaptive-rectangular-design (ARD):
ITU-R,  “Subjective  assessment  methods  for  3D  video  quality,”  ITU-R Recommendation P.915, Mar 2016.

Matchmaking:
R.  Herbrich,  T.  Minka,  and  T.  Graepel,  “Trueskill TM:  A  bayesian  skill rating system,” in Advances in Neural Information Processing Systems 19

HRactive:
Q.  Xu,  J.  Xiong,  X.  Chen,  Q.  Huang,  and  Y.  Yao,  “Hodgerank  with information  maximization  for  crowdsourced  pairwise  ranking  aggregation, ”Proceedings  of  the  Thirty-Second  AAAI  Conference  on  Artificial Intelligence, (AAAI-18), pp. 4326–4334, 2018. 

AKG:
X.  Chen,  K.  Jiao,  and  Q.  Lin,  “Bayesian  decision  process  for  cost-efficient  dynamic  ranking  via  crowdsourcing,”Journal  of  MachineLearning Research, vol. 17, no. 216, pp. 1–40, 2016.

Crowd-BT:
X. Chen, P. N. Bennett, K. Collins-Thompson, and E. Horvitz, “Pairwise ranking aggregation in a crowdsourced setting,” Proceedings of the Sixth ACM  International  Conference  on  Web  Search  and  Data  Mining,  pp.193–202, 2013

Hybrid-MST:
J.  Li,  R.  Mantiuk,  J.  Wang,  S.  Ling,  and  P.  Le  Callet,  “Hybrid-mst: A hybrid active sampling strategy for pairwise preference aggregation,” NIPS, 31st Conference on Neural Information Processing Systems, 2018.

YeDoermann (computationally very slow, included for completeness):

P. Ye and D. Doermann, “Active sampling for subjective image quality assessment,” in 2014 IEEE Conference on Computer Vision and Pattern Recognition, June 2014, pp. 4249–4256.

API (Numerically unstable, included for completeness):
T. Pfeiffer, X. Gao, Y. Chen, A. Mao, and D. Rand, “Adaptive polling for information aggregation,” AAAI Conference on Artificial Intelligence, 2012.


## License

MIT