# Overview
This repo contains code for the "TensorFlow for poets 2" series of codelabs (https://github.com/googlecodelabs/tensorflow-for-poets-2). This example shows how to recognize different types of flowers. If you have other objects to classify, change the path in the last line of Step 4 to your image path.

## Requirements
* Tensorflow
* Python 3.5

## Initial setup to retrain a model
1. Get images on which you want to retrain the model. For example flower images:
```
curl http://download.tensorflow.org/example_images/flower_photos.tgz \
tar xz -C tf_files
```
2. Set shell variables and start tensorboard
```
IMAGE_SIZE=224
ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"
tensorboard --logdir tf_files/training_summaries &
```

3. Start the retraining script (retrain.py) with additional parameters
```
python -m scripts.retrain \
  --bottleneck_dir=tf_files/bottlenecks \
  --how_many_training_steps=1000 \
  --model_dir=tf_files/models/ \
  --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
  --output_graph=tf_files/retrained_graph.pb \
  --output_labels=tf_files/retrained_labels.txt \
  --architecture="${ARCHITECTURE}" \
  --image_dir=tf_files/flower_photos
  ```
  
  4. Test your retrained graph with pictures the model has not seen before
  ```
  python -m scripts.label_image \
    --graph=tf_files/retrained_graph.pb  \
    --image=tf_files/NewImagePath
  ```




