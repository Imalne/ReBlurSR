# Usage Instruction For ReBlurSR Dataset 

## Dataset Using

### Generate ReBlurSR-Train and ReBlurSR-Test
1. Download the dataset files from the [Google Drive](https://drive.google.com/file/d/1mkjSd95VxWr63GBbfpmy9ImlweChorf0/view?usp=sharing)
2. Unzip the files to the corresponding folders. The structure tree of the unzipped folders is as follows:
    ```
    .
    ├── ALL_HR
    |── ALL_mask
    |── valid
    |   ├── defocus
    |   |   ├── LR
    |   |   |   └── X4
    |   └── motion
    |       ├── LR
    |       |   └── X4
    |── area_class.npy
    |── degree_class.npy
    |── defocus_motion_class.npy
    |── train_validation.npy
    └── train_validation_split.py
    ```
    File description for the unzipped folder:
    * `README.md`: This file.
    * `ALL_HR`: The high-resolution images of the ReBlurSR dataset, including the ReBlurSR-Train and ReBlurSR-Test subsets.
    * `ALL_mask`: The blur map for the HR images in `ALL_HR`. For each sample, the blur map value is `0(0)` if the pixel is blurred, and `1(255)` if the pixel is non-blurred.
    * `valid`: contains the LR versions of the ReBlurSR-Test subset. `defocus` and `motion` subfolders contain the defocus and motion subsubsets of the ReBlurSR-Test subset, respectively. Its structure tree is as follows:
        ```
        valid
        ├── defocus
        │   ├── LR
        │   │   └── X4
        └── motion
            └── LR
               └── X4
        ```
    * `area_class.npy`: The category of the area of the blur region in the ReBlurSR-Test subset. Samples are divided into 3 classes: small, medium, and large.
        ```
            0:"large",      1:"medium",     2:"small
        ```
    * `degree_class.npy`: The category of the degree of the blur region in the ReBlurSR-Test subset. Samples are divided into 3 classes: heavy, little, and middle.
        ```
            0:"heavy",      1:"little",     2:"middle"
        ```
    * `defocus_motion_class.npy`: The category of the blur type in the ReBlurSR-Test subset. Samples are divided into 2 classes: defocus and motion.
        ```
            0:"defocus",    1:"motion"
        ```
    * `train_validation.npy`: The category of the samples in the ReBlurSR-Train and ReBlurSR-Test subsets. Samples are divided into 2 classes: train and validation.
        ```
            0:"train",      1:"validation"
        ```

    * `train_validation_split.py`: The script to generate the ReBlurSR-Train and ReBlurSR-Test subsets from `ALL_HR` and `ALL_mask` folders according to the `defocus_motion_class.npy` and `train_validation.npy` files.
3. run the `train_validation_split.py` script to generate the ReBlurSR-Train and ReBlurSR-Test subsets.
    ```bash
    python train_validation_split.py # required packages: numpy, tqdm
    ```
4. The generated ReBlurSR-Train and ReBlurSR-Test subsets are saved in the `train` and `valid` folders, respectively. The structure tree of the complete `train` folder and `valid` folder are as follows:
    ```
    train
    ├── motion
    │   ├── HR
    │   └── mask
    └── defocus
        ├── HR
        └── mask

    valid
    ├── motion
    │   ├── HR
    │   ├── LR
    |   |   └── X4
    │   └── mask
    └── defocus
        ├── HR
        ├── LR
        |   └── X4
        └── mask
    ```

### Generate the subsets of the ReBlurSR-Test
You can generate the subsets of the ReBlurSR-Test according to the `area_class.npy`, `degree_class.npy`, and `defocus_motion_class.npy` files.
