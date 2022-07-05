```bash

$ git init 

$ dvc init

$ dvc remote add -d storage gdrive://1xYp213LgSCn81q4lx_ZPuZkf0J8fYZ4Y

$ dvc add data/prepared/train.csv data/prepared/test.csv

$ dvc run -n featurize -d src/featurize.py -d data/prepared -o data/features python src/featurize.py data/prepared data/features

$ dvc run -n train -p train.alpha -d src/train.py -d data/features -o model.pkl python src/train.py data/features model.pkl

$ dvc run -n evaluate -d src/evaluate.py -d model.pkl -d data/features --metrics scores.json --plots plots.json python src/evaluate.py model.pkl data/features scores.json plots.json

$ dvc metrics show

$ dvc dag

$ dvc repro

$ git add .

$ git commit -m " "

$ dvc push

$ git push

$ dvc params diff

$ dvc metrics diff

$ dvc plots show -y precision -x recall plots.json

$ dvc plots diff --targets plots.json -y precision
```
