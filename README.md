# TeachableMachineWebUI

## 📘 Teachable Machine Webcam Classifier

This is a simple web app that uses a machine learning model you trained with [Teachable Machine](https://teachablemachine.withgoogle.com/) to make predictions from your webcam in real time.

### 🧠 What This Does

1. Loads a pre-trained **image classification model** you made in Teachable Machine.
2. Connects to your webcam and captures live video frames.
3. Feeds each video frame into the model.
4. Displays the model's predictions (e.g., "Thumbs Up: 0.98") live on the screen.

No Python, no build tools—just HTML and JavaScript.

## 🚀 Try It With Your Own Model

To use **your own Teachable Machine model**:

1. Train a model at [https://teachablemachine.withgoogle.com/](https://teachablemachine.withgoogle.com/)
2. Click **Export Model → TensorFlow.js**
3. Copy the model URL provided (should look like:  
   `https://teachablemachine.withgoogle.com/models/your-model-id/`)
4. Replace the `URL` in the HTML:

```js
const URL = "https://teachablemachine.withgoogle.com/models/YOUR_MODEL_ID/";
```

## 🛠️ How You Can Use the Predictions

The key line is this:

```js
const prediction = await model.predict(webcam.canvas);
```

That gives you an **array of predictions**, one for each class in your model:

```js
[
    {
        "className": "Person",
        "probability": 0.9999200105667114
    },
    {
        "className": "Animal",
        "probability": 0.0000800028137746267
    },
    {
        "className": "Background",
        "probability": 1.6130065061403798e-9
    }
]
```

You can use that array to build interactive applications. For example:

### 🎨 Change the Background

```js
if (prediction[0].probability > 0.9) {
    document.body.style.backgroundColor = "blue";
}
```

### 🗣 Speak the Label

```js
if (prediction[0].probability > 0.9) {
    const msg = new SpeechSynthesisUtterance(prediction[0].className);
    window.speechSynthesis.speak(msg);
}
```

### 🕹 Trigger Logic or Animation

```js
if (prediction[1].probability > 0.8) {
    player.jump();
}
```