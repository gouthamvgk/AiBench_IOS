# AiBench - A tool for benchmarking CoreMLModels

AiBench helps you to know Coreml model's execution time and also supports output visualization for supported model types. You can either benchmark a wide variety of open source MLModels that is available in the App by default or add your own custom CoreMl Model for timing it.

## Benchmarking opensource models
By default, the app has opensource models for different tasks like classification, detection, pose estimation, segmentation, and regression. All these models aren't downloaded by default to save storage and so download only the model of your preference to benchmark it. Most of the default models comes with three different versions of weights float32, float16, and int8. If you are familiar with machine learning then these versions are quantized formats of the same model and accuracy degrades as precision decreases. Note: CoreMl runs the inference in Float32(CPU) or Float16(GPU) irrespective of weights precision.

The information of opensource models is maintained in servers and will be updated periodically so that the user can get hold of the latest opensource models once the developer adds them. If you have converted  some new state of the art model to CoreML and wish to add it to the library for everyone's use then please contact the developer. If you want to manually sync the opensource library in device with the current model information in server press refresh icon in App homepage

## Running on different devices
While benchmarking the opensource models or your custom models, you can choose the device on which the model should be run. The options are 

-  CPU - Runs on CPU
- C/GPU - Runs on GPU if compatible else on CPU
- Best - Runs on the best device available and it includes NPU if your Iphone supports it

## Deleting downloaded model weights
After downloading and benchmarking the models, you can delete the weights if you don't need them for future use. You can press Remove_model button in the model page to delete the corresponding model's weights or if you want to delete all downloaded weights at once press the bin icon in the App homepage. This will only delete the weights and all the model information is retained so that you can download them again in future(including custom models). In the case of custom models once you remove the model individually, then both model weights and information will be deleted.

## Downloading and running Custom models of User
The user can add his/her own model to benchmark for time and also visualize the results. To add your model press Add_model button in the app homepage. It will prompt you to enter the URL of your CoreML model and a name for it. Provide the correct URL of where your model is hosted and the app will download it, checks it for compliance with below mentioned rules, and then adds it to the library. Note: All your models are directly downloaded to your device and stored locally, the app doesn't collect any information about your custom models.

The custom model has to be in the following format for benchmarking. Following points assume you have some knowledge of CoreML

- The custom CoreMl model should be taking inputs in Image format directly. The App internally uses the Vision framework's VNModel for inference so the app expects the model to have input as MLFeature's Image type. 
- If you are having multiple inputs for your model then only the Image input should be mandatory and all other inputs must be optional. The app provides only the Image input to the model at runtime. So if your model expects some other mandatory input, adding of custom Model will result in failure
- If your custom model has image input and outputs in different formats like MultiArray, string, dictionary, etc then the App will display only the FPS and output information during benchmarking. If you want to visualize your model results, currently the app supports visualization for classification, detection, and segmentation. For each task, you should provide the model in the following format for visualization of results
	
	- For classification, your CoreML model should be of type NeuraNetwork Classifier and it should have the attribute "predictedFeatureName" and "predictedProbabilitiesName" configured inside it. Also, the two outputs of your model should have the same names contained in the properties mentioned above.
	-  For detection, your model should be of type pipeline and it should have only two outputs corresponding to boxes and class scores. The outputs should be of type MultiArray and they should be named as "confidence" and "coordinates" exactly. Refer this awesome blog [https://machinethink.net/blog/mobilenet-ssdlite-coreml/](https://machinethink.net/blog/mobilenet-ssdlite-coreml/) for conversion steps.
	- For segmentation, your network should be of type Neural Network and it should have only one output of type MultiArray and name "semanticPredictions". The shape of segmentation network output and input should be the same for proper visualization.

If your model output is different from above mentioned formats, then the output of benchmark is FPS and the description of each output.

## Usage
The developer has no ownership over the opensource models provided in the library. Use of them is entirely based on their opensource license for academic and research use. So usage of this App and opensource models present in it for commercial usage is strictly prohibited. For more information about each model's license click the about icon in model page.
