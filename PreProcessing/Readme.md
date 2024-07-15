### Preprocessing for Brain MRI

#### Install FSL

``python fslinstaller.py --dest /share/data_rechenknecht 03_2/students/vierkant/FSL --no_env --skip_registration``

You can use other directories. Don't forget `--no_env`! Already installed on IMI machines

#### Install nppy

Make an python 3.8 environment and install NPPY from https://github.com/Novestars/Neural_Pre_Processing .

<code>
conda create -n NeuralPreprocessing python=3.8

cd nppy

pip install -e .
</code>

You can use the environment `NeuralPreprocessing` on IMI machines.

#### Prepare input data

Input data are assumed to have four nifti images:
`<data-dir>/<patient-id>/<patient-id>_[t1|t1c|t2|flair].nii.gz`

For example:
<code>
./data/Pat_3_preop/Pat_3_preop_flair.nii.gz
./data/Pat_3_preop/Pat_3_preop_t1c.nii.gz
./data/Pat_3_preop/Pat_3_preop_t1.nii.gz
./data/Pat_3_preop/Pat_3_preop_t2.nii.gz`
</code>

Setup data-dir in `brainpp_config.py`

#### Run script

`python main.py -p Pat_5_preop`

Run-time is 5 - 10 minutes.
