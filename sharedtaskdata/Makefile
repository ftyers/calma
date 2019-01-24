ONMTPREPROCESS=~/OpenNMT-py/preprocess.py

onmt-data/%-track1-src-train.txt: train/%-uncovered
	python3 scripts/generate_onmt_data.py $* 1
	python3 scripts/generate_onmt_data.py $* 2

onmt-data/%.train.1.pt: onmt-data/%-src-train.txt
	python3 $(ONMTPREPROCESS) -train_src $< -train_tgt onmt-data/$*-tgt-train.txt \
                                  -valid_src onmt-data/$*-src-dev.txt -valid_tgt onmt-data/$*-tgt-dev.txt \
                                  -save_data onmt-data/$*

train-%:
	sbatch baseline/train-$*.sh

test-%:
	sbatch baseline/test-$*.sh

results/rom-track%-dev-covered.sys: onmt-data/rom-track%-src-dev.txt.nbest.out
	cat $^ | python3 scripts/get-analyses.py 0.6 2 dev/rom-covered > $@

results/tur-track%-dev-covered.sys: onmt-data/tur-track%-src-dev.txt.nbest.out
	cat $^ | python3 scripts/get-analyses.py 0.1 1 dev/tur-covered > $@

