# RECVIS_final_project
RECVIS18 Final project on Image Captioning with Region Attention based on the [Neural Baby Talk](http://openaccess.thecvf.com/content_cvpr_2018/CameraReady/0205.pdf) (NBT) paper. An implementation of NBT can be found on this [repository](https://github.com/jiasenlu/NeuralBabyTalk).

## UnRel dataset captioning instructions

Besides reproducing the paper experiment on the [Flickr30k](http://web.engr.illinois.edu/~bplumme2/Flickr30kEntities/) dataset, our goal for this project is to apply the NBT approach to a dataset of unusual visual relations named [UnRel](https://github.com/jpeyre/unrel).
This requires annotating a set of 115 images from the UnRel dataset.

This is a joint effort undertaken by all the groups that have selected this subject.

The goal is to caption a subset of the UnRel dataset and to produce 3 captions for each image. The captions should be:

1. General description focusing on relationships between objects (spatial relationships, actions)
2. Caption focusing on the attributes (color, pose, behavior) of the subject.
3. Most salient spatial relationship.

## Using NBT to produce captions on the UnRel dataset

This section focuses on how to adapt the existing NBT code to be able to produce captions on the subset of annotated UnRel images.
Note that to properly function, NBT needs a vision model to output region proposals alongside the detected category, a vocabulary (*textual* words) and a set of *visual* words, as well as the ground truth captions to evaluate the captioning task.

In this experiment, I used the ground truth proposals available in the UnRel dataset. I then used Flickr30k vocabulary and created a manual mapping for UnRel categories that were missing in the Flickr30k dataset.

I was able to reverse-engineer most of the steps required to produce the intermediate files used by the model to generate sentences. It includes:

* Extracting the ground truth proposals from UnRel using the ``annotations.mat`` file.
* Manually map missing categories in Flickr30k that are present in UnRel ground truth detections.
* Reformat the proposals so that they exhibit, for each proposal: ``(x_min, y_min, x_max, y_max, detection_index, confidence)``
* Produce a ``dataset_unrel.json`` file similar to ``dataset_flickr30k.json`` file to gather the captions and images data.
* Produce a ``cap_unrel.json`` similar to ``cap_coco.json`` file to make the ground truth captions available.
* Produce a ``dic_unrel.json`` based on ``dic_flickr30k.json`` to provide the vocabulary to the language model.
* Refactor the original code from ``demo.py`` to ``demo_unrel.py`` to be able to run the demonstration on the UnRel dataset.
* Refactor the original code from ``dataloader_flickr.py`` to ``dataloader_unrel.py`` to be able to load the UnRel dataset so that it can be fed to the NBT model as expected.
* Refactor the original code from ``main.py`` to ``eval_unrel.py`` so that the language evaluation can be performed on the UnRel dataset.
* Refactor the original configuration file ``cfgs/normal_coco_res101.yml`` to ``cfgs/normal_unrel_res101.yml``. I also provide the missing ``cfgs/normal_flickr30k_res101.yml`` in this repository.
* Produce a ``caption_unrel.json`` file similar to ``caption_flickr30k.json`` in ``tools/coco-caption/annotations/`` for the language evaluation to be performed on the UnRel dataset.

## Results on the UnRel dataset

* We provide the results in the ``visu`` folder.
* Results table can be found in the ``report`` folder.


