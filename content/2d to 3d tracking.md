
input: 2d detections + lidar pointcloud
output: 3d detections

- using `tf2_ros::Buffer->lookupTransformation` : converts from lidar frame to camera frame (associate lidar points to camera detections)
	- returns `geometry_msgs::TransformStamped` if transformation is sucessful
- remove floor from lidar
	- why are we using a mutex lock guard?
	- `ProjectionUtils::removeFloor`
- transform lidar points to 2d camera points
	- `ProjectionUtils::projectLidarToCamera`
	- add to `lidar2dProjs`
	- add to `inCameraPoints` (contains `pcl::PointXYZ` points)
- for each 2d detection
	- `ProjectionUtils::pointsInBbox` get lidar points in bounding box
	- store it in `inlier_points`
	- `ProjectionUtils::getClusteredBBoxes` get cluster of 3d bounding boxes
	- `highestIOUScoredBBox` get best bounding box from all clustered 3d bounding boxes
		- iou score computed by calculating overlap
	- add to marker and 3d detection array