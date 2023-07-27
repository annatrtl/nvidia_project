Poisonous Plant Identifier

This model identifies whether a plant is poisonous or not. It is trained on an imagenet Resnet-18 model using transfer learning. It can help people avoid illness and death by informing the user if the plant is dangerous.

## The Algorithm
The algorithim uses a 2GB Jetson Nano, and so it uses it a preflashed SD card flashed from the NVIDIA webpage. The transfer model classifies the plant as safe or not by using pattern recognition. It does so by being trained on a modified version of the Pl@ntNet dataset, making it able to recognize 65 different plants. Once it recognizes the plant it will output out: whether the plant is poisonous or not based on training, and the confidence of the answer based on validation. It is up to the user to interepret the information.
Note: A flower is considered poisonous if it is unsafe to eat.

## Running this project
1. Connect to your Jetson Nano via VSCODE. 
2. Ensure that you have the proper things installed. The Renet18.onnx and all others like that - the ones that say resnet18.onnx. Also, esure that you have the labels.txt file.
3. Since using the preflashed SD card, there should be a docker container. This is accesable by implementing this code. Change directories into jetson-inference
4. Then run this code -$ ./docker/run.sh
5. In jetson-inference/python/training/classification, run the following code to train the model - $ python3 train.py --model-dir=models/images data/images
6. Run the ennox export script - $ python3 onnx_export.py --model-dir=models/images
7. Exit the docker container and make sure you are in jetson-inference/python/training/classification
8. Make sure the model is on the nano (You should see a file named resnet18.onnx) - $ ls models/images/
9a. Set the NET variable - $ NET=models/images
9b. Set the DATASET variable - $ DATASET=data/images
10. Test it out on a poisonous image - $ imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/poisonous/0a0d16e9ef6ec8dfe67f98fea4c311d6dadb2932.jpg poisonous.jpg
10. Open VsCode and view the output!

https://youtu.be/BbmQsvx0TRI
