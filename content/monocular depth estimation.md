https://paperswithcode.com/task/monocular-depth-estimation

goal: measuring 3D depth using cameras
### used in:
- 3d scene reconstruction
- autonomous driving
- AR
### methods:
- network to regress depth map
- splitting inputs into bins or windows to reduce complexity

### 📊 benchmarks
- KITTI
- NYUv2 datasets
### 📈 evaluation
- RMSE
- absolute relative error

alternative: LiDAR
- pros:
	- accurate depth using TOF (Time of Flight)
- cons:
	- sparse in vertical and horizontal resolution
		- difficult segmentation to determine location and shape
compared to monocular depth
- pros:
	- denser texture
- cons:
	- less depth info

solution to this => [LiDAR + Monocular Depth Fusion](https://www.ri.cmu.edu/app/uploads/2019/12/20190716-Chen.pdf)
- provides denser pixel-wise map
- leverages
	- early fusion technique
		- input: 
			- RGB image
			- sparse depth info
	- finetuned ResNet model = encoder
	- Residual Up-Projection (RUB) block: 
		- recovers spatial features + context within depth map
		- increase spatial resolution (solves depth completion)
		- nearest neighbor interpolation
		- concatenation of 4 RUB
	- depth feature tensor: 
		- propagates encoder -> decoder (RUB) through skip connections
		- sends 3 skip connections to pass feature tensors
		- forward more info like object boundaries, feature tensors, context info
- loss: Berhu instead of MSE (larger error penalization)
- evaluated against  NYUdepthV2 and KITTI datasets

depth info:
- heading angle of vehicle
- 3d location + distance
- rough shape of vehicle/obstacle

### 🌧️ factors
- lighting
- occlusion (car itself)
- texture
Learn how to build a [Depth estimation pipeline](https://huggingface.co/docs/transformers/main/en/tasks/monocular_depth_estimation) 

### depth prediction
single RGB image
- hard but not impossible
- Markov Random Field (MRF)
	- depth + superpixels
- combined semantic labels
### depth completion
- depth inpainting
- dense completion

Side Note:
RADAR:
- object level speed

## WATonomous
section to note what's being used
- they did some benchmarking and [Depth-Anything](https://github.com/LiheYoung/Depth-Anything) was the fastest one
- [ros2 implementation](https://github.com/scepter914/DepthAnything-ROS) 


## Toyota Research
based on this [article](https://medium.com/toyotaresearch/monocular-depth-in-the-real-world-99c2b287df34)  that summarizes _Self-Supervised Camera Self-Calibration from Video_ (ICRA, 2022)

components to use geometry as inductive bias
- depth
- pose (ego motion)
- camera model
	- "assumed", simplified to pinhole camera model which is not good for approximating other types of cameras: fisheye, radial distortion, catadioptric

introduces *Unified Camera Model* (UCM)
- 5 params (1 more than pinhole) - better approx

- learned camera parameters