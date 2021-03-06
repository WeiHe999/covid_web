# edm_condo_v2

## edm_condo_v2 models

### Description

* Trained with Zillow ground-truth data, KNN table is edm_v4.knn_base 
* edm_v4 training job names:
```
{'numberofbaths':       'edm-TrainCatA1V3-numberofbat01',
 'foundationtype':      'edm-TrainCatA1V3-foundationt01',
 'finishedbasement':    'edm-TrainCatA1V3-finishedbas01',
 'rooftype':            'edm-TrainCatA1-rooftype-31',
 'numberofstoreys':     'edm-TrainB5-numberofstoreys-17',
 'exteriorwalltype':    'edm-TrainB5-exteriorwalltype17',
 'garagetype':          'edm-TrainA6-garagetype-44',
 'architecturalstyle':  'edm-TrainA6-architecturalsty44',
 'yearbuilt':           'edm-TrainNumA1-yearbuilt-41',
 'totalfloorarea':      'edm-TrainNumA1-totalfloorare41'}
```
* edm_v4 step-function training job-keys:
```
{'numberofbaths':      'TrainCatA1V3',
 'foundationtype':     'TrainCatA1V3',
 'finishedbasement':   'TrainCatA1V3',
 'rooftype':           'TrainCatA1',
 'numberofstoreys':    'TrainB5',
 'exteriorwalltype':   'TrainB5',
 'garagetype':         'TrainA6',
 'architecturalstyle': 'TrainA6',
 'yearbuilt':          'TrainNumA1',
 'totalfloorarea':     'TrainNumA1'}
```
* edm_v4 models are used to score national datalake
* URL for edm_v4 model dict:
```
s3://rnd-sagemaker-model-artifacts-dev/model_dict/edm_v4/dict_config.pickle
```

### Re-train:
* Step function inputs:
``` 
{
  "job_key": "TrainCatK1",
  "task": "training",
  "targets": "numberofbaths, foundationtype, finishedbasement, rooftype",
  "bucket": "rnd-edm-v4-dev"
}
{
  "job_key": "TrainNumK1",
  "task": "training",
  "targets": "yearbuilt, totalfloorarea",
  "bucket": "rnd-edm-v4-dev"
}
{
  "job_key": "TrainCatK2",
  "task": "training",
  "targets": "numberofstoreys, exteriorwalltype, architecturalstyle, garagetype",
  "bucket": "rnd-edm-v4-dev"
}
```

### Batch transform for test set evaluation or datalake scoring:
* Step function inputs:
```
# Test set evaluation
{
  "job_key": "EvalTrainCatA1V3PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "numberofbaths, foundationtype, finishedbasement",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainCatA1V3"
}
{
  "job_key": "EvalTrainCatA1PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "rooftype",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainCatA1"
}
{
  "job_key": "EvalTrainB5PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "numberofstoreys, exteriorwalltype",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainB5"
}
{
  "job_key": "EvalTrainA6PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "garagetype, architecturalstyle",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainA6"
}
{
  "job_key": "EvalTrainNumA1PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "yearbuilt, totalfloorarea",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainNumA1"
}
```
* For datalake scoring, set **test_data_key** to: datalake/data/df_1.csv, datalake/data/df_2.csv, datalake/data/df_3.csv, datalake/data/df_4.csv, datalake/data/df_5.csv, respectively.

### Base data:
* Step function input:
```
{
  "job_key": "Base202202",
  "task": "base_data",
  "bucket": "rnd-edm-v4-dev"
}
```


## edm_mpac_v4 models

### Description

