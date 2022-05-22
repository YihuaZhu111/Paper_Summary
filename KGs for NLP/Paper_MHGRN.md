# Information

* **Scalable Multi-Hop Relational Reasoning for Knowledge-Aware Question Answering**
* Yanlin Feng Xinyue Chen Bill Yuchen Lin Peifeng Wang Jun Yan Xiang Ren
* Url: https://arxiv.org/abs/2005.00646
* Code: https://github.com/INK-USC/MHGRN
* Other: EMNLP2020



# Motivation

* Domain: **graph structure, Knowledge base, Multi-hop QA**
* QA-GNN extended the research based on MHGRN, and MHGRN can be the first few paper which opened the KB-QA domain.
* new method which used path-based 



# Background

* QA task requires not only machine comprehension of question and context, but also relational reasoning over entities (concepts) and their relationships by referencing external knowledge
* Large-scale pre-trained language models are useful, but they cannot provide interpretable predictions. 
* Incorporating KGs brings the potential of interpretable and trustworthy predictions, as the knowledge is now explicitly stated.
* These models(Magnet, MHPG, directly model relation paths, attention mechanisms upon these relations can provide interpretability). However, these models cannot scalable, reasons:
  * 1, polynomial (large scale of the number of nodes)
  * 2, exponential (path length)
* GNN can be scalable, but it lacks transparency (GCN, RGCNs).
* MHGRN can combine the strengths of path-based models(interpretable, but not scalable) and GNNs(scalable but not transparency or interpretable).



# Approach

* ![szIIUYZA](https://tva1.sinaimg.cn/large/e6c9d24egy1h2h4dhns7zj218g0p20wt.jpg)



# Experiment

* **Dataset:**
  * CommensenseQA, OpenBookQA.
  * Conceptnet (https://conceptnet.io)
* **Results:**
  * Performance comparison on CommonsenseQA in-house split:
    * ![image-20220522150519693](https://tva1.sinaimg.cn/large/e6c9d24egy1h2h5d31wetj22gd0u0wq3.jpg)
  * Performance comparison on official test of CommonsenseQA:
    * ![image-20220522150616097](https://tva1.sinaimg.cn/large/e6c9d24egy1h2h5dz80g9j20wh0u0q7s.jpg)
  * OpenBookQA:
    * ![image-20220522150721734](https://tva1.sinaimg.cn/large/e6c9d24egy1h2h5f5fqvlj212k0u0jwq.jpg)
  * Case study:
    * ![image-20220522151024797](https://tva1.sinaimg.cn/large/e6c9d24egy1h2h5rnf55bj21gy0t6n3n.jpg)



# Review

* For the experiment of interpretable, only use a **case study** and two real examples to show that is not enough??? can we find a good evaluation way to do the experiments and then prove the model interpretable??
* From QA-GNN, we can know that, **MHGRN** separate QA context and KG. Then apply LMs to QA and apply GNNs to KG. cannot perform **structure reasoning**(mentioned in the QA-GNN paper)
  * Structured reasoning: enable the model be interpretable and explainable, and it is crucial for making robust predictions.