
Installer : 
	uvc_camera  (ou nouveau : libuvc_camera)
	april_tags_node
	camera_calibration
	image-proc
	
Sourcer : 

	source /opt/ros/indigo/setup.bash


Liste des caméras dispos : 

	ls -l /dev/video*


Lancer le noeud récupérant l'image caméra : (par défaut /dev/video0)

	rosrun uvc_camera uvc_camera_node [device]    (rosrun uvc_camera uvc_camera_node _device:=/dev/video0)


Calibration de la caméra : (http://wiki.ros.org/camera_calibration/Tutorials/MonocularCalibration)

	rosrun camera_calibration cameracalibrator.py --size 8x6 --square 0.108 image:=/camera/image_raw camera:=/camera

utilisé : 
	rosrun camera_calibration cameracalibrator.py --size 9x6 --square 0.025 image:=/image_raw camera:=/ --no-service-check

(dammier de 9x6 carreau de 2,5 (cm de côté) )

=> extraire ost.yaml : fichier de calibration. Changer à l'intérieur de nom de la camera :  camera au lieu de narrow_stereo



Lancement du noeud driver : 

	 ROS_NAMESPACE=camera rosrun uvc_camera uvc_camera_node _camera_info_url:="file:///home/hoagie/Bureau/CameraEtTags/ost.yaml"



Lancement du noeud de rectification : 

	ROS_NAMESPACE=camera rosrun image_proc image_proc



Script de lancement détecteur d'apriltag: 

<launch>
<node pkg="apriltags_ros"  type="apriltag_detector_node" name="apriltag_detector" output="screen">
  <remap from="image_rect" to="/camera/image_rect" />
  <remap from="camera_info" to="/camera/camera_info" />
  <param name="tag_family" type="str" value="36h11" />
  <rosparam param="tag_descriptions">
     [{id: 0, size: 0.163513},
     {id: 1, size: 0.163513}]
  </rosparam>
</node>
</launch>



Liste des tags détectés et de leurs poses : 

	rostopic echo /tag_detections_pose
