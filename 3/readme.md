# Semeval Task-3



##### 本存储库主要包含 [SemEval-2022 任务 3 - 预设分类法：评估神经网络语义 (PreTENS)](https://sites.google.com/view/semeval2022-pretens/)的结果和代码文件。 我们首先从牛津词典中收集定义以增强知识，将这些定义作为提示添加到需要分类的实体的编码器中。 然后，我们采用带 FGM 方法的 Deberta-v3 模型，为两个子任务训练英语和法语数据集，其中意大利语数据集被翻译成英语以进行数据增强。 最后，通过回归任务对训练好的分类模型进行微调（500 个来自回归，5000 个来自分类数据集）。 实验结果表明，所提出的方法在两个子任务中均胜出，证明了我们方法的有效性。



#### 流程

1. utils.py是官方文件的评分代码；
2. read.py 读取三个不同语种的数据集，并以1:8划分验证集与训练集；
3. read_ner.py中，我们遍历所有的数据集（训练集与测试集），找到其中词频较低的词汇，我们默认这些词汇是有待分类的层次性词汇，之后再次遍历数据集，如果一段话中蕴含两个完整词汇，则将本条样本重构为实体抽取样本，并将两个完整词汇作为标签；
4. train_ner.py,是训练实体抽取模型的代码，基于mdeberta进行训练，将上一流程中两个词汇标记为1，其余为0，训练TokenClassification模型，进行实体抽取任务；
5. all_ner.pu 是将训练完成的实体抽取模型，对所有的数据集进行实体抽取，抽取出整个数据集中所有的实体；
6.    unknown  是定义爬取代码，负责将步骤4中抽取到的实体从牛津词典中爬取定义；
7.  translate.py 将意大利语数据集翻译成英文；
8. train_task1.py和train_task2.py分别是任务一与任务二的训练代码；
9. test_task1.py和test_task2.py是生成任务一与任务二结果的代码。

## Cite
```

@inproceedings{xia-etal-2022-lingjing,
    title = "{L}ing{J}ing at {S}em{E}val-2022 Task 3: Applying {D}e{BERT}a to Lexical-level Presupposed Relation Taxonomy with Knowledge Transfer",
    author = "Xia, Fei  and
      Li, Bin  and
      Weng, Yixuan  and
      He, Shizhu  and
      Sun, Bin  and
      Li, Shutao  and
      Liu, Kang  and
      Zhao, Jun",
    booktitle = "Proceedings of the 16th International Workshop on Semantic Evaluation (SemEval-2022)",
    month = jul,
    year = "2022",
    address = "Seattle, United States",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2022.semeval-1.30",
    doi = "10.18653/v1/2022.semeval-1.30",
    pages = "239--246",
    abstract = "This paper presents the results and main findings of our system on SemEval-2022 Task 3 Presupposed Taxonomies: Evaluating Neural Network Semantics (PreTENS). This task aims at semantic competence with specific attention on the evaluation of language models, which is a task with respect to the recognition of appropriate taxonomic relations between two nominal arguments. Two sub-tasks including binary classification and regression are designed for the evaluation. For the classification sub-task, we adopt the DeBERTa-v3 pre-trained model for fine-tuning datasets of different languages. Due to the small size of the training datasets of the regression sub-task, we transfer the knowledge of classification model (i.e., model parameters) to the regression task. The experimental results show that the proposed method achieves the best results on both sub-tasks. Meanwhile, we also report negative results of multiple training strategies for further discussion. All the experimental codes are open-sourced at https://github.com/WENGSYX/Semeval.",
}
```