* Trained with Zillow and MPAC ground-truth data, KNN table is edm_v4.knn_base_v2 
* edm_mpac_v4 training job names:
```
{'numberofbaths':      'edm-TrainR2Cat2B-numberofbat40',
 'foundationtype':     'edm-TrainR2Cat2B-foundationt40',
 'finishedbasement':   'edm-TrainR2Cat2B-finishedbas40',
 'rooftype':           'edm-TrainR2Cat2B-rooftype-40',
 'numberofstoreys':    'edm-TrainR2Cat2A-numberofsto26',
 'exteriorwalltype':   'edm-TrainR2Cat2A-exteriorwal26',
 'garagetype':         'edm-TrainR2Cat2A-garagetype-26',
 'architecturalstyle': 'edm-TrainR2Cat2A-architectur26',
 'yearbuilt':          'edm-TrainR2Num3-yearbuilt-08',
 'totalfloorarea':     'edm-TrainR2Num3-totalfloorar08'}
```
* edm_mpac_v4 step-function training job-keys:
```
{'numberofbaths':       'TrainR2Cat2B',
 'foundationtype':      'TrainR2Cat2B',
 'finishedbasement':    'TrainR2Cat2B',
 'rooftype':            'TrainR2Cat2B',
 'numberofstoreys':     'TrainR2Cat2A',
 'exteriorwalltype':    'TrainR2Cat2A',
 'garagetype':          'TrainR2Cat2A',
 'architecturalstyle':  'TrainR2Cat2A',
 'yearbuilt':           'TrainR2Num3',
 'totalfloorarea':      'TrainR2Num3'}
```
* edm_mpac_v4 models are used to score **Ontario** datalake
* URL for edm_mpac_v4 model dict:
```
s3://rnd-sagemaker-model-artifacts-dev/model_dict/edm_mpac_v4/dict_config.pickle
```

### Re-train:
* Step function inputs:
``` 
{
  "job_key": "TrainCatM1",
  "task": "training",
  "mpac": 1,
  "targets": "numberofbaths, foundationtype, finishedbasement, rooftype",
  "bucket": "rnd-edm-v4-dev"
}
{
  "job_key": "TrainNumM1",
  "task": "training",
  "mpac": 1,
  "targets": "yearbuilt, totalfloorarea",
  "bucket": "rnd-edm-v4-dev"
}
{
  "job_key": "TrainCatM2",
  "task": "training",
  "mpac": 1,
  "targets": "numberofstoreys, exteriorwalltype, architecturalstyle, garagetype",
  "bucket": "rnd-edm-v4-dev"
}
```

### Batch transform for test set evaluation or datalake scoring:
* Step function inputs:
```
# Test set evaluation
{
  "job_key": "EvalTrainR2Cat2BPV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "numberofbaths, foundationtype, finishedbasement, rooftype",
  "task": "batch_transform",
  "mpac": 1,
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainR2Cat2B"
}
{
  "job_key": "EvalTrainR2Cat2APV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "numberofstoreys, exteriorwalltype, garagetype, architecturalstyle",
  "task": "batch_transform",
  "mpac": 1,
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainR2Cat2A"
}
{
  "job_key": "EvalTrainR2Num3PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "yearbuilt, totalfloorarea",
  "task": "batch_transform",
  "mpac": 1,
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainR2Num3"
}
```
* For datalake scoring, set **test_data_key** to: datalake-ON/data/df_1.csv, datalake-ON/data/df_2.csv, datalake-ON/data/df_3.csv, datalake-ON/data/df_4.csv, datalake-ON/data/df_5.csv, respectively.

### Base data:
* Step function input:
```
{
  "job_key": "BaseM202202",
  "task": "base_data",
  "mpac": 1,
  "bucket": "rnd-edm-v4-dev"
}
```




# training

{
  "job_key": "TrainCat4",
  "task": "training",
  "targets": "numberofbaths, numberofbedrooms, numberofdens, architecturalstyle",
  "bucket": "rnd-edm-condo-v2-dev"
}

{
  "job_key": "TrainNum4",
  "task": "training",
  "targets": "totalfloorarea, yearbuilt, numberofstoreys, floorlevel",
  "bucket": "rnd-edm-condo-v2-dev"
}

# batch-transform
{
  "job_key": "TestCat4",
  "test_data_key": "base_data/TrainCat4/result/df_test_set.csv",
  "targets": "numberofbaths, numberofbedrooms, numberofdens, architecturalstyle",
  "task": "batch_transform",
  "bucket": "rnd-edm-condo-v2-dev",
  "training_job_key": "TrainCat4"
}

{
  "job_key": "TestNum4",
  "test_data_key": "base_data/TrainNum4/result/df_test_set.csv",
  "targets": "totalfloorarea, yearbuilt, numberofstoreys, floorlevel",
  "task": "batch_transform",
  "bucket": "rnd-edm-condo-v2-dev",
  "training_job_key": "TrainNum4"
}



# base data
{
  "job_key": "Base3",
  "task": "base_data",
  "bucket": "rnd-edm-condo-v2-dev"
}
