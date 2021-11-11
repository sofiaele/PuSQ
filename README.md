# PuSQ 
A Public Speaking Quality dataset for assessing the speaker's skills.

In order to use this dataset among with the openly provided ML framework, follow the quickstart guide. 

## Quickstart 

1. Clone the current repo
```git clone https://github.com/sofiaele/PuSQ.git```

2. Unzip the dataset
```unzip features_data.zip```

3. Clone the repo of the ML framework
``` git clone https://github.com/tyiannak/readys.git ```
Move the contents of the PusQ repo into the 'annotation_agreement' folder of the readys repo. 

4. Aggregate the annotations

    Example:

    ```python3 aggregate_annotations.py -c 1 -a 3 -t 1 -g 1 -mh 4.0 -ml 2.0 -ea annotator8```

      This command will aggregate the annotations of class 1 (expressive) with the following settings:

      - minimum number of annotators = 3
      - type of aggregation = averaging
      - gender = female
      - low mean threshold = 2.0
      - high mean threshold = 4.0
      - exclude annotator8 (because of his high average disagreement for the specific task) 

      For more information about aggregation procedure, follow the instructions at readys/annotation_agreement/.

5. Parse the data into class folders: 
```python3 dataset_parser.py -n expressive_female -aa aggregated_Class1female.csv -i features_data```

6. Train recording-level classifier with the previous parsed data 
```python3 models/train_recording_level_classifier.py -i annotation_agreement/datasets/expressive_female/ -mn test_model -f```

    Note: the specs of this classifier are defined in the 'models/config.yaml'.

7. Test an input (predict) 
```python3 models/test_recording_level.py -i annotation_agreement/datasets/expressive_female/negative/1_speaker27_female_MetaAudio.npz -m models/output_models/recording_level/test_model_MA.pt -m2 models/output_models/recording_level/test_model_LLA.pt```
