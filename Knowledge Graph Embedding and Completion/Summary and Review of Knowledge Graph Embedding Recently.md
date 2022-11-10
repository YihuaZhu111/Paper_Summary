# Summary and Review of Knowledge Graph Embedding Recently



## Papers:

### Rotation part:

* ComplE: Complex Embeddings for Simple Link Prediction (https://proceedings.mlr.press/v48/trouillon16.html)
* RotatE: Knowledge Graph Embedding by Relational Rotation in Complex Space (https://arxiv.org/abs/1902.10197)
* PairRE: Knowledge Graph Embeddings via Paired Relation Vectors (http://arxiv.org/abs/2011.03798)
* HAKE: Learning Hierarchy-Aware Knowledge Graph Embeddings for Link Prediction (https://ojs.aaai.org/index.php/AAAI/article/view/5701)
* QuatE: Quaternion Knowledge Graph Embeddings (https://proceedings.neurips.cc/paper/2019/hash/d961e9f236177d65d21100592edb0769-Abstract.html)
* RotateCT: Knowledge Graph Embedding by Rotation and Coordinate Transformation in Complex Space (https://aclanthology.org/2022.coling-1.436)
* CompoundE: Knowledge Graph Embedding with Translation, Rotation and Scaling Compound Operations (http://arxiv.org/abs/2207.05324)
* Dual Quaternion Knowledge Graph Embeddings (https://ojs.aaai.org/index.php/AAAI/article/view/16850)
* Knowledge graph embedding by relational and entity rotation (https://linkinghub.elsevier.com/retrieve/pii/S0950705121005724)
* Learning Hierarchy-Aware Quaternion Knowledge Graph Embeddings with Representing Relations as 3D Rotations (https://aclanthology.org/2022.coling-1.175)
* LineaRE: Simple but Powerful Knowledge Graph Embedding for Link Prediction

### Topology and Space part:

* Low-Dimensional Hyperbolic Knowledge Graph Embeddings (http://arxiv.org/abs/2005.00545)
* BiQUE: Biquaternionic Embeddings of Knowledge Graphs (http://arxiv.org/abs/2109.14401)
* Geometry Interaction Knowledge Graph Embeddings
* 5* Knowledge Graph Embeddings with Projective Transformations (https://ojs.aaai.org/index.php/AAAI/article/view/17095)
* Ultrahyperbolic Knowledge Graph Embeddings (http://arxiv.org/abs/2206.00449)

## Dataset Information

* ![截屏2022-11-05 21.30.18](https://tva1.sinaimg.cn/large/008vxvgGgy1h7uiz60iftj314m090tb1.jpg)
* ![截屏2022-11-05 21.30.45](https://tva1.sinaimg.cn/large/008vxvgGgy1h7uiznoo9yj315m08iac1.jpg)
* 

## Summary of Problems in Knowledge Graph Embedding

* Complex Relation: 1-N, N-1, N-N.
* Relation Patterns:
  * Symmetry
  * Antisymmetry
  * Inverse
  * Composition (need non-commutative composition and associative (DualE))
    * Non-commutative compostion
      * need to incorporate translation and rotation(From DualE and RotateCT)
    * commutative composition 
  * Hierarchy
* Multiple relations (shown in DualE)
* Multiple subgraph structures in a neighborhood (combination of loop and path structure, 5 star)



## Mathematic

* Mathematic about complex space and Quaternions (RotatE and QuatE)
  * https://krasjet.github.io/quaternion/quaternion.pdf
  * https://www.bilibili.com/video/BV1SW411y7W1/?spm_id_from=333.1007.top_right_bar_window_custom_collection.content.click&vd_source=b6fe625c6d3a78a798c706d2e7f2bc2b
* Dual Quaternion (DualE)
  * in paper, and https://en.wikipedia.org/wiki/Dual_quaternion
* Biquaternion (BiQUE)
  * in paper.

## Summary of Paper



### RotatE

* Background and Motivation
  * In order to model several relation patterns (symmetry, antisymmetry, inverse, composition)
* Method
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7rxhpntbjj30w00u0q6j.jpg" alt="截屏2022-11-03 15.35.27" style="zoom: 33%;" />
  * Self-adversial negative sampling.
    * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7rxj8h830j30yc044jrm.jpg" alt="截屏2022-11-03 15.37.11" style="zoom:33%;" />
    * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7rxjonsyjj30q603u74j.jpg" alt="截屏2022-11-03 15.37.38" style="zoom:33%;" />
    * **What is the fr here????**
* experiment and result
  * the experiment about relation patterns need more examples but not just two or three examples to show the final results.

### QuatE

* Background and Motivation
  * more expressive hypercomplex representation than RotatE.
* Mathematic about complex space and Quaternions
  * https://krasjet.github.io/quaternion/quaternion.pdf
  * https://www.bilibili.com/video/BV1SW411y7W1/?spm_id_from=333.1007.top_right_bar_window_custom_collection.content.click&vd_source=b6fe625c6d3a78a798c706d2e7f2bc2b
* Method
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7s6sogxpij30u010843r.jpg" alt="IMG_0036" style="zoom: 25%;" />
* Experiment and result
  * accuracy result is good, while **no results for relation patterns**.
* Review
  * 文章具体没说为什么head和relation用hermilton product，但之后用inner product。其hermilton所代表的几何空间意义是指空间3d的旋转，所以最后实验很难直观的像rotate一样有关于relation patterns的结果，这也是最后没有结果的原因。
  * 从2d到3d的一个延伸。是否能有直观的实验结果可以证明其具有一些relation patterns的属性呢？各类角度该如何表达。
  * 后续有一篇文章，DualE, 是8元组，更加丰富了4元组，同样也是在实验上无法论证，只能单靠理论证明。

### DualE

* Background and Motivation

  * embrace a richer set of relational information. More expressive than QuatE.
  * incorporate translation and rotation.
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7u85o97kfj30vs0amt9r.jpg" alt="截屏2022-11-05 15.15.39" style="zoom:33%;" />

* Problem: 

  * Multiple Relations

    * example: <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7u90lbfouj31fm0i4q5z.jpg" alt="截屏2022-11-05 15.45.40" style="zoom: 33%;" />

    * neither translation nor rotation can represent multiple relations (John is the father and guardian of Hunk)
    * some translation family like TransR can represent simple multiple relations, while they cannot model some special relations like inverse and symmetry relation simultaneously. 

* Methematic:

  * in paper, and https://en.wikipedia.org/wiki/Dual_quaternion

* Method

  * similar to QuatE
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7ubpo0ig0j313a0slte3.jpg" alt="IMG_15275799580C-1的副本" style="zoom:25%;" />

* Experiment and results:

  * Pool

* Review:

  * dual quaternion is non-commutative and associative, that can be helpful for the composition relation pattern.  Composition 中有不可互换的性质，但是需要具有交换律。
  * 实验部分垃圾，和quate一样，不可以从实验结果看出具有一系列性质。

### PairRE

* Background and Motivation
  * Want to have Complex relation and several relation pattern simultaneously.
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7uc0dq755j315i092406.jpg" alt="截屏2022-11-05 17.29.18" style="zoom: 25%;" />
* Method:
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7uc51dq5wj30u00w1q4u.jpg" alt="截屏2022-11-05 17.33.39" style="zoom:25%;" />
* Experiment and results
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7uc7vt22zj310e0u0tde.jpg" alt="截屏2022-11-05 17.36.30" style="zoom:25%;" />
* Review:
  * 实验结果无法复现
  * 和rotate一样，举例单一，如果可以多举例子，然后综合起来在一张图中，会更有说服力。
  * 文章方法，归纳后发现和HAKE中modulus part中的mixture bias本质是在做一个东西。
  * 但是文章方法和思路对于处理relation patterns 和complex relation 有启发意义。

### HAKE

* Background and Motivation
  * Hierarchy
* Method
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7ucdwnug2j30yp0u0wkk.jpg" alt="截屏2022-11-05 17.42.18" style="zoom:33%;" />
* Experiment and Result:
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7ucf3rgouj30pq0fkjtu.jpg" alt="截屏2022-11-05 17.43.27" style="zoom: 25%;" />
* Review
  * 文章可以复现，准确度的效果很好。实验结果同样找的一两个例子，可以多举例子，并且总结到一张图上。
  * 但是实验部分，method中的lamda，不是用valid data找出来的，而是自己手动设置的，可以算是一种cheating。
  * 同时单拆出来最后embedding中的一部分，阐明其具有hierarchy的性质是否合理？如上图实验结果。和hyperbolic embedding 直接map到hyperbolic的方法使其具有hierarchy的性质不同，这个方法不够严谨。
  * 本质上是从rotate而来，只是限制了rotate的modulus part。

### RotatCT

* Background and Motivation

  * infer the non-commutative composition patterns and improve the computational efficiency.
  * the combination of rotation and coordinate transformation in complex plane is non-commutative.

* Method

  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7uim6gqbbj30rs0cu3z5.jpg" alt="截屏2022-11-05 21.16.43" style="zoom:25%;" />

    <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7uim3icx3j30mg05st8r.jpg" alt="截屏2022-11-05 21.17.20" style="zoom: 33%;" />

* Experiment and Result

  * case study

* Review

  * 本质上就是translation和rotation的结合，只是换了一个说法。
  * 同时也印证了，non-commutative需要translation和rotation的结合。

### MRotatE

* Background and Motivation
  * like PairRE, want to have Complex relation and several relation pattern simultaneously.
* Method
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7uki429r5j31c80sg786.jpg" alt="截屏2022-11-05 22.23.10" style="zoom: 25%;" />
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7ukrhib2qj31330fxacs.jpg" alt="IMG_46CBB1062B8A-1" style="zoom:25%;" />
  * the distance between the head and tail entities and the distance of the corresponding relations are close enough
* Experiment and Result
  * dataset complex relation number<img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7ul6n4hlqj31580n2tc1.jpg" alt="截屏2022-11-05 22.46.43" style="zoom:33%;" />
* Review
  * 不太喜欢这种用weight硬加的方法，因为最后的embedding就有两部分，并不是一个整体。文中提到best weight setting, 是意味着这个也是和hake一样是人为控制的么？那也算是cheating。
  * 方法比较单一，但是可以得出一定的对于complex relation的启示，可以增加对relation的自由度，从而达到自由学习的效果。pairre是给头尾分别增加一个r，本文是增加r的自由度。
  * 第二部分，只限制了head,只对1-n有有效果，n-1没有效果。。后续实验也印证了这一点。
  * 实验部分对于具体细节的描述值得借鉴，1-n,n-1，n-n的分开实验做的很好。

### LinearRE

* Background and Motivation
  * like PairRE, complex relation and several relation patterns.
* Method
  * add a bias part based on PairRE
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7ullloi9wj30d202iq2t.jpg" alt="截屏2022-11-05 23.01.04" style="zoom:33%;" />
* Experiment and Result
  *  <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7uln9aumlj31rk0fo0vs.jpg" alt="截屏2022-11-05 23.02.41" style="zoom:25%;" />
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7ulns81pyj30u00v1439.jpg" alt="截屏2022-11-05 23.03.10" style="zoom:25%;" />
* Review
  * relation patterns的实验部分比较完善，不是像之前rotate和pairre一样单例，而是很多。以后要做此类实验可以借鉴。
  * 其余review和pairre一样

### CompoundE

* **no code provided**

* Background and Motivation
  * combine Translation, Rotation, and Scaling three operations in the KGE models.
* Method
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7umz12rp1j312k0m9q5z.jpg" alt="IMG_A37FEB57618F-1" style="zoom: 33%;" /><img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7un7g9wnrj31mq0h4q5d.jpg" alt="截屏2022-11-05 23.56.28" style="zoom:25%;" />
  * this formula can model TransE, RotatE, PairRE, LinearRE. and it can have non-commutative composition.
* Experiment and Result
  * this part need more
* Review
  * 是从机器人学中过来的，融合上三种具体形式translation, rotation, and scaling，算是比较经典的融合，但是论文不知道为什么不提供代码，无法复现。
  * 是否可以考虑机器人学中的DH算法？或者是换成3d的效果，会不会更好？
  * 和其余几篇（下面总结的）论文的方法本质上是相似的。

### ATTH

* Background and Motivation
  * want to caature hierarchy and logical patterns simultaneously.
  * combine hyperbolic reflection and rotation by using attention framework.
  * **add rotation operations into hyperbolic embedding.**
* Method
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7wxemh9owj30u010f7bm.jpg" alt="IMG_A148F841F82A-1" style="zoom: 33%;" />
* Experiment and Result
  * No relation patterns visulization results
  * code by tensorflow.
* Review
  * 本文最大的启发在于，在双曲空间中进行rotation的操作，之前一直只有translation的操作。
  * 是否可以将这一方法灵活运用在其余的方法中。融合一下？（以下几篇和空间有关的论文）。

### 5 star

* Background and Motivation
  * cannot cpature well on multiple subgraph structure (path and loop structure)
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7xppkn450j30sm0mywjt.jpg" alt="截屏2022-11-08 15.39.53" style="zoom:25%;" />
  * propose a metheds that can have translation, rotation, homothety, inversion, and reflection, 5 star.
* Method
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7xyw97qmvj31880krq63.jpg" alt="IMG_48B31CE176C0-1" style="zoom: 25%;" /><img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7xyxrghvyj30vm0f8783.jpg" alt="截屏2022-11-08 20.59.12" style="zoom:25%;" />
* Experiment and result
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7xz0gcwt8j31p30u0wlc.jpg" alt="截屏2022-11-08 21.01.42" style="zoom: 25%;" />
  * can verify the hypotheses shown in intrduction, although just a example "hypernym".
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7xz24uli4j31ue0qmk10.jpg" alt="截屏2022-11-08 21.03.28" style="zoom:25%;" />
  * clustering can perform better.
* Review
  * 实际是将relation看成了莫比乌斯空间转换，去解决path-loop的问题。在relation上下足了功夫。
  * 本文的实验内容也比较好，实验结果证明了自己所提出的猜想。
  * 本文提供了思路，两个思路：
    * 从dataset中找到目前的triple的很多特性和特点，然后看是否有space transformation可以解决。
    * 直接看有关space transformation的内容（数学，几何，拓扑，映射），然后思考目前的dataset是否有这样的triple需要去解决。
  * 有时候relation可以有表示不同程度的关系。。这时候需要借助isometry来定义？？？？可行？

### GIE

* Background and Motivation
  * previous work embeded KGs into single geometric space (Euclidean space, hyperbolic space)
  * this paper use attention framework to combine E, H, and hypersphercial space.
* Method
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h80c26v8nqj30u00xnwkh.jpg" alt="IMG_33E8F224FBD2-1" style="zoom: 25%;" />
  * do rotation and translation in Euclidean, Hyperbolic, and Hyperspherical space, then use attention   framework to combine them together.
* Experiment and Result
  * Pool.......
* Review
  * 实验做的很少很烂。
  * 用attention的方式把三个空间结合，不确定是否真的在几何上有什么意义，就好像之前hake一样只是相加。
  * 是否有空间上的结合可以将三者(E,H,S)或者两者（E,H）结合？
  * **先在欧几里得空间rotation，translation，然后在hyperbolic空间rotation，translation。连接起来！！！！！！**

### 　BiQUE

* Background and Motivation
  * combine Euclidean rotation and hyperbolic transformations, in a coherent geometric representation. (same space, not simplely use attention framework to do so).
  * Employ Biquaternions to intergrate multiple geometric transformations. (scaling, translation, Euclidean rotation, and hyperbolic rotation) (注意这里没有hyperbolic translation, 是否可以加一个上去？)
* Method
  * <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7z6pvr8udj30vv0u0jw6.jpg" alt="IMG_5EE19383BA6B-1" style="zoom:25%;" />
  * method like QuatE with adding a translation part before the multiplication.
* Experiment
  * the experiment to show the hierarchy is pool.
* Review
  * 发现有关于体现hierarchy的论文，实验以及结果都很敷衍。
  * 和QuatE方法基本一致，只是在开始之前加了一个translation的部分。虽然证明了不少是Euclidean rotation 和 Hyperbolic rotation的结合，但是不太懂证明的部分，而且最后方法部分完全没有体现。

### UltraE

































