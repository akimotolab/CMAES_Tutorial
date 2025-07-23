# CMAES_Tutorial

CMA-ESの学習用コンテンツ．
利用者は多くいるにも関わらず，日本語での適切な説明資料および学習コンテンツが知る限り存在しないので，昔教育用に作成したノートブックをもとに作成．
時間的余裕があるときに少しずつ更新していきます．
1_から順に学ぶことを想定しています．

## CMA-ESを理解するために最低限読んでおいたほうが良い論文
いずれも機関レポジトリやアーカイブなどでPDFを確認できます．
- Nikolaus Hansen, Andreas Ostermeier; Completely Derandomized Self-Adaptation in Evolution Strategies. Evol Comput 2001; 9 (2): 159–195. doi: https://doi.org/10.1162/106365601750190398
  - CMA-ESの原型．CSAによるステップサイズ更新とRank-one更新による共分散行列更新を用いたアルゴリズム
- Nikolaus Hansen, Sibylle D. Müller, Petros Koumoutsakos; Reducing the Time Complexity of the Derandomized Evolution Strategy with Covariance Matrix Adaptation (CMA-ES). Evol Comput 2003; 11 (1): 1–18. doi: https://doi.org/10.1162/106365603321828970
  - Rank-mu更新の導入．これにより，大きな集団サイズを効率的に活用できるようになった．
- Hansen, N., Kern, S. (2004). Evaluating the CMA Evolution Strategy on Multimodal Test Functions. In: Yao, X., et al. Parallel Problem Solving from Nature - PPSN VIII. PPSN 2004. Lecture Notes in Computer Science, vol 3242. Springer, Berlin, Heidelberg. https://doi.org/10.1007/978-3-540-30217-9_29
  - 多峰性関数での性能評価．集団サイズを大きくすることで最適解発見確率が高くなること，一部の問題では集団サイズの増加が効果的でないこと，を示した結果．なお，weighted-recombination（ランキング毎に異なる重みを与えるスキーム）もここで導入されているが，多峰性とは特に関係はなく，均等な重みよりも少しだけ効率的なのでその後はずっと使われている．
- G. A. Jastrebski and D. V. Arnold, "Improving Evolution Strategies through Active Covariance Matrix Adaptation," 2006 IEEE International Conference on Evolutionary Computation, Vancouver, BC, Canada, 2006, pp. 2814-2821, doi: https://doi.org/10.1109/CEC.2006.1688662.
  - 共分散行列の適応の際に負の重みを活用するActive更新の提案．これまでのCMA-ESでは相対的に大きな固有値を学習することが得意であったが，このActive更新によって相対的に小さな固有値の学習を効率化できる．共分散行列の正定値性の保証がなくなるが，十分に小さい学習率を用いている限りは実用上問題ない．
- Ros, R., Hansen, N. (2008). A Simple Modification in CMA-ES Achieving Linear Time and Space Complexity. In: Rudolph, G., Jansen, T., Beume, N., Lucas, S., Poloni, C. (eds) Parallel Problem Solving from Nature – PPSN X. PPSN 2008. Lecture Notes in Computer Science, vol 5199. Springer, Berlin, Heidelberg. https://doi.org/10.1007/978-3-540-87700-4_30
  - 共分散行列を対角行列に限定することで変数の数に対して線形の計算量を実現するSep-CMA-ESの提案．高次元最適化のための方法としても有用だが，それ以上に，1)共分散行列を制限すると一部の目的関数においてヘッセ行列の逆行列を近似できないため探索が非効率になるという点，2)逆に，一部の問題ではSeparability（変数毎にスケールが異なるにしても，変数間に依存関係がない構造）を活用することになり，共分散行列の学習が高速化され（学習率を高く設定できるため），学習時間が短縮される（収束の速さ自体はかわらない）という点を理解することが重要
- Y. Akimoto, N. Hansen; Diagonal Acceleration for Covariance Matrix Adaptation Evolution Strategies. Evol Comput 2020; 28 (3): 405–435. doi: https://doi.org/10.1162/evco_a_00260
  - Sep-CMA-ESと従来のCMA-ESのいいとこ取りをするdiagonal decodingの提案．Active更新における共分散行列の正定値性を保証する枠組みも提案．
