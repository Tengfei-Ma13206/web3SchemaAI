# Fine Tuning

## Raise a Child in Large Language Model: Towards Effective and Generalizable Fine-tuning

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>The illustration of CHILD-TUNING. Left: It forwards on the whole network while backwarding on a subset of network (i.e., child network). Right: To achieve this, a task-free or task-driven mask is performed on the gradients of the non-child network, resetting them to zero (grey diagonal grids).</p></figcaption></figure>

In recent years, the field of natural language processing (NLP) has witnessed a significant leap forward with the development of large pretrained language models (PLMs). These models, often comprising millions to billions of parameters, have become the cornerstone for a wide range of NLP tasks, such as text classification, question-answering, and language translation. The power of PLMs lies in their ability to understand and generate human-like text based on the vast amount of information they've learned during their initial training phase, often referred to as "pretraining."

#### The Challenge of Fine-Tuning Large Models

Despite their impressive capabilities, deploying these large PLMs for specific tasks (known as "downstream tasks") poses a significant challenge, especially when the available training data for these tasks is limited. The conventional approach to making a PLM adept at a specific task involves "fine-tuning," where the model's parameters are slightly adjusted using the task-specific dataset. However, fine-tuning an enormous model with a relatively small dataset can lead to overfitting, where the model performs well on its training data but fails to generalize to new, unseen data. This overfitting problem is particularly acute for large PLMs due to their vast number of parameters relative to the typically much smaller size of task-specific datasets.

#### Introducing CHILD-TUNING

To address this challenge, a novel fine-tuning technique called CHILD-TUNING has been proposed. The essence of CHILD-TUNING lies in its innovative approach to updating only a subset of the model's parameters during the fine-tuning process. By strategically "masking" the gradients of certain parameters—effectively preventing them from being updated—the technique focuses the fine-tuning effort on a specific part of the model, referred to as the "child network."

**How CHILD-TUNING Works**

During the backward pass of the training process, where gradients are computed to update the model's parameters, CHILD-TUNING employs a mask to zero out the gradients for the non-child network parameters. This selective updating allows the full model to leverage its prelearned knowledge while ensuring that only the most relevant parameters for the task at hand are refined. This process can be visualized as follows:

1. **Forward Pass:** The entire model processes the input data, leveraging its full capacity.
2. **Backward Pass with Masking:** During backpropagation, a mask is applied to the gradients of the non-child network parameters, setting them to zero and thus preventing their update.
3. **Parameter Update:** Only the child network's parameters are updated based on the computed gradients, focusing the fine-tuning on this subset of the model.

**Variants of CHILD-TUNING**

CHILD-TUNING comes in two flavors, differing in how the child network is determined:

* **CHILD-TUNINGF:** This variant selects the child network randomly, without considering the specific task. This approach introduces a form of regularization, helping to prevent overfitting to the small dataset by injecting noise into the training process.
* **CHILD-TUNINGD:** This variant takes a task-driven approach, identifying the most relevant parameters for the specific downstream task and designating these as the child network. This method effectively narrows down the hypothesis space of the model, focusing its learning capacity on the task-relevant aspects.

#### Advantages of CHILD-TUNING

The experiments conducted with CHILD-TUNING have demonstrated its effectiveness across various NLP tasks, consistently outperforming conventional fine-tuning techniques. By focusing the fine-tuning on a subset of parameters, CHILD-TUNING achieves better task performance and generalization to new data. Moreover, because CHILD-TUNING's approach is orthogonal to other fine-tuning methods, it can be combined with them for even further improvements.

#### Conclusion

CHILD-TUNING represents a significant advancement in the fine-tuning of large pretrained language models for downstream NLP tasks. By strategically updating only a subset of the model's parameters, it effectively addresses the challenge of fine-tuning with limited task-specific data, leading to models that are both more performant and generalizable. This technique opens new avenues for efficiently leveraging the power of large PLMs across a wider array of tasks and datasets, making advanced NLP capabilities more accessible and effective.
