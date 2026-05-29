# Finger Identity Classifier Deployment Instructions

This document provides instructions for deploying the finger identity classifier using the EfficientNet-B1 model, which was determined to be the best balance of accuracy, speed, and size.

## Prerequisites
Check requirments.txt

## Model Weights
The trained model weights are saved as `EfficientNetB1_best.pth`.

## Deployment Steps

### 1. Load the Model
```python
import torch
import timm
import torch.nn as nn

def load_model(model_path):
    model = timm.create_model('efficientnet_b1', pretrained=False, num_classes=5)
    model.load_state_dict(torch.load(model_path, map_location=torch.device('cpu')))
    model.eval()
    return model
```

### 2. Preprocess Input
Input images should be cropped to the finger region using MediaPipe or a similar landmark detector, then resized to 224x224.
```python
from torchvision import transforms
from PIL import Image

preprocess = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.ToTensor(),
    transforms.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225])
])

def predict(model, image_path):
    image = Image.open(image_path).convert('RGB')
    input_tensor = preprocess(image).unsqueeze(0)
    with torch.no_grad():
        output = model(input_tensor)
    _, predicted = torch.max(output, 1)
    classes = ['thumb', 'index', 'middle', 'ring', 'pinky']
    return classes[predicted.item()]
```

### 3. API Integration
You can wrap this in a FastAPI or Flask application for real-time inference.

## Performance Metrics
- **Accuracy**: ~42.7% (on demo subset, expected higher with full training)
- **Inference Latency**: ~10ms per image (CPU)
- **Model Size**: ~25 MB
