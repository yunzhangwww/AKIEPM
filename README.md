# AKIEPM
AKIEPM version 0.9.0 <br>
AKIEPM can be used to predict the outcomes of AKI inpatients in 24h, 48h, 72h and 7d. You can train the model separately for different times to make prediction.
This tool is for research purpose and not approved for clinical use.

Dependencies
=
You can install the required dependency library by requirement.txt. (Python 3.7 and TensorFlow 1.15)

Data
=
Patient file format

For a patient, the csv files in the following format are needed for prediction. If value is unknow, you can leave the cell empty. (Please refer to the supplementary materials of the paper for specific data and types. The categorical variables need to be coded discretely.)

p1.csv

|T|Variable 1|	Variable 2|	Variable 3	|……	|Variable N-1| Variable N|
|  ------  | ------- | ------- | ------- | ------- | ------- | ------- |
|t1| | | | | |  |
|t2| | | | | |	|						
|t3| | | | | |	|						

Label file format

For all patients, a csv file in the following format is needed for prediction. (For different time window 24h, 48h, 72h and 7d, label should be corresponding outcome.)

|File Name|Label|
|  ------  | ------- |
|p1.csv|0/1|
|p2.csv|0/1|	
|p3.csv|0/1|	

The patient data should be divided into derivation, internal validation, and external validation cohorts with corresponding label and put them to the directory /data.

Train/Test
=
First, you should set the parameters in main.py, for example, the directory of data, batch_size, epoch, and so on. The mode should be set as “train”. You can set them by command line.

Second, you should set the number of class and input dimension (e.g., num_classes = 2, input_dim = 110) and modify the input dimension in the function of read_single_xlsx() in reader.py.

Third, you should comment the following code in main.py.
```
#val_data_path = os.path.join(args.data,'TrainData1-siwang/7d/val/')
#val_label_path = os.path.join(args.data,'TrainData1-siwang/7dtotalval.csv')
#val_data = data_load2(val_data_path , val_label_path, mode='train')
#random.shuffle(val_data)
```

Finally, you can conduct the train and test process.

Validation
=
First, you should set the parameters in main.py, for example, the directory of data, batch_size, epoch, and so on. The mode should be set as “val”. The load_state should set as the path of trained model. You can set them by command line.

Second, you should set the number of class and input dimension (e.g., num_classes = 2, input_dim = 110) and modify the input dimension in the function of read_single_xlsx() in reader.py.

Third, you should comment the following code in main.py.
```
#train_data_path = os.path.join(args.data,'TrainData1-siwang/7d/train/')
#train_label_path = os.path.join(args.data,'TrainData1-siwang/7dtotaltrain.csv')
#train_data = data_load(train_data_path, train_label_path, mode='train')
#random.shuffle(train_data)

#test_data_path = os.path.join(args.data,'TrainData1-siwang/7d/test/')
#test_label_path = os.path.join(args.data,'TrainData1-siwang/7dtotaltest.csv')
#test_data = data_load2(test_data_path, test_label_path, mode='train')
#random.shuffle(test_data)
```

Finally, you can conduct the validation process.

Evaluation
=
Evaluation code will analyse the prediction results by precision, recall, f-score, accuracy and AUROC.

The trained model and results are stored in output_save_path.
