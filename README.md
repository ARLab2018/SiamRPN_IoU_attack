# SiamRPN_IoU_attack



## Introduction

<img src="https://github.com/VISION-SJTU/IoUattack/blob/main/demo/intro.png" width='500'/><br/>

We observe that the increase of noise level positively correlates to the decrease of IoU scores, but their directions are not exactly the same.
- The IoU attack seeks to inject the lowest amount of noisy perturbations at the same contour line of IoU score for each iteration.
- We chose **SiamRPN++** as the representative tracker.
- To enhance the original IoU attack we introduced dynamic Lambda adjustment which adaptively balances the spatial and temporal components of the IoU
during the attack.
- To generate perturbation we used gradient based optimization, instead solely relying on random sampling.
  
## Results

 #### Result for IoU Attack on SiamRPN++ on VOT2018 Dataset with multiple model iterations
|                   | Original Model  |  0.01 Weight Decay  | 0.001 Weight Decay | 32 Anchors | 96 Anchors | Color OFF | Blur ON |
| ------------------| :------------:  | :---------------:   |:----------------:  |:--------:  |:---------: |:--------: |:-----:  |
| Accuracy          | 0.661           | 0.336               | 0.278              | 0.306      | 0.308      | 0.303     | 0.285   |
| Robustness        | 1.370           | 1.182               | 1.397              | 1.290      | 1.424      | 1.316     | 2.892   |
| EAO               | 0.131           | 0.103               | 0.079              | 0.090      | 0.087      | 0.077     | 0.037   |
 

## Code
:herb: **The code of IoU attack for SiamRPN++ is released!!**
- You should put the datasets into ```pysot/testing_dataset``` folder.
- Please download the pretrained model and set the environments of SiamPRN++.
- See [SiamRPN++](https://github.com/STVIR/pysot) for more details.

Test the original performance on VOT2018 dataset, please use the following command.
```
cd pysot/experiments/siamrpn_r50_l234_dwxcorr
python -u ../../tools/test_original.py 	\
	--snapshot model.pth 	\ # model path
	--dataset VOT2018 	\ # dataset name
	--config config.yaml	  # config file
```
Test IoU attack on VOT2018 dataset, please use the following command.
```
cd pysot/experiments/siamrpn_r50_l234_dwxcorr
python -u ../../tools/test_IoU_attack.py 	\
	--snapshot model.pth 	\ # model path
	--dataset VOT2018 	\ # dataset name
	--config config.yaml	  # config file
```

For the adversarial attack of other datasets, you should change the dataset name as mentioned above.

## Demo

<img src="https://github.com/VISION-SJTU/IoUattack/blob/main/demo/car_clean.gif" width='300'/>   <img src="https://github.com/VISION-SJTU/IoUattack/blob/main/demo/car_attack.gif" width='300'/><br/>
&emsp; &emsp;&emsp;&emsp;&emsp;&emsp; <img src="https://github.com/VISION-SJTU/IoUattack/blob/main/demo/legend.png" width='300'/><br/>


## Citation
If any part of our paper and code is helpful to your work, please generously citing: 
```
@inproceedings{jia-cvpr21-iouattack,
  title={IoU Attack: Towards Temporally Coherent Black-Box Adversarial Attack for Visual Object Tracking},
  author={Jia, Shuai and Song, Yibing and Ma, Chao and Yang, Xiaokang},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  year={2021}
}
```

Thank you :)

## Reference
We choose three representative trackers, SiamRPN++, DiMP and LTMU. 
The original code of these trackers are list as follows:
- SiamRPN++: https://github.com/STVIR/pysot
- DiMP: https://github.com/visionml/pytracking
- LTMU: https://github.com/Daikenan/LTMU

We also refer to the code of Boundary Attack for IoU attack.
- Boundary Attack: https://github.com/greentfrapp/boundary-attack

Thanks for their wonderful works!

## License
Licensed under an MIT license.
