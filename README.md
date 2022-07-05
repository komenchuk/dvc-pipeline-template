git init 

dvc init

dvc remote add -d storage gdrive://1xYp213LgSCn81q4lx_ZPuZkf0J8fYZ4Y

dvc run -n data_preparation -p data_preparation.categories -d src/data_preparation.py -o data/prepared python src/data_preparation.py

dvc dag

dvc repro

dvc run -n featurize -d src/featurize.py -d data/prepared -o data/features python src/featurize.py data/prepared data/features

dvc run -n train -p train.alpha -d src/train.py -d data/features -o model.pkl python src/train.py data/features model.pkl

dvc run -n evaluate -d src/evaluate.py -d model.pkl -d data/features --metrics scores.json --plots plots.json python src/evaluate.py model.pkl data/features scores.json plots.json

git add src/ params.yaml dvc.yaml dvc.lock

git commit -m "experiment 1"

dvc params diff

dvc metrics diff

dvc plots show -y precision -x recall plots.json

