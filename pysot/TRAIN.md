# PySOT Training Tutorial

This implements training of SiamRPN with backbone architectures, such as ResNet, AlexNet.
### Add PySOT to your PYTHONPATH
```bash
export PYTHONPATH=/path/to/pysot:$PYTHONPATH
```

## Prepare training dataset
Prepare training dataset, detailed preparations are listed in [training_dataset](training_dataset) directory.
* [VID]([https://xdshang.github.io/docs/imagenet-vidvrd.html#:~:text=Useful%20downloading%20links,evaluation%20codes])

## Training

To train a model (SiamRPN++), run `train.py` with the desired configs:

```bash
cd experiments/siamrpn_r50_l234_dwxcorr_8gpu
```
```bash
python ../../tools/train.py --config config.yaml
```


## Testing
After training, you can test snapshots on VOT dataset.
For `AlexNet`, you need to test snapshots from 35 to 50 epoch. 
For `ResNet`, you need to test snapshots from 10 to 20 epoch.

```bash 
START=10
END=20
seq $START 1 $END | \
    xargs -I {} echo "snapshot/checkpoint_e{}.pth" | \
    xargs -I {} \ 
    python -u ../../tools/test.py \
        --snapshot {} \
	--config config.yaml \
	--dataset VOT2018 2>&1 | tee logs/test_dataset.log
```

## Evaluation
```
python ../../tools/eval.py 	 \
	--tracker_path ./results \ # result path
	--dataset VOT2018        \ # dataset name
	--num 4 		 \ # number thread to eval
	--tracker_prefix 'ch*'   # tracker_name
```
