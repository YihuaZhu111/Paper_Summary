# Information

* **Large-Scale Relation Learning for Question Answering over Knowledge Bases with Pre-trained Language Models**
* Yuanmeng Yan1, Rumei Li2, Sirui Wang2, Hongzhi Zhang2, Daoguang Zan3 Fuzheng Zhang2, Wei Wu2, Weiran Xu1∗
* URL: https://aclanthology.org/2021.emnlp-main.296/
* Code: https://github.com/yym6472/kbqarelationlearning
* Other: EMNLP2021, short paper



# Motivation

* **Domain:** QA over KB.
* novel method. pay attention on **Relation Extraction, Relation Matching, Relation Reasoning**.



# Background

* Traditional retrieval-based KBQA technologies(name entity recognization, entity linking, subgraph retrieval, and entity scoring) have achieved remarkable performance.
* KBQA(multi-hop) still has challenges:
  * difficult to align the natural language questions with the reasoning paths in the KB.
  * the KB is often incomplete, which requires the model to reason over the incomplete graph.
* To solve these problems, some approaches have been proposed, but their approach mainly grasps the topological structure of the graph but ignores the textual information in entities and relations that should be also useful to score candidate entities.
* this paper bridges the gap between the natural language and the structured KB. and can explicitly train the model to reason over the incomplete KB.



# Approach

* ![image-20220522171059291](https://tva1.sinaimg.cn/large/e6c9d24egy1h2h8zr28tlj221q0u0wqh.jpg)
* Main task:
  * in the figure 2a
  * **but can the LM substitute the large textual information???**
* RE trains the model through inferring relations from the sentences.
  * use the relation extraction dataset
* RM through determining whether two sentences express the same relation. 
  * the label is 1 if s1 and s2 express the same relation and 0 otherwise.
* RR constructs the training data from the KB in a self-supervised manner and trains the model to reason over the missing KB connections given the existing paths.



# Experiment

* **Dataset**
  * KBQA dataset: WebQuestionsSP (WebQSP, https://www.microsoft.com/en-us/research/publication/semantic-parsing-via-staged-query-graph-generation-question-answering-with-knowledge-base/)
  * Relation Extraction Datasets: 
    * WebRED
    * FewRel
* **Results**
  * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2h9hatg9pj20u010yq82.jpg" width="40%">
* **Analysis**
  * <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h2hc5f6kksj20u00yl42r.jpg" width="40%">



# Review

* can the LM substitute the large textual information???
* the method for solving incomplete KG problems is useful.
  * ![image-20220522190634569](https://tva1.sinaimg.cn/large/e6c9d24egy1h2hcfybdm5j21xc0k8jx4.jpg)



