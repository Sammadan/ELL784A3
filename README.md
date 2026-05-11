# ELL784A3
The Repo Contains the Solution for A3 For ELL784


If running locally, download the Soli dataset and update `DATA_ROOT`
in the second cell of the notebook to point to the directory containing
the `.h5` files. Files are expected to follow the naming convention
`{subject_id}_{class_id}_{instance_id}.h5`, with each file containing
four channels (`ch0`, `ch1`, `ch2`, `ch3`) of range-Doppler frames.

## How to run

### Training and evaluation (single fold)

Open `notebook.ipynb` and run all cells in order. The final cell:

1. Loads train and test subjects
2. Trains the GAN for 50 epochs
3. Generates synthetic samples for fine-grained classes
4. Trains the DANN classifier for 80 epochs on the augmented set
5. Evaluates on the held-out subject fold and prints per-class accuracy

The default split is **fold 0**: train on subjects [0,1,2,3,4],
test on subjects [5,6,7,8,9].

#Switching folds for two-fold cross-validation

To run **fold 1**, edit the dataset construction lines:

change 
train_dataset = SoliDataset(DATA_ROOT, subject_ids=[5,6,7,8,9], training=True)
test_dataset  = SoliDataset(DATA_ROOT, subject_ids=[0,1,2,3,4], training=False)


Then re-run the cell. The final reported metric is the mean of the
two folds.

