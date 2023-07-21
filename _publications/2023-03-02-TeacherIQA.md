---
title: "Teacher-Guided Learning for Blind Image Quality Assessment"
collection: publications
permalink: /publication/2023-03-02-TeacherIQA
excerpt: 'The performance of deep learning models for blind image quality assessment (BIQA) suffers from annotated data insufficiency. However, image restoration, as a closely-related task with BIQA, can easily acquire training data without annotation. Moreover, both image semantic and distortion information are vital knowledge for the two tasks to predict and improve image quality. Inspired by these, this paper proposes a novel BIQA framework, which builds an image restoration model
as a teacher network (TN) to learn the two aspects of knowledge and then
guides the student network (SN) for BIQA. In TN, multi-branch convolutions are leveraged for performing adaptive restoration from diversely
distorted images to strengthen the knowledge learning. Then the knowledge is transferred to the SN and progressively aggregated by computing long-distance responses to improve BIQA on small annotated data.
Experimental results show that our method outperforms many state-ofthe-arts on both synthetic and authentic datasets. Besides, the generalization, robustness and effectiveness of our method are fully validated.
The code is available in https://github.com/chencn2020/TeacherIQA.'
date: 2023-03-02
venue: 'ACCV 2022'
paperurl: 'https://openaccess.thecvf.com/content/ACCV2022/papers/Chen_Teacher-Guided_Learning_for_Blind_Image_Quality_Assessment_ACCV_2022_paper.pdf'
citation: 'Chen Z, Wang J, Li B, et al. Teacher-Guided Learning for Blind Image Quality Assessment[C]//Proceedings of the Asian Conference on Computer Vision. 2022: 2457-2474.'
---

# Abstract 

# Introduction

# Experiments


[Download paper here](https://openaccess.thecvf.com/content/ACCV2022/papers/Chen_Teacher-Guided_Learning_for_Blind_Image_Quality_Assessment_ACCV_2022_paper.pdf)

Recommended citation:
```
@inproceedings{chen2022teacher,
  title={Teacher-Guided Learning for Blind Image Quality Assessment},
  author={Chen, Zewen and Wang, Juan and Li, Bing and Yuan, Chunfeng and Xiong, Weihua and Cheng, Rui and Hu, Weiming},
  booktitle={Proceedings of the Asian Conference on Computer Vision},
  pages={2457--2474},
  year={2022}
}
```