# Fashion MNIST Classifier

A Streamlit web app that classifies clothing images into one of 10 Fashion MNIST categories using a dense neural network trained from scratch.

**Live app:** https://fashionmnistwebapp.streamlit.app/

## Features

- **Upload an image** — drop in a photo of a clothing item (PNG/JPG/JPEG/BMP/WEBP) and get a live prediction. A toggle handles the light-background-vs-dark-background inversion Fashion MNIST images expect.
- **Try a sample** — pull a random image straight from the Fashion MNIST test set and compare the model's prediction against the actual label.
- **About the model** — view the network architecture and live-computed accuracy, precision, recall, and F1-score per class on the full 10,000-image test set.
- Light/dark theme support with a custom blue-violet gradient design.

## Categories

T-shirt/top · Trouser · Pullover · Dress · Coat · Sandal · Shirt · Sneaker · Bag · Ankle boot

## Model

A fully-connected (dense) network trained on the 28x28 grayscale Fashion MNIST images, flattened to 784-length input vectors:

```
Input(784)
  -> Dense(32, relu)
  -> Dense(64, relu)
  -> Dense(128, relu)
  -> Dense(10, softmax)

optimizer: rmsprop
loss: sparse_categorical_crossentropy
```

The trained model is saved at `model/fashion_mnist.keras` and loaded via `tensorflow.keras`.

## Project structure

```
.
├── streamlit_app.py       # Main Streamlit UI (upload, sample, about tabs)
├── utils/
│   └── model.py            # Model loading, preprocessing, and prediction helpers
├── model/
│   └── fashion_mnist.keras # Trained Keras model
├── requirements.txt         # Python dependencies
├── runtime.txt              # Python version hint (see Deployment notes below)
└── .streamlit/
    └── config.toml          # Light/dark theme configuration
```

## Running locally

1. Clone the repository:
   ```bash
   git clone https://github.com/HammadHasan2004/Fashion_Mnist_web_app.git
   cd Fashion_Mnist_web_app
   ```
2. Create a virtual environment and install dependencies:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. Run the app:
   ```bash
   streamlit run streamlit_app.py
   ```
4. Open the URL Streamlit prints (usually `http://localhost:8501`).

## Tech stack

- [Streamlit](https://streamlit.io/) — web UI
- [TensorFlow / Keras](https://www.tensorflow.org/) — model definition, loading, and inference
- [scikit-learn](https://scikit-learn.org/) — classification report (precision/recall/F1)
- [pandas](https://pandas.pydata.org/) / [NumPy](https://numpy.org/) — data handling
- [Pillow](https://python-pillow.org/) — image preprocessing for uploads

## Deployment notes

This app is deployed on [Streamlit Community Cloud](https://streamlit.io/cloud). Note that Community Cloud does **not** read `runtime.txt` to select the Python version — the version must be set explicitly in the app's **Advanced settings** (or dashboard **Settings**) instead. This project targets **Python 3.12**, since that's the range with published TensorFlow wheels for the pinned `tensorflow` version in `requirements.txt`.

## License

No license specified.
