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

results/ast-track1-%-covered.sys: onmt-data/ast-track1-src-%.txt.nbest.out
	cat $^ | python3 scripts/get-analyses.py 0.8 3 $*/ast-covered > $@

results/ast-track2-%-covered.sys: onmt-data/ast-track2-src-%.txt.nbest.out
	cat $^ | python3 scripts/get-analyses.py 0.7 3 $*/ast-covered > $@

results/ast-track3-%-covered.sys: onmt-data/ast-track3-src-%.txt.nbest.out
	cat $^ | python3 scripts/get-analyses.py 0.6 2 $*/ast-covered > $@

results/crh-track1-%-covered.sys: onmt-data/crh-track1-src-%.txt.nbest.out
	cat $^ | python3 scripts/get-analyses.py 0.9 4 $*/crh-covered > $@

results/crh-track2-%-covered.sys: onmt-data/crh-track2-src-%.txt.nbest.out
	cat $^ | python3 scripts/get-analyses.py 0.6 2 $*/crh-covered > $@

results/crh-track3-%-covered.sys: onmt-data/crh-track3-src-%.txt.nbest.out
	cat $^ | python3 scripts/get-analyses.py 0.1 1 $*/crh-covered > $@

