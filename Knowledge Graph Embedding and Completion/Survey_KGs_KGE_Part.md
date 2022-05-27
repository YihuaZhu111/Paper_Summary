# Information

* A Survey on Knowledge Graphs: Representation, Acquisition, and Applications
* Shaoxiong Ji , Shirui Pan , *Member, IEEE*, Erik Cambria , *Fellow, IEEE*, Pekka Marttinen , and Philip S. Yu , Life Fellow, IEEE
* URL: https://ieeexplore.ieee.org/abstract/document/9416312
* Code: no code
* other: this summary is mainly on the part of KGE over the survey.



# Motivation

* Want to detect the new direction for Knowledge Graph, and the Knowledge Graph Embedding is a good direction, therefore, find this survey to learn and try to find some potential and interesting detailed directions.



# Overview

* The part of KGE(Knowledge Representation Learning) is in the left-top corner.
  * ![image-20220523224538668](https://tva1.sinaimg.cn/large/e6c9d24egy1h2ioabajkij21ak0u0ahp.jpg)



* this part can be divided into four sections:
  * **Representation Space**:
    * which space the relations and entities are represented.
    * The embedding space should follow three conditions, i.e., differentiability, calculation possibility, and definability of a scoring function <sup><a href="#ref1">1</a></sup>.
    * Real-valued pointwise space: vector, matrix, and tensor space
    * other space: complex vector space, Gaussian space, and manifold.
  * **Scoring Function**:
    * Measure the plausibility of factual triples
  * **Encoding Models**:
    * represent and learn relational interaction.
  * **Auxiliary Information**:
    * Incorporate other information to help KG Embedding 



# Main Content



## Representation Space

* **Pointwise Space** (Pointwise Euclidean Space)

  * TransE<sup><a href="#ref2">2</a></sup>: the relations and entities in d-dimension vector space: **h**+**r** ≈ **t**

    * <img src = "https://tva1.sinaimg.cn/large/e6c9d24egy1h2jqx9bw7xj20ei0ci0t1.jpg" width = "35%">

  * TransR<sup><a href="#ref3">3</a></sup>: divide the relation and entity space, and then project entity (**h**,**t** in R^k) into relation space by a projection matrix **M**.

  * NTN<sup><a href="#ref4">4</a></sup>:   (topic about KGC, important)

    * $$
      h^TMt, M \in \mathbb{R}^{d*d*k}
      $$

    * M is a tensor which indicates the relational interaction between head and tail.

  * HAKE<sup><a href="#ref5">5</a></sup>: map the relations and entities into polar coordinates to capture the semantic hierarchies

    *  concentric circles in the polar coordinate system can naturally reflect the hierarchy.

    * the radius coordinate aims to model entities at different levels of hierarchies.

    * the angular coordinate aims to distinguish entities at the same level of hierarchies.

    * $$
      e_m \in \mathbb{R}^d,    e_p \in [0,2\pi)^d
      $$
    
  * TransH<sup><a href="#ref17">17</a></sup>: models a relation as a hyperplane together with a translation operation on it.

    * TansE can not handle problems of reflexible, one-to-many, many-to-one, and many-to-many. TransH can do that.
    * TransH Utilizes the one-to-many/many-to-one mapping property of relation, they propose a simple trick to reduce the possibility of false-negative labeling to solve the incomplete KGs problem.
    * <img src = "https://tva1.sinaimg.cn/large/e6c9d24egy1h2lr8i1xcqj20uc0jgt9z.jpg" width="50%">

* **Complex Vector Space** 

  * $$
    h,t,r \in \mathbb{C}^d, h = Re(h)+i\cdot Im(h)
    $$

  * ComplEx<sup><a href="#ref6">6</a></sup>: can capture symmetric and antisymmetric relations, and use Hermitian dot product (dot product for complex).

  * RotatE<sup><a href="#ref7">7</a></sup>: use Euler's identity and elementwise Hadmard product

    * $$
      e^{i\theta}=\cos \theta+i\sin \theta, t=h \circ r
      $$

    * <img src = "https://tva1.sinaimg.cn/large/e6c9d24egy1h2jrdphp1hj20t00gmgmy.jpg" width = "60%">

    * capture the symmetric, antisymmetric, inversion, and composition.

    * defines each relation as a rotation from the head entity to the target entity in the complex vector space.

    * a novel self-adversarial negative sampling technique for efficiently and effectively training the RotatE model.

  * QuatE<sup><a href="#ref8">8</a></sup>: extend the complex-valued space into hypercomplex. 

    * use Quaternion:

      *  $$
        Q=a+bi+cj+dk
        $$

    * 

    * Hamilton product is used as a compositional operator for head entity and relation:

      * $$
        h \otimes r
        $$

    * <img src = "https://tva1.sinaimg.cn/large/e6c9d24egy1h2jsdp6im8j21es0i6go7.jpg" width = "80%">

    * advantages
      * Latent inter-dependencies (between all components) are aptly captured with Hamilton product.
      * Quaternions enable expressive rotation in four-dimensional space and have more degree of freedom than rotation in complex plane
      * The proposed framework is a generalization of ComplEx on hypercomplex space while offering better geometrical interpretations, concurrently satisfying the key desiderata of relational representation learning (i.e., modeling symmetry, anti-symmetry and inversion)

* **Gaussian Distribution**

  * KG2E<sup><a href="#ref9">9</a></sup>: introduces Gaussian distribution to deal with the (un)certainties of entities and relations.

    * embed entity(**H**) and relation(**T**) into multidimensional Gaussian distribution :

      * u means the position of entity and relation position in the complex space, E means their uncertainty.

      * $$
        H \sim N（u_h, \boldsymbol{\Sigma}_h）, T \sim N（u_t, \boldsymbol{\Sigma}_t）
        $$

    * the probability distribution of entity transformation H - T is donated as:

      * $$
        P_e \sim N(u_h-u_t, \boldsymbol{\Sigma}_h+\boldsymbol{\Sigma}_t）
        $$

    * popular entities with fewer uncertainty, which contain more relations and facts than unpopular ones, high-frequency rela- tions with more uncertainty, which link more entity pairs than low frequency ones

  * TransG<sup><a href="#ref10">10</a></sup>: similar to KG2E, but this paper represents entities with Gaussian distributions, while it draws a mixture of Gaussian distribution for relation embedding, where the *m*th component translation vector of relation *r* is denoted as:

    * $$
      \mathbf u_{r,m}=t-h \sim \mathbf N(u_t - u_h,(\sigma ^2_h+\sigma^2_t)\mathbf E)
      $$

    * TransG can discover the latent semantics of a relation automatically and leverage a mixture of relation components for embedding.

* **Manifold and Group**（KGE in manifold space, lie group, dihedral group）

  * basic definition:
  
    * Manifiold: A manifold is a topological space, which could be defined as a set of points with neighborhoods by the set theory
    * Group: The group is algebraic structures defined in abstract algebra.
  
  * ManifoldE<sup><a href="#ref11">11</a></sup>:  for the link prediction.
  
    * the pointwise modeling has two problem:
      * the number of scoring equations is far more than the number of entities and relations, resulting in the problem of **ill-posed algebraic system**.
      * embeddings are restricted in an **overstrict geometric** form even in some methods with subspace projection.
    * this paper proposes two settings of manifold-based embedding:
      * Sphere: reproducing the Kernel Hilbert space.
      * Hyperplane: enhance the model with intersected embedding.
      * <img src = "https://tva1.sinaimg.cn/large/e6c9d24egy1h2kvg9uvr9j20y50u0n3g.jpg" width = "60%">
  
  * MuRP<sup><a href="#ref12">12</a></sup>: epresents the multirelational knowledge graph in the Poincaré ball of hyperbolic space.
  
  * ATTH<sup><a href="#ref13">13</a></sup>: utilize a class of hyperbolic KG embedding models that capture hierarchical and logical patterns. 
  
  * TorusE<sup><a href="#ref14">14</a></sup>: TransE has the regularization problem, TorusE try to use torus (Lie group) to solve it.
  
  * * project from vector space into torus space.
  
    * $$
      [h]+[r] \approx [t]
      $$
  
    * <img src = "https://tva1.sinaimg.cn/large/e6c9d24egy1h2kypea7dxj20vk0ogdld.jpg" width="50%">
  
  * DihEdral<sup><a href="#ref15">15</a></sup>: a dihedral symmetry group preserving a 2-D polygon.



## Scoring Function

* **Basic information**

  * The scoring function is used to measure the plausibility of facts.

  * Two types:

    * Distance-based function (Euclidean distance):

      * $$
        h+r \approx t
        $$

    * Similarity-based function:

      * $$
        \mathbf h^\top \mathbf M_r \approx \mathbf t^\top
        $$

    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2kzmeukmkj20wy0hyac7.jpg" width="60%">

* **Distance-Based Scoring Function**:

  * TransE:

    * $$
      f_r(h,t)= \lVert h+r-t \rVert_{L_1 \diagup L_2}
      $$

  * TransF:

    * $$
      f_r(h,t)=(\mathbf h+ \mathbf r)^\top \mathbf t
      $$

  * ITransF<sup><a href="#ref15">15</a></sup>: enables **hidden concepts discovery** and **statistical strength transferring** by learning associations between relations and concepts via **sparse attention vectors**:

    * $$
      f_r(h,t)=\lVert \alpha_r^H \cdot \mathbf D \cdot \mathbf h +\mathbf r -\alpha_r^T \cdot \mathbf D \cdot \mathbf t \rVert_l
      $$

    * 
      $$
      \mathbf D \in \mathbb R^{n*d*d}.\alpha_r^H,\alpha_r^T \in [0,1]^n
      $$

    * **D** is stacked concept projection matrices of entities and relations, **alpha** is attention vectors calculated by sparse softmax.

  * TransMS: trans- lates and transmits multidirectional semantics.

    * he semantics of head/tail entities and relations to tail/head entities with **nonlinear functions**
    * the semantics from entities to relations with **linear bias vectors**
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2l1acuvrpj20ts03uq34.jpg" width="60%">

  * KG2E: (Gaussian Space) use 1, asymmetric KL-divergence. 2, symmetric expected likelihood.

  * ManifoldE:

    * <img src = "https://tva1.sinaimg.cn/large/e6c9d24egy1h2l1eetymkj20wm05mgm9.jpg" width="65%">



* **Semantic Matching** (Similarity-based sccoring function)
  * SME<sup><a href="#ref16">16</a></sup>: match separate combinations of entity-relation pairs (h, r) and (r, t).
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2lo8tihgcj21py0tcwjr.jpg" width="70%">
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2loa0c9bpj20h4020q2w.jpg" width="40%">
  * CrossE<sup><a href="#ref18">18</a></sup>: It not only learns one general embedding for each entity and relation as in most previous methods, but also generates multiple triple specific embeddings for both of them, named interaction embeddings.
    * use interaction matrix **C** to simulate the bidirectional interaction between entity and relation.
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2lulfdoikj20ww098acn.jpg" width="70%">
  * TorusE<sup><a href="#ref14">14</a></sup> and DihEdral<sup><a href="#ref15">15</a></sup> also use sementic matching:
    * for DihEdral：
      * <img src = "https://tva1.sinaimg.cn/large/e6c9d24egy1h2lup88s11j20we09qwfr.jpg" width="60%">



## **Encoding Models**

* **Basic information**: encode the interactions of entities and relations by using model architecture.

  * Linear/Bilinear models: regard relations as a linear/bilinear mapping by projecting head entities into a space close to tail entities.
  * Factorization: decompose relation into a low-rank matrices for representation learning.
  * Neural networks: encode relational with nonlinear neural activation and complex network to represent complex sementic similarity of entities and relations.

* **Linear/Bilinear Models**

  * Definition:
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2lze9a4e5j213w0ea40a.jpg" width="70%">

  * traditional linear/bilinear model like SE, SME, DistMult, ComplEx, and ANALOGY, use:
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2lyv7xqvvj20as0400sn.jpg" width="20%">
    * Bilinear: RESCAL, DistMult, HolE, ComplEx.
  * TransE<sup><a href="#ref2">2</a></sup> use L2 regularization:
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2lyxtcik7j20se02cq30.jpg" width="55%">
  * SimplE<sup><a href="#ref19">19</a></sup>:  
  * * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m00vzwjcj20fu0320so.jpg" width="32%">
    * r' is the embedding of inversion relation.

* **Factorization Models**

  * Definition:

    * tensor factorization can be denoted as:

    * $$
      \chi_{hrt} \approx \mathbf h^\top \mathbf M_r \mathbf t
      $$

  * RESCAL<sup><a href="#ref20">20</a></sup>: 

    * for the *k*th relation of m relations, the *k*th slice of **X** is factorized as:
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m1sct0wej207u01ut8j.jpg" width="17%">

* **Neural Networks**

  * Basic:

    * Linear/bilinear model can be modeled by NN.
    * feed the entities and rellations into NN and get score output.

  * **CNN**

    * ConvE<sup><a href="#ref21">21</a></sup>: use 2D convelution over embedding.

      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m39yw633j20l201o3yj.jpg" width="45%">
      * ; means concatenate, * means conv operation, w means conv filter, Vec means reshape a tensor into a vector.
      * ![image-20220526215440837](https://tva1.sinaimg.cn/large/e6c9d24egy1h2m3o7iqtij21sa0jq0vs.jpg)

    * ConvKB<sup><a href="#ref22">22</a></sup>:

      * <img src = "https://tva1.sinaimg.cn/large/e6c9d24egy1h2m3q35j1zj20ju01wglm.jpg" width="45%">

      * ​                                                         <img src ="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m36h4q2kj20920acjrm.jpg" width="25%">
      * compared with ConvE, ConvKB can capture local relationships.

  * **RNN**

    * RSN<sup><a href="#ref23">23</a></sup>: 
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m4cy21lnj20hu09iq3m.jpg" width="40%">
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m4f5l546j20tw0igjuv.jpg" width="50%">

  * **Transformer**

    * In order to add contextual information into KG, CoKE<sup><a href="#ref24">24</a></sup> employs transformers to encode edges and path sequences:
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m5fvlmuxj21mc0u0ah0.jpg" width="80%">
    * KG-BERT<sup><a href="#ref25">25</a></sup> use BERT to encode entities and relations:
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m5kgzo0ej21ch0u0n3a.jpg" width="60%">

  * **GNN**

    * use R-GCN<sup><a href="#ref26">26</a></sup> to do the Link prediction (recovery of missing facts, i.e. subject-predicate-object triples) and en- tity classification (recovery of missing entity attributes):
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m6bx1i5xj20qg05q3ys.jpg" width="45%">
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m6e4gq1mj214m0u0jxe.jpg" width= "50%">
    * SACN<sup><a href="#ref27">27</a></sup> use weight GCN(WGCN) as encoder, use Conv-TransE as decoder to combine the advantages of GCN and ConvE.
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2m6tu7oibj21o20u0tgc.jpg" width ="100%">
    * CompGCN



## **Embedding With Auxiliary Information**

* **Textual Description**
  * DKRL<sup><a href="#ref28">28</a></sup>:
    * use Convelutional encoder.
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2mt7myt4tj21h80paq7n.jpg" width="80%">
  * SSP<sup><a href="#ref29">29</a></sup>:
    * project triples and textual information into semantic space:
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2mtbnhalgj20uy0lkjuc.jpg" width="50%">
* **Type Information**
  * entities are represented with heirarchical classes or types, and relations with sementic types.
* **Visual Information**
  * utilize visual information to embed entities.
* **Uncertain Information**
  * uncertain embedding models aim to capture uncertainty rep- resenting the likelihood of relational facts.



## **Summary**

* Which representation space to choose.
* how to measure the plausibility of triples in a specific space.
* which encoding model to use for modeling relational interactions.
* whether to ultilize auxiliary information.



## Review

* for the representation space part, we can use several space like normal Euclidean space, complex space, manifold, etc. Each kind of space has its own benefits.
* For the scoring part, we need to use semantic matching now.
* but for the encoding models, we need to use NN models, but not the traditional linear models. LMs and transformers need to be utilized well in the KGE.
* if we can, we need to use extention auxiliary information to enhance the KGE, especially for large textual information.
* In conclusion, I need to find some paper about KGE recently, grasp the detail about the KGE，and undderstand the benchmark and how to evaluate the KGE from the experiments.
* a good KGE, and a suitbale representation space, encoding model can help us to do NLP task which need to use KG and Graph Structure.
* ![image](https://tva1.sinaimg.cn/large/e6c9d24egy1h2natr6sx1j20u00vjq9h.jpg)



# Reference

1. <span name = "ref1"> T. Ebisu and R. Ichise, “TorusE: Knowledge graph embedding on a lie group,” in Proc. AAAI, 2018, pp. 1819–1826.</span>  
2. <span name = "ref2">A. Bordes, N. Usunier, A. Garcia-Duran, J. Weston, and O. Yakhnenko, “Translating embeddings for modeling multi-relational data,” in Proc. NIPS, 2013, pp. 2787–2795.</span>  
3. <span name = "ref3">Y. Lin, Z. Liu, M. Sun, Y. Liu, and X. Zhu, “Learning entity and relation embeddings for knowledge graph completion,” in Proc. AAAI, 2015, pp. 2181–2187.</span>  
4. <span name = "ref4">R. Socher, D. Chen, C. D. Manning, and A. Ng, “Reasoning with neural tensor networks for knowledge base completion,” in Proc. NIPS, 2013, pp. 926–934.</span>  
5. <span name = "ref5">Z. Zhang, J. Cai, Y. Zhang, and J. Wang, “Learning hierarchy-aware knowledge graph embeddings for link prediction,” in Proc. AAAI, 2020, pp. 3065–3072.</span>  
6. <span name = "ref6">T. Trouillon, J. Welbl, S. Riedel, E. Gaussier, and G. Bouchard, “Complex embeddings for simple link prediction,” in Proc. ICML, 2016, pp. 2071–2080.</span>  
7. <span name = "ref7">Z. Sun, Z.-H. Deng, J.-Y. Nie, and J. Tang, “RotatE: Knowledge graph embedding by relational rotation in complex space,” in Proc. ICLR, 2019, pp. 1–18.</span>  
8. <span name = "ref8">S. Zhang, Y. Tay, L. Yao, and Q. Liu, “Quaternion knowledge graph embedding,” in Proc. NeurIPS, 2019, pp. 2731–2741.</span> 
9. <span name = "ref9">S. He, K. Liu, G. Ji, and J. Zhao, “Learning to represent knowledge graphs with Gaussian embedding,” in Proc. 24th ACM Int. Conf. Inf. Knowl. Manage., Oct. 2015, pp. 623–632.</span> 
10. <span name = "ref10">H. Xiao, M. Huang, and X. Zhu, “TransG: A generative model for knowledge graph embedding,” in Proc. ACL, vol. 1, 2016, pp. 2316–2325.</span> 
11. <span name = "ref11">H. Xiao, M. Huang, Y. Hao, and X. Zhu, “From one point to a manifold: Orbit models for knowledge graph embedding,” in Proc. IJCAI, 2016, pp. 1315–1321.</span> 
12. <span name = "ref12">I. Balazevic, C. Allen, and T. Hospedales, “Multi-relational poincaré graph embeddings,” in NeurIPS, 2019, pp. 4463–4473.</span> 
13. <span name = "ref13">I. Chami, A. Wolf, D.-C. Juan, F. Sala, S. Ravi, and C. Ré, “Lowdimensional hyperbolic knowledge graph embeddings,” in Proc. 58th Annu. Meeting Assoc. Comput. Linguistics, 2020, pp. 6901–6914.</span> 
14. <span name = "ref14">T. Ebisu and R. Ichise, “TorusE: Knowledge graph embedding on a lie group,” in Proc. AAAI, 2018, pp. 1819–1826.</span> 
15. <span name = "ref15">Q. Xie, X. Ma, Z. Dai, and E. Hovy, “An interpretable knowledge transfer model for knowledge base completion,” in Proc. 55th Annu. Meeting Assoc. Comput. Linguistics, vol. 1, 2017, pp. 950–962.</span> 
16. <span name = "ref16">A. Bordes, X. Glorot, J. Weston, and Y. Bengio, “A semantic matching energy function for learning with multi-relational data,” Mach. Learn., vol. 94, no. 2, pp. 233–259, Feb. 2014.</span> 
17. <span name = "ref17">Z. Zhang, J. Cai, Y. Zhang, and J. Wang, “Learning hierarchy-aware knowledge graph embeddings for link prediction,” in Proc. AAAI, 2020, pp. 3065–3072.</span> 
18. <span name = "ref18">W. Zhang, B. Paudel, W. Zhang, A. Bernstein, and H. Chen, “Interaction embeddings for prediction and explanation in knowledge graphs,” in Proc. 12th ACM Int. Conf. Web Search Data Mining, Jan. 2019, pp. 96–104.</span> 
19. <span name = "ref19">S. M. Kazemi and D. Poole, “SimplE embedding for link prediction in knowledge graphs,” in Proc. NeurIPS, 2018, pp. 4284–4295.</span> 
20. <span name = "ref20">M. Nickel, V. Tresp, and H.-P. Kriegel, “A three-way model for collective learning on multi-relational data,” in Proc. ICML, vol. 11, 2011, pp. 809–816.</span> 
21. <span name = "ref21">T. Dettmers, P. Minervini, P. Stenetorp, and S. Riedel, “Convolutional 2D knowledge graph embeddings,” in Proc. AAAI, vol. 32, 2018, pp. 1811–1818.</span> 
22. <span name = "ref22">D. Q. Nguyen, T. D. Nguyen, D. Q. Nguyen, and D. Phung, “A novel embedding model for knowledge base completion based on convolutional neural network,” in Proc. Conf. North Amer. Chapter Assoc. Comput. Linguistics: Human Lang. Technol., vol. 2, 2018,</span> 
23. <span name = "ref23">L. Guo, Z. Sun, and W. Hu, “Learning to exploit long-term relational dependencies in knowledge graphs,” in Proc. ICML, 2019, pp. 2505–2514.</span> 
24. <span name = "ref24">Q. Wang et al., “CoKE: Contextualized knowledge graph embedding,” 2019, arXiv:1911.02168. [Online]. Available: http://arxiv.org/abs/1911.02168</span>. 
25. <span name = "ref25">L. Yao, C. Mao, and Y. Luo, “KG-BERT: BERT for knowledge graph completion,” 2019, arXiv:1909.03193. [Online]. Available: http://arxiv.org/abs/1909.03193</span> 
26. <span name = "ref26">M. Schlichtkrull, T. N. Kipf, P. Bloem, R. Van Den Berg, I. Titov, and M. Welling, “Modeling relational data with graph convolutional networks,” in Proc. ESWC, 2018, pp. 593–607.</span> 
27. <span name = "ref27">C. Shang, Y. Tang, J. Huang, J. Bi, X. He, and B. Zhou, “Endto-end structure-aware convolutional networks for knowledge base completion,” in Proc. AAAI, vol. 33, 2019, pp. 3060–3067.</span> 
28. <span name = "ref28">R. Xie, Z. Liu, J. Jia, H. Luan, and M. Sun, “Representation learning of knowledge graphs with entity descriptions,” in Proc. AAAI, 2016, pp. 2659–2665.</span> 
29. <span name = "ref29">H. Xiao, M. Huang, L. Meng, and X. Zhu, “SSP: Semantic space projection for knowledge graph embedding with text descriptions,” in Proc. AAAI, 2017, pp. 3104–3110.</span>
