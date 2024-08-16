# README for GAN Training Script

This repository contains a script for training a Generative Adversarial Network (GAN) to generate images. The GAN is trained on a dataset of images stored in your Google Drive. The script loads the images, preprocesses them, and trains a GAN consisting of a generator and a discriminator. The model can generate images based on a latent space of random noise.

## Requirements

To use this script, you need the following libraries and tools:

- TensorFlow
- NumPy
- Matplotlib
- tqdm
- PIL (Pillow)
- Google Colab (for running the script and accessing Google Drive)

These libraries can be installed using the following command:
```bash
pip install tensorflow numpy matplotlib tqdm pillow
```

## Files

- `gan_training.py`: This is the main script that contains the GAN implementation and training procedure.
- `README.md`: This documentation file.

## How to Use

### Step 1: Mount Google Drive
The script mounts Google Drive to access your image dataset. You must have Google Drive mounted on Colab:
```python
drive.mount('/content/drive')
```

### Step 2: Set the Image Folder
Modify the `IMAGE_FOLDER` variable to point to the folder in Google Drive where your dataset is stored. Example:
```python
IMAGE_FOLDER = '/content/drive/MyDrive/your_image_folder'
```

### Step 3: Set Image Parameters
The default image size is 32x32, with 3 channels (RGB). Modify these values if your dataset has different dimensions:
```python
IMG_HEIGHT = 32
IMG_WIDTH = 32
CHANNELS = 3
```

### Step 4: Load and Preprocess Images
Images are loaded from the specified folder and resized to the target dimensions. The pixel values are normalized to the range [-1, 1] for input to the GAN.

### Step 5: GAN Model Structure
This script builds both the generator and discriminator models:
- The **Generator** takes random noise (latent vector) as input and generates images using transposed convolution layers.
- The **Discriminator** classifies images as real or fake using convolution layers.

### Step 6: Loss Functions and Optimizers
The script uses binary cross-entropy as the loss function for both the generator and discriminator:
- **Generator Loss**: Measures how well the generator fools the discriminator.
- **Discriminator Loss**: Measures how well the discriminator distinguishes between real and fake images.

Both models are optimized using the Adam optimizer.

### Step 7: Training the GAN
The `train` function iterates through the dataset for a given number of epochs:
- A random noise vector is passed through the generator to create fake images.
- The discriminator is trained on both real and fake images.
- The generator is trained to improve its ability to generate realistic images.

The `train` function accepts two arguments:
- `dataset`: The preprocessed image dataset.
- `epochs`: Number of training epochs (default is set to 3000).

### Step 8: Generate and Save Images
During training, images are generated by the generator every 50 epochs and saved to the specified output directory:
```python
os.makedirs('/content/drive/MyDrive/gan_output', exist_ok=True)
```

Images are saved in the `gan_output` folder in Google Drive as `image_at_epoch_xxxx.png`.

### Example Output:
The following is an example of the expected output images during the GAN training process.

```
/gan_output/
  image_at_epoch_0050.png
  image_at_epoch_0100.png
  ...
```

### Step 9: Start Training
To start training the GAN, run the following code:
```python
EPOCHS = 3000  # You can modify this value based on your requirements
train(dataset, EPOCHS)
```

### Modify the Script
- If your dataset has different image dimensions, adjust the `IMG_HEIGHT`, `IMG_WIDTH`, and `CHANNELS`.
- You can also modify the architecture of the generator and discriminator to fit your needs.

## Directory Structure

Here’s an overview of the key components of the script and folders:

```
├── gan_training.py           # Main GAN training script
├── README.md                 # Documentation
└── /gan_output/              # Folder where output images are saved
```

## Results

The output images generated by the GAN during training will be stored in the `gan_output` directory in your Google Drive. You can use these images to evaluate the performance of the GAN over time.

## Notes

- **Training Time**: GANs can take a long time to train, especially for high-resolution images or large datasets.
- **Hardware**: It is recommended to use GPU hardware acceleration in Colab for faster training.

## License

This code is free to use and modify for educational and research purposes.
