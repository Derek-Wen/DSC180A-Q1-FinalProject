# Streetwatch: Utility and Wildfire Risks Detected From Street View Imagery

San Diego Gas & Electric leverages many different public and private data sources to make critical decisions that impact our communities. We would like to explore Google Street View as a publicly available source of data to help us identify risks that can be observed from the perspective of San Diego citizens. The project goals are to quantify the ability to observe damaged assets or fire from commonly traveled paths, determine whether there are clear compliance infractions that can be seen from the citizen's perspective, and identify other utility-related hazards that can be seen from this public data source.
 
## Data Sources
Data for this project is collected from [Google Street View Static API](https://developers.google.com/maps/documentation/streetview/overview). 

To run sunny.py, you need specifically structured JSON file. The JSON file will have 2 main item(OH and UG) and each should be the list of 5 different pole and within each pole, there should be 'loc' for lat and long 'heading' for heading direction of the image.

### Additional Files
The files below are needed in order to run `scripts/collect_images.py`:
* `joshua_structures.json`
* `kevin_structures.json`
* `jonathan_structures.json`
* `structure_coordinates.json`

However, files needed have already been added to the repository.

## Setup

### Conda Environment
After cloning repo, navigating to root level and run:
```
conda env create -f environment.yml
```

### Credentials
You will need a Google Maps API key and a Google Secret Key to store in "API_KEY" and "SECRET" respectively in `.env`. Store credentials in `.env` file and load using [python-dotenv](https://pypi.org/project/python-dotenv/).

### Training Data
Create training data by running the following after setup is complete:
```
python scripts/collect_images.py
```

# DETR (Detection Transformer) Model
A [DETR model](https://github.com/woctezuma/finetune-detr) was modified to fit our data set and image labeling needs.

[Google Colab is recommended and should be copied and saved in your personal drive.](https://colab.research.google.com/drive/1GikatFXOZD20bXc-qNZIvU0uGiuBNrh9?usp=sharing)

After running all of the cells before the section **"Check the dataset after it was pre-processed for fine-tuning"**, we expect the DETR directory structure to be the following:
```
path/to/coco/data/poles/
├ annotations/  # JSON annotations
│  ├ annotations/custom_train.json
│  └ annotations/custom_val.json
├ train2017/    # training images
└ val2017/      # validation images
```
The files `custom_train.json`, `custom_val.json`, and all of the training and validations images are in the data folder. You will have to add these files into the DETR directory structure.

In summary, run all of the cells before the section **"Check the dataset after it was pre-processed for fine-tuning"**. Afterwards, add in `custom_train.json` and `custom_val.json` in the **annotations**, training images in **train2017**, and validation images in **val2017**. Run the rest of the cells once you have added the necessary files

# Project Structure

```
├── data/               <- Local data files only
│
├── notebooks/          <- Jupyter notebooks
│
├── scripts/            <- Python scripts to run in command line
│
├── .env                <- Environment variables for the project
│
├── .gitignore          <- Git ignore file
│
├── environment.yml     <- Conda environment file
│
└── README.md           <- The top-level README for repo
```
