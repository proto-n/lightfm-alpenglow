# lightfm-alpenglow

# This description is under construction

# LightFM evaluation with Alpenglow

[Alpenglow](https://github.com/rpalovics/Alpenglow) makes it possible to evaluate recommender models in an online setting. This repository contains an example of connecting Alpenglow's evaluation with [LightFM](https://github.com/lyst/lightfm).

## How to run
```bash
git clone https://github.com/proto-n/lightfm-alpenglow.git
cd lightfm-alpenglow
mkdir batches
python prepare_data.py
python run_lightfm.py
```

At this point, you can open the notebook `evaluate.ipynb` to evaluate the results.

## Implementation details

The simplest way of evaluating external batch models with Alpenglow is through the [ExternalModelExperiment](...) interface of Alpenglow's API. This experiment has two modes of operation -- one is "write", which writes the training data to disk, and the other is "read", which reads the predictions made by the external model and evaluates them.

This experiment runs in 3 phases:
- The first one, `prepare_data.py` prepares the experiment by running `ExternalModelExperiment` in write mode. This writes train files and the list of corresponding test users who need toplists in the next time period.
- The second one, `run_lightfm.py` runs LightFM model, preparing the toplists for evaluation.
- Finally, the results are evaluated in `evaluate.ipynb`, once again using `ExternalModelExperiment`, this time in read mode.
