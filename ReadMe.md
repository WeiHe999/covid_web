## How to run the pipeline?

* Training:
{\
  "job_key": "train-202104v5",\
  "version": "v0",\
  "year_month": 202104,\
  "task": "training",\
  "bucket": "rnd-avm-v2-dev"\
}

* Batch transform:
{\
  "job_key": "EvTfProd202104a31",\
  "version": "v0",\
  "year_month": 202104,\
  "task": "batch_transform",\
  "training_job_key": "TrProd202104a31",\
  "bucket": "rnd-avm-v2-dev",\
  "test_data_key": "avm2.5/production/monthly-evaluation/202104-prov-models/df_sales.csv"\
}

* Base data:
{\
  "job_key": "base-202105v7",\
  "year_month": 202105,\
  "task": "base_data",\
  "bucket": "rnd-avm-v2-dev"\
}

Note: the value for "version" must be the same as the variable **experiment_version** defined in terraform.





