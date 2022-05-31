# Information

* A Survey on Knowledge Graphs: Representation, Acquisition, and Applications
* Shaoxiong Ji , Shirui Pan , *Member, IEEE*, Erik Cambria , *Fellow, IEEE*, Pekka Marttinen , and Philip S. Yu , Life Fellow, IEEE
* URL: https://ieeexplore.ieee.org/abstract/document/9416312
* Code: no code
* other: this summary is mainly on the part of KGC over the survey.



# Motivation

* Want to detect the new direction for Knowledge Graph, and the Knowledge Graph Completion is a good direction, therefore, find this survey to learn and try to find some potential and interesting detailed directions.



# Overview

* construct a knowledge graph from unstructured text and other sources, complete an existing graph, and discover or recognize entities and relations.
* ![image-20220523224538668](https://tva1.sinaimg.cn/large/e6c9d24egy1h2ioabajkij21ak0u0ahp.jpg)



# Main Content



## Knowledge Graph Completion



* KGC is developed to add new triples to a KG.
* **Embedding-Based Models**
  * normal method
    * TransE, TransH, TransR, HolE, R-GCN, and DKRL(referenced in the last summary), these methods calculate scores of all the candidate entities and rank the top-k entities. They represent inputs and candidates in the unified embedding space. 
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2n8nsy42aj20u00w2q4h.jpg" width="30%">
  * ProjE<sup><a href="#ref1">1</a></sup>: finally is a classification problem.
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2n8swrrhsj20u90u00ym.jpg" width="50%">
  * ConMask<sup><a href="#ref2">2</a></sup>: can find new entities and relations from open-world, but not rely on the existing knowledge graph. This model learns embeddings of the entity's name and parts of its description to connect unseen entities to the KG.
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2n9zo7fhyj20u010ptda.jpg" width="60%">
* **Relation Path Reasoning**
  * for this part, the methods were old and cannot get enough attention.
* **RL-Based Path Finding**
  * ![image](https://tva1.sinaimg.cn/large/e6c9d24egy1h2nb3hr8pkj21pc0hk0xj.jpg)
  * *I need to learn **RL** firstly, then come back to this part to follow these papers*
* **Rule-Based Reasoning**
  * Example:
    * <img  src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2o3vtnjq7j20v802c0sx.jpg" width="80%">
  * RLvLR<sup><a href="#ref3">3</a></sup>: 
    * Learning rules automatically from a very large KG is a challenge.
    * RLvLR tries to use embedding in representation learning together with a new sampling method. Based on RLvLR, a new method RLvLR-Stream is developed for learning rules from streams of knowledge graphs.
  * KALE<sup><a href="#ref4">4</a></sup>: jointly embedding the KGs and logical rules.
    * triples are represented as atomic formulae and modeled by the translation as- sumption
    * rules represented as complex formulae and modeled by t-norm fuzzy logic
    * minimizing a global loss over both atomic and complex formulae.
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2o4op0r4wj20sy0istab.jpg" width="60%">
  * Logical rule is one kind of auxiliary information.
    * The combination of neural and symbolic computation has complementary advantages that utilize efficient data-driven learning and differentiable optimization and exploit prior log- ical knowledge for precise and interpretable inference.
  * Markov Logic Network(MLN) and KGE:
    * pLogoicNet<sup><a href="#ref5">5</a></sup>: combine the advantages of MLN and KGE.
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2o76qldawj21oe0u0woy.jpg">
    * ExpressGNN<sup><a href="#ref6">6</a></sup>: generalize pLogicNet by tuning graph networks and embedding and achieves more efficient logical reasoning. (Combine GNNs and MLN)
      * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2o7n1ufvkj21fg0msaeh.jpg" >
* **Metarelational Learning** (few-shot relational learning)
  * **Definition**: requires models to predict new relational facts with only a very few samples.
  * GMatching
  * Meta-KGR<sup><a href="#ref7">7</a></sup>: an optimization-based metalearning approach, adopts model agnostic metalearning for fast adaption and **RL** for entity searching and path reasoning.
  * MetaR<sup><a href="#ref8">8</a></sup>: transfers relation-specific metainformation from support set to query set and archives fast adaption via loss gradient of high-order relational representation.
  * FSRL<sup><a href="#ref9">9</a></sup>: 
    * Existing work of one-shot learning limits method generalizability for few-shot scenarios and does not fully use the supervisory information; 
    * FSRL can effectively capture knowledge from heterogeneous graph structure, aggregate representations of few-shot refer- ences, and match similar entity pairs of reference set for ev- ery relation.
    * ![截屏2022-05-28 23.00.19](https://tva1.sinaimg.cn/large/e6c9d24egy1h2ogtcn6j2j218a0u0tfw.jpg)
  * GANs-R<sup><a href="#ref10">10</a></sup>: 
  * * consider a novel formu- lation, zero-shot learning, to free this cumbersome curation.
    * For newly-added relations, we attempt to learn their semantic features from their text descriptions and hence recognize the facts of unseen relations with no examples being seen
    * For this purpose, we leverage Generative Adversarial Networks (GANs) to establish the connection between text and knowl- edge graph domain: The generator learns to generate the rea- sonable relation embeddings merely with noisy text descrip- tions.
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2oh2vm2cjj20x40r6tdk.jpg" width="50%">
  * GEN<sup><a href="#ref11">11</a></sup>: 
    * not only predict the links between the seen and unseen nodes as in a conventional out-of-knowledge link prediction task but also between the unseen nodes, with only few edges per node.
    * GEN meta-learns both the node embedding network for inductive inference (seen-to-unseen) and the link prediction network for transductive inference (unseen-to-unseen).
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2ohd8swq8j20u00zk0yq.jpg" width="40%">
* **Triple Classification**
  * Triple classification is to determine whether facts are correct in testing data, which is typically regarded as a binary classification problem.



## Entity Discovery

* this part can be divided into four sections, Named Entity Recognition(NER), Entity Typing, Entity Disambiguation, and Entity Alignment. But this part is mainly not about the graph structure, therefore, I will not do the summary for this part.



## Relation Extraction

* **Basic Information**

  * Relation extraction is a key task to build large-scale knowl- edge graphs automatically by extracting unknown relational facts from plain text and adding them into knowledge graphs.
  * this section mainly review the methods with neural relation extraction(NRE).
  * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2p86m7qmoj20lu0diabd.jpg" width="60%">
* **Summary of NRE and Recent Advances**

  * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2rf1athfaj21jk0r27ec.jpg" width="100%">
* **CNNs and RNN**
* O-CNNs<sup><a href="#ref12">12</a></sup> and Multi-CNN<sup><a href="#ref13">13</a></sup>: simple CNN applied for RE. The papers which use CNNs and RNN are old, and I canknow the main ideas from the table.
* **Attention Mechanism**

  * HATT<sup><a href="#ref14">14</a></sup>: incorporate the hierarchical information of relations for distantly supervised relation extraction and propose a novel hierarchical at- tention scheme.
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2pc0ohha3j21g20ss0xz.jpg" width="70%">
  * DSRL<sup><a href="#ref15">15</a></sup>: use BERT.
* **GCN**

  * GCNs are utilized for encoding a dependence tree over sentences or learning KGEs to leverage relational knowledge for sentence encoding.

  * C-GCN<sup><a href="#ref16">16</a></sup>: 
    * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2qplo40m5j21oe0sggsw.jpg" width="80%">
  * AGGCN<sup><a href="#ref17">17</a></sup>: 
    * ![截屏2022-05-30 21.52.20](https://tva1.sinaimg.cn/large/e6c9d24egy1h2qq37cmfmj217i0u0dpg.jpg)
* **Adversarial Training**

  * AT is applied to add adversar- ial noise to word embeddings for CNN- and RNN-based relation extractions.
* **RL**

  * RL has been integrated into NRE recently by training instance selectors with policy networks.



# Reference

1. <span name = "ref1">B. Shi and T. Weninger, “ProjE: Embedding projection for knowledge graph completion,” in Proc. AAAI, 2017, pp. 1236–1242.</span>  

2. <span name = "ref2">B. Shi and T. Weninger, “Open-world knowledge graph completion,” in Proc. AAAI, 2018, pp. 1957–1964.</span>  

3. <span name = "ref3">P. G. Omran, K. Wang, and Z. Wang, “An embedding-based approach to rule learning in knowledge graphs,” IEEE TKDE, vol. 33, no. 4, pp. 1348–1359, Apr. 2021.</span>  

4. <span name = "ref4">S. Guo, Q. Wang, L. Wang, B. Wang, and L. Guo, “Jointly embedding knowledge graphs and logical rules,” in Proc. Conf. Empirical Methods Natural Lang. Process., 2016, pp. 192–202.</span>  

5. <span name = "ref5">M. Qu and J. Tang, “Probabilistic logic neural networks for reasoning,” in Proc. NeurIPS, 2019, pp. 7710–7720.</span>  

6. <span name = "ref6">Y. Zhang et al., “Efficient probabilistic logic reasoning with graph neural networks,” in Proc. ICLR, 2020, pp. 1–20.</span>  

7. <span name = "ref7">X. Lv, Y. Gu, X. Han, L. Hou, J. Li, and Z. Liu, “Adapting meta knowledge graph information for multi-hop reasoning over few-shot relations,” in Proc. Conf. Empirical Methods Natural Lang. Process. 9th Int. Joint Conf. Natural Lang. Process. (EMNLP-IJCNLP), 2019, pp. 3374–3379.</span>  

8. <span name = "ref8">M. Chen, W. Zhang, W. Zhang, Q. Chen, and H. Chen, “Meta relational learning for few-shot link prediction in knowledge graphs,” in Proc. Conf. Empirical Methods Natural Lang. Process. 9th Int. Joint Conf. Natural Lang. Process. (EMNLP-IJCNLP), 2019, pp. 4217–4226.</span>  

9. <span name = "ref9">C. Zhang, H. Yao, C. Huang, M. Jiang, Z. Li, and N. V. Chawla, “Fewshot knowledge graph completion,” in Proc. AAAI, 2020, pp. 1–8.</span>  

10. <span name = "ref10">P. Qin, X. Wang, W. Chen, C. Zhang, W. Xu, and W. Y. Wang, “Generative adversarial zero-shot relational learning for knowledge graphs,” in Proc. AAAI, 2020, pp. 1–8.</span>  

11. <span name = "ref11">J. Baek, D. B. Lee, and S. J. Hwang, “Learning to extrapolate knowledge: Transductive few-shot out-of-graph link prediction,” in Proc. NeurIPS, 2020, pp. 546–560.</span>  

12. <span name = "ref12">D. Zeng, K. Liu, S. Lai, G. Zhou, and J. Zhao, “Relation classification via convolutional deep neural network,” in Proc. COLING, 2014, pp. 2335–2344.</span>  

13. <span name = "ref13">T. H. Nguyen and R. Grishman, “Relation extraction: Perspective from convolutional neural networks,” in Proc. 1st Workshop Vector Space Model. Natural Lang. Process., 2015, pp. 39–48.</span> 

14. <span name = "ref14">X. Han, P. Yu, Z. Liu, M. Sun, and P. Li, “Hierarchical relation extraction with coarse-to-fine grained attention,” in Proc. Conf. Empirical Methods Natural Lang. Process., 2018, pp. 2236–2245</span> 

15. <span name = "ref15">L. Baldini Soares, N. FitzGerald, J. Ling, and T. Kwiatkowski, “Matching the blanks: Distributional similarity for relation learning,” in Proc. 57th Annu. Meeting Assoc. Comput. Linguistics, 2019, pp. 2895–2905</span> 

16. <span name = "ref16">Y. Zhang, P. Qi, and C. D. Manning, “Graph convolution over pruned dependency trees improves relation extraction,” in Proc. Conf. Empirical Methods Natural Lang. Process., 2018, pp. 2205–2215.</span> 

17. <span name = "ref17">Z. Guo, Y. Zhang, and W. Lu, “Attention guided graph convolutional networks for relation extraction,” in Proc. 57th Annu. Meeting Assoc. Comput. Linguistics, 2019, pp. 241–251.</span>

    