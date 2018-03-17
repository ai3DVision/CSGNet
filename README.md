# CSGNet: Neural Shape Parser for Constructive Solid Geometry
This repository contains code accompaning the paper: [CSGNet: Neural Shape Parser for Constructive Solid Geometry, CVPR 2018](https://arxiv.org/abs/1712.08290).

Here we only include the code for 2D CSGNet. Code for 3D is very similar to 2D and is coming soon.

![](image.png)
### Dependency
- Python 3.*
- Pytorch 0.1.2 or Pytorch 0.3

### Data
- Synthetic Dataset:

    Dataset is provided in the form of program expressions, instead of rendered images. Images for training, validation and testing are rendered on the fly. The dataset is split in different program lengths.
    ```bash
    tar -zxvf data/synthetic.tar.gz -C data/
    ```

- CAD Dataset

    Dataset is provided in H5Py format. Do this before using in the directory `data/cad/cad.h5`.

### Supervised Learning
- To train, update `config_synthetic.yml` with required arguments. Default arguments are already filled. Then run:
    ```python
    python train_synthetic.py
    ```

- To test, update `config_synthetic.yml` with required arguments. Default arguments are already filled. Then run:
    ```python
    # For top-1 testing
    python test_synthetic.py
    ```
    ```python
    # For beam-search-k testing
    python test_synthetic_beamsearch.py
    ```

### RL fintuning
- To train a network using RL, fill up configuration in `config_cad.yml` or keep the default values and then run:
    ```python
    python train_cad.py
    ```
    Make sure that you have trained a network used Supervised setting first.

- To test the network trained using RL, fill up configuration in `config_cad.yml` or keep the default values and then run:
  ```python
  # for top-1 decoding
  python test_cad.py
  ```
  ```python
  # beam search decoding
  python test_cad_beamsearch.py
  ```
  For post processing optmization of program expressions (visually guided search), set the flag `REFINE=True` in the script `test_cad_beam_search.py`, although it is little slow. For saving visualization of beam search use `SAVE_VIZ=True`

- To optmize some expressions for cad dataset:
  ```
  # To optmize program expressions from top-1 prediction
  python refine_cad.py path/to/exp/to/optmize/exp.txt  path/to/directory/to/save/exp/
  ```
  Note that the expression files here should only have 3k expressions corresponding to the 3k test examples from the CAD dataset.

- To optmize program expressions from top-1 prediction
  ```
  python refine_cad_beamsearch.py path/to/exp/to/optmize/exp.txt  path/to/directory/to/save/exp/
  ```
  Note that the expression files here should only have 3k x beam_width expressions corresponding to the 3k test examples from the CAD dataset.


### Contact
To ask questions, please [email](mailto:gopalsharma@cs.umass.edu).