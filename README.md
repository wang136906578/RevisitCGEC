# Revisiting the Evaluation for Chinese Grammatical Error Correction
Data for the paper Revisiting the Evaluation for Chinese Grammatical Error Correction.

# How to use
## Prepare the data
```system corrections``` contains the output from each system. 

Source sentences and references can be extracted from [YACLC](https://github.com/blcuicall/CCL2022-CLTC/tree/main/datasets/track3/dev) and [MuCGEC](https://github.com/HillZhang1999/MuCGEC/blob/main/data/MuCGEC/MuCGEC_dev.txt) using the ids provided in ```sentence ids```.

```judgments.xml``` contains the human rankings.
## Acquire human rankings
Download the scripts from https://github.com/grammatical/evaluation/ .

Replace the ```data/judgments.xml``` with ours.

To generate the statistic data and human rankings showed in our paper, you can use following command.

```
cd data
make -j 8 trueskill
```

## Acquire Automatic metric scores
### ChERRANT (M^2 score)
Download scripts from https://github.com/HillZhang1999/MuCGEC/tree/main/scorers/ChERRANT .

Convert the parallel files into M^2 format. You need to do this for source-system and source-reference pairs.
```
python parallel_to_m2.py -f /para/files/path -o /output/m2/path -g <choose char or word> -m
```
Evaluate.
```
python compare_m2_for_evaluation.py -hyp /sys/m2/path -ref /ref/m2/path
```
### GLEU
Download scripts from https://github.com/keisks/jfleg/tree/master/eval .

Evaluate.
```
python gleu.py --src /src/path --hyp /sys/path --ref /ref/path
```
### PT-M2
Download scripts from https://github.com/pygongnlp/PT-M2/ .

Evaluate.
```
python evaluate.py --base m2 --scorer bertscore \
--model_type bert-base-chinese \
--source /src/path --hypothesis /sys/path \
--reference /ref/path --output /output/path
```
