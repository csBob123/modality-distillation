## Code for the paper 'Modality Distillation with Multiple Stream Networks for Action Recognition'. 

[arXiv](https://arxiv.org/abs/1806.07110)

[ECCV 2018](http://openaccess.thecvf.com/content_ECCV_2018/html/Nuno_Garcia_Modality_Distillation_with_ECCV_2018_paper.html)

__ERRATA__ (ECCV paper, Figure 2): first convolutional block of each ResNet unit is 1x1, not 3x3. The [code](https://github.com/pmorerio/admd/blob/39f871dc104cd1923717d09bb00da128248c487e/ActionRecogDatasets/nets/resnet_v1_two_stream.py#L36) is correct. 


If you use this code as part of any published research, please acknowledge the following paper:

    @InProceedings{Garcia_2018_ECCV,
    author = {Garcia, Nuno C. and Morerio, Pietro and Murino, Vittorio},
    title = {Modality Distillation with Multiple Stream Networks for Action Recognition},
    booktitle = {The European Conference on Computer Vision (ECCV)},
    month = {September},
    year = {2018}
    }


###### Data and Imagenet checkpoint directories are defined in utils.py  
###### Arguments are described in utils.py - get_arguments().

###### To read logs
``
cat ./log/uwa3dii/s1_train_depth_01012018_010101__dset_uwa3dii_eval_mode_cross_view/log.txt
``
###### Train Step 1 models, e.g.   

depth: 
``python s1_train_stream.py --dset=ntu --modality=depth --eval=cross_subj  ``

RGB: 
``python s1_train_stream.py --dset=nwucla --modality=rgb  ``

###### Train Step 2 model, e.g.   
Define the right path for depth and rgb checkpoints in ``s2_twostream_depth_rgb.py``
``python s2_twostream_depth_rgb.py --interaction --dset=ntu-mini``

###### Evaluate twostream model, rgb and depth e.g.  
``python s2_twostream_depth_rgb --dset=uwa3dii --just_eval --ckpt=./step2_checkpoint_dir_model.ckpt``

###### Train Hallucination model, e.g.
``python s3_distillation.py --dset=nwucla  --ckpt=./step2_checkpoint_dir_model.ckpt``

###### Train Step 4 model, e.g.
Define the right path for depth (checkpoint from step 3) and rgb (checkpoint from step 2) ckpts in ``s4_depth_hall.py``
``python s4_depth_hall.py --dset=uwa3dii``

###### Evaluate Step 4 model (rgb and hall), e.g.  
``python s4_depth_hall.py --dset=uwa3dii --just_eval --ckpt=./step4_checkpoint_dir_model.ckpt``
