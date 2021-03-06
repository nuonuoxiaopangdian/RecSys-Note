### *Title: Adversarial Learning to Compare: Self-Attentive Prospective Customer Recommendation in Location based Social Networks*

###### Authors: Ruirui Li,Xian Wu, Wei Wang

###### Publication: [WSDM '20: Proceedings of the 13th International Conference on Web Search and Data Mining](https://dl.acm.org/doi/proceedings/10.1145/3336191)January 2020 Pages 349–357https://doi.org/10.1145/3336191.3371841

###### Note: Yiming Cao



#### **1. Introduction**

- In location-based social networks (LBSNs), prospective customer predictions suffer severely from data sparsity. For those new businesses and customers, we have limited information.
- introduce a Self-Attentive prospective Customer RecommendAtion framework, SACRA, which learns to recommend by making comparisons among **users’ historical check-ins** with **adversarial training**. 
  - Each check-in business of a user is explained with attention to all his/her historical check-in businesses.

#### 2. **Preliminaries**

- *Prospective customer recommendation*

  - rank candidate customers given a business. 

  - The goal is to rank the true incoming new customers higher than other candidates. 

  - The candidates here are all customers who have not checked in this business before.

    

#### 3. Methods
<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/df5cb3d6a64943cfaccc9982957bafbe" width="50%" height="50%" />

- *Multi-head Fusion Network*
  - to complement each check-in business with others, we feed the business embeddings into a multi-head fusion network, the output of which yields the fused business representations.
  - the multi-head attention operation takes the business embeddings *EB* ∈ R*c*×*d* as the inputs,  the results of which are further concatenated as the final output.
  - Each fused business embedding *E*˜*Bi* is a weighted sum of business embedding of itself and other related businesses, where each weight gauges the similarity between one business and another one in *B*. (pairwise closeness)

- *Aggregation Attention Network*

  -  to derive the aggregated representative business embedding

  <img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/9f083ea53c5d4e668f8e862c6f38fa34" width="30%" height="30%"/>

- *Check-in Tendency Network*
  - to model the check-in tendency between user *u* and business *b*, we compare the similarity between the embedding *Eb* of the investigated business *b* and the representative fused business embedding*E*¯*B*.
  - the similarity is represented by *Eb* • *E*¯*B*, where • represents the element-wise multiplication. The similarity is then concatenated with the user embedding *Eu* , the geographical features *Eд*(*b*,*u*), and fed into a one-layer neutral network to calculate the check-in tendency.
  - apply a pairwise ranking scheme to measure the ranking error defined on a business *b*, as well as two users *u*+ and *u*- :
  
  <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/12d57ded1f6a453b8195e6eb46d33163" width="70%" height="70%" />


- *Adversarial Training*

  - additionally optimize the model to minimize the objective function with the perturbed parameters. Formally, we define the objective function with adversarial examples incorporated as

    <img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/232b907e50724e6aa5f16c67ce1b64d6" width="30%" height="30%" />

  - the training process can be summarized as playing a minimax game

    <img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/836d09ff90c749109a55c01982ca3389" width="30%" height="30%" />

  - constructing adversarial perturbations

    - Given a training instance (*b*,*u*+,*u*-), the problem of constructing adversarial perturbations ∆*adv* is formulated as maximizing、
    
  <img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/e9f1121481db42aeaa3c61087d7ca518" width="70%" height="70%" />
  
  <img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/c913ba42230e42929d739adc9cc6e25f" width="70%" height="70%" />

- *Geographical Influence*
  - employ the Gaussian mixture model (GMM) to generate the geographical features.

#### 4. Experiments

<img src="https://p26-tt.byteimg.com/origin/pgc-image/a45789a08fbe4dd6a1c53fdc28ecdcc0" width="50%" height="50%"  />

- *Evaluation*
  - evaluate the ranking list using **Hit Ratio (HR)** and**Normalized Discounted Cumulative Gain (NDCG)**. (*HR* is a recall-based metric, measuring whether the testing item is in the top-K list. While *NDCG* is position-sensitive,which assigns higher score to hits at higher positions.)
- *Baselines*
  -  WRMF is a point-wise matrix factorization method while MMMF and BPRMF are pair-wise based. 
  - CofiRank, CLiMF focus on optimizing top ranked positions. 
  - USG, GeoMF, Rank-GeoFM, ASMF, ARMF, and CORALS utilize additional information, such as check-in locations, social relationship, businesses’ attributes, online reviews and temporal information to improve recommendation performance in LBSNs. 
  - SAE-NAD utilizes auto-encoders, with business neighborhood information considered, to make recommendations.

<img src="https://p26-tt.byteimg.com/origin/pgc-image/aac9620c2a224f848a701f06d8ea63b7" width="50%" height="50%" />

