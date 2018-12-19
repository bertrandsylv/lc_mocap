#!/usr/bin/env python  

import rospy

import tf

from geometry_msgs.msg import PoseArray, Pose, Point, Quaternion



def handle_turtle_pose(poseArray, tagNo):
    br = tf.TransformBroadcaster()
    br.sendTransform(pose[0].position, pose[0].orientation, rospy.Time.now(), 'tag%s' % tagNo, 'world')



if __name__ == '__main__':
    rospy.init_node('tf_broadcaster')
    
    rospy.Subscriber('/tags_detections_pose',
                     PiseArray,
                     handle_turtle_pose, '0')
    rospy.spin()
