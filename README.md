# code2seq
This is a fork (with some adjustments) of the code2seq implementation (https://github.com/tech-srl/code2seq).

## Requirements
```pip install -r requirements.txt```

## Basic Setup
### Cloning this repository
```
git clone https://github.com/philmon2/code2seq.git
cd code2seq
```

### Retrieve the raw java dataset
```
mkdir data
cd data
```
* For Java-small, `wget https://s3.amazonaws.com/code2seq/datasets/java-small.tar.gz`
* For Java-med, `wget https://s3.amazonaws.com/code2seq/datasets/java-med.tar.gz`
* For Java-large, `wget https://s3.amazonaws.com/code2seq/datasets/java-large.tar.gz`

Then unpack your dataset with `tar -xvzf [name_of_file.tar.gz]`


### Preprocess the raw Java dataset
  * Edit the file [preprocess.sh](preprocess.sh) using the instructions there, pointing it to the correct training, validation and test directories.
  * Run the preprocess.sh file: `bash preprocess.sh`


### Retrieve trained model (137 MB)
```
wget https://s3.amazonaws.com/code2seq/model/java-large/java-large-model.tar.gz
tar -xvzf java-large-model.tar.gz
```

### Evaluating a trained model
```
python3 code2seq.py --load models/java-large-model/model_iter52.release --test data/java-large/java-large.test.c2s
```
While evaluating, a file named "log.txt" is written to the same directory as the saved model, with each test example name and the model's prediction.

Note that the `load` option takes the file path of the pre-trained model as its argument, and the `test` option takes the file path of the pre-processed test dataset.
