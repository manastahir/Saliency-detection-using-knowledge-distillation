# Saliency-detection-using-knowledge-distillation
Exploring the concept of knowledge distillation on the task of Saliency detection. 
<hr/>

<p>
Project on a really interesting topic of knowledge distillation. To know about the knowledge distillation concept read this article : <a href="https://towardsdatascience.com/knowledge-distillation-simplified-dd4973dbc764">
Article.</a>
</p>

<h2> About the project </h2>

<h4> Model </h4>

<h5>Teacher model</h5>
<p>
I applied the knowledge distillation to the task of saliency detection. The <i>MSI-NET</i> presented in the paper <a href="https://www.sciencedirect.com/science/article/pii/S0893608020301660">
Contextual encoder–decoder network for visual saliency prediction</a> is used as the teacher model. Teacher model has approximately <b>25 million parameters</b>.
This github <a href="https://github.com/alexanderkroner/saliency">repository</a> provides the implementaion of the model in tensorflow, dataset links and related files. 
</p>
<img src="https://github.com/manastahir/Saliency-detection-using-knowledge-distillation/blob/master/teacher%20model.jpg">

<h5>Student Model</h5>
</p>
The student model simply consists of Resnet18 backbone, the output from the last residual block is passed to a series of UpScale2D and Convolution2D layers. For comparison of simple training with
teacher-student training two variants were implemnted. <br/><br/>
<b>Model A</b>: simple model with unbranched decoder and produces just one output: a saliency map. <br/>
<b>Model B</b>: student model with last layer of the decoder branched to produce 2 outputs: a saliency map and a feature map for correspondance with teacher output.<br/>
</p>


<h4>Data</h4>
<p>
Dataset used is the SALICON dataset <a href="http://salicon.net/download/">Link</a><br/>
Along with the original dataset the output from the teacher model is also generated for both trainining and validation images(stimuli) and stored.
</p>

```shell
python ./saliency/main.py test -p ./data/salicon/stimuli/train
python ./saliency/main.py test -p ./data/salicon/stimuli/val
```

<h4>Training</h4>
