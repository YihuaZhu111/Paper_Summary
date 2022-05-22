# Information

* **Fusing Context Into Knowledge Graph for Commonsense Question Answering**
* Yichong Xu∗, Chenguang Zhu∗, Ruochen Xu, Yang Liu, Michael Zeng, Xuedong Huang
* code: https://github.com/microsoft/KEAR
* URL: https://arxiv.org/abs/2012.04808
* other: ACL2021



# Motivation

* QA-GNN only uses Glove to do the node embedding, which may cause the node contains less information, this paper (DEKCOR) adds the contextual information to the model and the reasoning process. And finally, it can get better results with a much smaller model.



# Background

* commonsense reasoning has emerged as an important task in natural language understanding, with various datasets and models proposed in this area.
* These methods(graph structure methods) combine the merits of language modeling and structural knowledge information and improve the performance of commonsense reasoning and question answering. 
* although a KG can encode topological information between the concepts, it lacks rich context information.
* DEKCOR model can combine the contextual information.



# Approach

![image-20220521212433328](https://tva1.sinaimg.cn/large/e6c9d24egy1h2gc6upqfqj21p80u0dmz.jpg)



* use **KCR method** (Jession Lin. 2020. Knowledge chosen by relations.) to select relation triples. 
  * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2gconkmoaj21hk0s6q8m.jpg" alt="image-20220521213331606" width="600" />
* **Reasoning** (attention_based framework)
  * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2gcorkx3sj20n20iewf6.jpg" alt="image-20220521213559319" width="300" />



# Experiments

* **datasets and baselines**: 
  * CommonsenseQA (Commonsenseqa: A question answering challenge targeting commonsense knowledge)
  * OpenBookQA (Can a suit of armor conduct electric- ity? a new dataset for open book question answering)
* **Result**
  * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2gcowi7hzj20u00wwq76.jpg" alt="image-20220521215128274" width="400" />
  * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2gcp06bvzj219c0u078t.jpg" alt="image-20220521215241968" width="400" />



# Review

* QA-GNN only use the information of Knowledge Graph(conceptnet), we can add the contextual information to QA-GNN.
* use the pre-trained LM can combine the contextual information with the graph structure. For example,  in qa-gnn, we can use this methods to do the node embedding but not just only use Glove.
* AMR-SG (https://arxiv.org/abs/2105.11776) can use AMR structure to connect large textual information with graph structure to do the Question Answering. Can we do something for that? 
