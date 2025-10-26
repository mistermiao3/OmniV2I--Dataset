The OmniV2I Dataset: Detailed Information
1. Overview
The OmniV2I dataset is a multi-modal, multi-illumination dataset collected for the research and evaluation of online Vehicle-to-Infrastructure (V2I) calibration and cooperative perception algorithms. It was collected in Zhenjiang, China, and features a unique, panoramic roadside sensor suite.
2. Data Acquisition Platform
Roadside Unit (RSU): A perception unit deployed at the center of the intersection.
LiDAR System: A 360° fused point cloud is generated from one RoboSense RS-80 (80-beam mechanical LiDAR) and two RoboSense RS-LiDAR-M1P (solid-state LiDARs). All LiDARs are pre-calibrated, and their data is fused into a single, high-density point cloud in the rsu_base coordinate frame.
Camera System: Two industrial cameras are coaxially mounted with the two solid-state LiDARs, providing surround-view coverage.
Data Synchronization: All RSU sensor data is synchronized using a hardware trigger and recorded as a ROS 1 bag file.
Onboard Unit (OBU): A system mounted on a test vehicle.
Camera System: A single, forward-facing stereo camera, from which only the left video feed is used.
Data Recording: The onboard video is recorded as a standard MP4 file. A manual synchronization signal (e.g., a visual marker event) was performed at the beginning of each take to enable offline time alignment with the RSU data.
3. Collection Scenarios
Data was collected at two challenging urban intersections in Zhenjiang, China, known for their high traffic density and complex environments:
Intersection 1 (IS1): Xuefu Road & Guyang Road intersection.
Intersection 2 (IS2): Dingmao Viaduct & Zhihui Avenue intersection.
For each intersection, data was systematically collected along two primary paths (East-West and North-South) under three distinct lighting conditions:
Daytime: Clear daylight conditions with strong shadows.
Dusk: Low-light, transitional conditions, often with vehicle headlights active.
Nighttime: Full darkness, with illumination provided only by streetlights and vehicle lights.
This resulted in a total of 2 intersections * 2 paths * 3 lighting conditions = 12 unique scenarios, each with multiple trial runs.
4. Provided Data
For each scenario, the dataset provides:
RSU Data: A ROS 1 bag file (which can be converted to ROS 2) containing:
/rsu/pointcloud_stitched (sensor_msgs/PointCloud2): The 360° fused point cloud.
/rsu/camera/[direction]/image_raw (sensor_msgs/Image): Image streams from the roadside cameras.
OBU Data:
[trajectory_id].mp4: The raw video file from the onboard camera.
Calibration & Ground Truth:
calib/rsu_extrinsics.yaml: Extrinsic parameters between all RSU sensors.
calib/rsu_camera_intrinsics.yaml: Intrinsic parameters for all RSU cameras.
calib/obu_camera_intrinsics.yaml: Intrinsic parameters for the onboard camera.
ground_truth/trajectory_lengths.csv: A file containing the manually measured, high-precision ground truth lengths for 48 evaluated trajectory segments, indexed by a unique segment ID.
5. Recommended Usage
This dataset is primarily designed for the task of online, targetless extrinsic calibration between a moving vehicle and static infrastructure. It can also be used for research in related V2I cooperative perception tasks, such as 3D object detection, tracking, and sensor fusion, especially for evaluating algorithm robustness under different lighting conditions.
