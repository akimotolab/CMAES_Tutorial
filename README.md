# CMAES Tutorial

CMA-ESの学習用コンテンツ．
Learning materials for CMA-ES. 


## CMA-ESを理解するために最低限読んでおいたほうが良い論文</br> List of papers you should read to understand CMA-ES

- Nikolaus Hansen, Andreas Ostermeier; Completely Derandomized Self-Adaptation in Evolution Strategies. Evol Comput 2001; 9 (2): 159–195. doi: https://doi.org/10.1162/106365601750190398
  - CMA-ESの原型．CSAによるステップサイズ更新とRank-one更新による共分散行列更新を用いたアルゴリズム</br>
  The original CMA-ES: An algorithm employing step-size adaptation (CSA) and the rank-one covariance matrix adaptation.

- Nikolaus Hansen, Sibylle D. Müller, Petros Koumoutsakos; Reducing the Time Complexity of the Derandomized Evolution Strategy with Covariance Matrix Adaptation (CMA-ES). Evol Comput 2003; 11 (1): 1–18. doi: https://doi.org/10.1162/106365603321828970
  - Rank-mu更新の導入．これにより，大きな集団サイズを効率的に活用できるようになった．</br>
  Introduction of the rank-mu update. It allows for exploiting a large population efficiently.

- Hansen, N., Kern, S. (2004). Evaluating the CMA Evolution Strategy on Multimodal Test Functions. In: Yao, X., et al. Parallel Problem Solving from Nature - PPSN VIII. PPSN 2004. Lecture Notes in Computer Science, vol 3242. Springer, Berlin, Heidelberg. https://doi.org/10.1007/978-3-540-30217-9_29
  - 多峰性関数での性能評価．集団サイズを大きくすることで最適解発見確率が高くなること，一部の問題では集団サイズの増加が効果的でないこと，を示した結果．なお，weighted-recombination（ランキング毎に異なる重みを与えるスキーム）もここで導入されているが，多峰性とは特に関係はなく，均等な重みよりも少しだけ効率的なのでその後はずっと使われている．</br>
  Evaluation of the performance on multimodal functions. It shows that the success rate is improved by a larger population on many (well-structured) multimodal functions, and a large population size is not effective on some (weakly-structured or deceptive) multimodal functions. The weighted recombination has been introduced in this paper, irrespective of multimodality. The weighted recombination is slightly more efficient than the truncation, hence it is used as the default weighting scheme.

- G. A. Jastrebski and D. V. Arnold, "Improving Evolution Strategies through Active Covariance Matrix Adaptation," 2006 IEEE International Conference on Evolutionary Computation, Vancouver, BC, Canada, 2006, pp. 2814-2821, doi: https://doi.org/10.1109/CEC.2006.1688662.
  - 共分散行列の適応の際に負の重みを活用するActive更新の提案．これまでのCMA-ESでは相対的に大きな固有値を学習することが得意であったが，このActive更新によって相対的に小さな固有値の学習を効率化できる．共分散行列の正定値性の保証がなくなるが，十分に小さい学習率を用いている限りは実用上問題ない．</br>
  Active update, which uses negative weights for (rank-mu) covariance matrix update, is introduced. The rank-one and rank-mu update is good at learning relatively large eigenvalues. The active update, on the other hand, excels at learning relatively small eigenvalues. The positive definiteness is not guaranteed by the update and the parameter setting in this paper, but the positivity tends to be satisfied as long as a sufficiently small learning rate is used.

- Ros, R., Hansen, N. (2008). A Simple Modification in CMA-ES Achieving Linear Time and Space Complexity. In: Rudolph, G., Jansen, T., Beume, N., Lucas, S., Poloni, C. (eds) Parallel Problem Solving from Nature – PPSN X. PPSN 2008. Lecture Notes in Computer Science, vol 5199. Springer, Berlin, Heidelberg. https://doi.org/10.1007/978-3-540-87700-4_30
  - 共分散行列を対角行列に限定することで変数の数に対して線形の計算量を実現するSep-CMA-ESの提案．高次元最適化のための方法としても有用だが，それ以上に，1)共分散行列を制限すると一部の目的関数においてヘッセ行列の逆行列を近似できないため探索が非効率になるという点，2)逆に，一部の問題ではSeparability（変数毎にスケールが異なるにしても，変数間に依存関係がない構造）を活用することになり，共分散行列の学習が高速化され（学習率を高く設定できるため），学習時間が短縮される（収束の速さ自体はかわらない）という点を理解することが重要</br>
  Sep-CMA-ES: A variant of CMA-ES with linear time and space internal complexity. It restricts the covariance matrix to be diagonal. Importantly, with diagonal covariance matrices, 1) the inverse of the Hessian matrix of a non-separable problem can not be well approximated, leading to slow convergence, but 2) we can increase the learning rate of the covariance matrix adaptation (as the degree of freedom is smaller), reducing the adaptation time on separable problems (convergence rate is unchanged).

- Y. Akimoto, N. Hansen; Diagonal Acceleration for Covariance Matrix Adaptation Evolution Strategies. Evol Comput 2020; 28 (3): 405–435. doi: https://doi.org/10.1162/evco_a_00260
  - Sep-CMA-ESと従来のCMA-ESのいいとこ取りをするdiagonal decodingの提案．Active更新における共分散行列の正定値性を保証する枠組みも提案．</br>
 DD-CMA-ES takes the advantages of both Sep-CMA-ES and CMA-ES by diagonal decoding. It also proposes a mechanism to guarantee the positive definiteness of the covariance matrix under active update.
