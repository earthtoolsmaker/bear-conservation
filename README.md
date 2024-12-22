# AI for Bears

It contains a collection of software packages to work with bears.

<img src="./docs/development/assets/images/model_output/facedetection/image1.jpg" width="250" alt="Detected bear face using the bear face detector" /> <img src="./docs/development/assets/images/model_output/pose/image1.jpg" width="250" alt="Pose of a bear using the bearfacelandmarkdetector" /> <img src="./docs/development/assets/images/model_output/facesegmentation/image1.jpg" width="250" alt="Segmented face of a bear" />

It provides bear detection, bear face detection, bear face segmentation, bear
facial landmark detection and bear re-identification models.

[<img src="./docs/assets/images/ml_space.png" />](https://www.earthtoolsmaker.org/spaces/bear_identification/)

## Context

Bears, particularly brown bears, are not only charismatic but also serve as
indicator and umbrella species. By understanding and protecting them, we
contribute to the overall health of the environment. However, monitoring bears
is difficult due to their elusive and wide-ranging nature. The toolbox of
methods available to study bears in non-invasive ways is limited, leading to a
reduced understanding of their population status and trends.

Human-bear conflicts can pose challenges to effective bear conservation and
threats to people and property. Promoting coexistence and mitigating human-bear
conflicts is key to the long-term conservation of brown bears, preserving the
vital role they play in maintaining a balanced ecosystem.

## Setup

### git-lfs

Make sure [`git-lfs`](https://git-lfs.com/) is installed on your system.

Run the following command to check:

```sh
git lfs install
```

If not installed, one can install it with the following:

#### Linux

```sh
sudo apt install git-lfs
git-lfs install
```

#### Mac

```sh
brew install git-lfs
git-lfs install
```

#### Windows

Download and run the latest [windows installer](https://github.com/git-lfs/git-lfs/releases).

## Detect bears

Binary classifier to detect bears from camera trap frames (nighttime and daytime).

| Normalized Confusion Matrix | Training Metrics | Precision/Recall |
|:---------------------------:|:----------------:|:----------------:|
| ![Normalized Confusion Matrix](./reports/beardetection/best_upsample_imgsz_640/evaluation/confusion_matrix_normalized.png) | ![Training](./reports/beardetection/best_upsample_imgsz_640/training/results.png) | ![Precision/Recall curve](./reports/beardetection/best_upsample_imgsz_640/evaluation/PR_curve.png) |

### beardetection virtualenv

Create a virtualenv using your tool of
choice (eg. conda, pyenv, regular python,
...) and activate it.

```sh
conda create -n beardetection python=3.9
conda activate beardetection
```

### Install the beardetection dependencies

```sh
make beardetection_setup
```

### Install the model

Run the following command to install the model:

```sh
make beardetection_install_model
```

### Detect

![Predictions](./reports/beardetection/best_upsample_imgsz_640/training/val_batch0_pred.jpg)

Use the dummy detection script to check that everything works as expected:

```sh
make beardetection_predict
```

You should be able to find the predictions in the folder
`./data/07_model_output/beardetection/predictions/`

Now you can start predicting on your own images using the following python script:

```sh
python ./scripts/beardetection/model/predict.py \
  --model-weights ./data/06_models/beardetection/model/weights/model.pt \
  --source-path ./data/09_external/detect/images/bears/image1.jpg \
  --save-path ./data/07_model_output/beardetection/predictions/ \
  --loglevel "info"
```

## Identify bears

### Pipeline Overview

![Bear IDentification Pipeline](./docs/development/assets/images/pipeline.png)

### Performance

| Precision at 1 | Precision at 3 | Precision at 5 | Precision at 10 |
|:--------------:|:--------------:|:--------------:|:---------------:|
|           95.5 |           96.5 |           97.3 |            98.5 |

### bearidentification virtualenv

Create a virtualenv using your tool of
choice (eg. conda, pyenv, regular python,
...) and activate it.

```sh
conda create -n bearidentification python=3.9
conda activate bearidentification
```

### Install the bearidentification dependencies

```sh
make bearidentification_setup
```

### Install the packaged pipeline

Run the following command to install the pipeline:

```sh
make install_packaged_pipeline
```

### Predict

Use the dummy prediction script to check that everyhing works as expected:

```sh
make identify_default
```

You should be able to find the predictions in the folder
`./data/07_model_output/identify/default/`.

Now you can start predicting on your own images using the following python script:

```sh
python ./scripts/identify.py \
  --source-path ./data/09_external/identify/P1250243.JPG \
  --output-dir ./data/07_model_output/identify/default/
```

<img src="./docs/development/assets/images/model_output/identification/prediction_at_5_individuals_5_samples_per_individual.png" alt="Identification of a bear" width="550px" />

## Development

To contribute to this repository, one can follow the [relevant
documentation](./docs/development/README.md).

## Partnerships

This project was hosted and made possible by the following organizations:

- [FruitpunchAI](https://app.fruitpunch.ai/challenge/ai-for-bears)
- [The BearID Project](https://bearresearch.org/)
- [HackThePlanet](https://www.hack-the-planet.io/)

## Literature

- [Circle Loss](./references/litterature/papers/circle_loss.pdf)
- [Dolphin ID](./references/litterature/papers/dolphin_id.pdf)
- [FaceNet](./references/litterature/papers/facenet.pdf)
- [DataAugmentation with pseudo infrared vision](./references/litterature/papers/data-augmentation-with-pseudo-infrared-night-vision.pdf)
- [Automated Facial Recognition For Wildlife that lacks unique markings](./references/litterature/papers/Ecology_and_Evolution_2020_Clapham_Automated_facial_recognition_for_wildlife_that_lack_unique_markings.pdf)
- [Multispecies Facial Detection For Indiviual Identification](./references/litterature/papers/multispeciesfacialdetectionforindividualidentification.pdf)
- [Wildlife Dataset Re-ID](./references/litterature/papers/wildlifedatasetreid.pdf)
- [The Animal ID problem](./references/litterature/papers/theanimalidproblem.pdf)
- [ArcFace: Additive Angular Margin Loss for Deep Face Recognition](./references/litterature/papers/arcface.pdf)
