# Proyecto

- Código:

~~~
#!/usr/bin/env python3

#Tortuga 5
#Laboratorio de Principios de Mecatronica 
#Benito Granados
#Primavera 2021
#Isaias Jesus Garcia Moreno
#Mercedes Citlalic Luna Herrera

import rospy
from geometry_msgs.msg import Twist
from turtlesim.msg import Pose
import math
import time
from std_srvs.srv import Empty

x = 0
y = 0
z = 0
theta = 0

x1 = 0
y1 = 0

x2 = 0
y2 = 0

x3 = 0
y3 = 0

x4 = 0
y4 = 0

x6 = 0
y6 = 0


def poseCallback(pose_message):
    global x
    global y
    global z
    global theta

    x = pose_message.x
    y = pose_message.y
    theta = pose_message.theta


def poseCallback1(pose_message):
    global x1
    global y1

    x1 = pose_message.x
    y1 = pose_message.y


def poseCallback2(pose_message):
    global x2
    global y2

    x2 = pose_message.x
    y2 = pose_message.y


def poseCallback3(pose_message):
    global x3
    global y3

    x3 = pose_message.x
    y3 = pose_message.y


def poseCallback4(pose_message):
    global x4
    global y4

    x4 = pose_message.x
    y4 = pose_message.y


def poseCallback6(pose_message):
    global x6
    global y6

    x6 = pose_message.x
    y6 = pose_message.y


def checkTurtleRadiusFront(radius):
    m = math.tan(theta)
    if (x1 - x)**2 + (y1-y)**2 < radius**2 and y1 >= y+m*(x1-x):
        print('Tortuga1')
        return True

    elif (x2 - x)**2 + (y2-y)**2 < radius**2 and y2 >= y+m*(x2-x):
        print('Tortuga2')
        return True

    elif (x3 - x)**2 + (y3-y)**2 < radius**2 and y3 >= y+m*(x3-x):
        print('Tortuga3')
        return True

    elif (x4 - x)**2 + (y4-y)**2 < radius**2 and y4 >= y+m*(x4-x):
        print('Tortuga4')
        return True

    elif (x6 - x)**2 + (y6-y)**2 < radius**2 and y6 >= y+m*(x6-x):
        print('Tortuga6')
        return True

    else:
        return False


def checkTurtleRadiusBack(radius):
    m = math.tan(theta)
    if (x1 - x)**2 + (y1-y)**2 < radius**2 and y1 < y+m*(x1-x):
        print('Tortuga1')
        return True

    elif (x2 - x)**2 + (y2-y)**2 < radius**2 and y2 < y+m*(x2-x):
        print('Tortuga2')
        return True

    elif (x3 - x)**2 + (y3-y)**2 < radius**2 and y3 < y+m*(x3-x):
        print('Tortuga3')
        return True

    elif (x4 - x)**2 + (y4-y)**2 < radius**2 and y4 < y+m*(x4-x):
        print('Tortuga4')
        return True

    elif (x6 - x)**2 + (y6-y)**2 < radius**2 and y6 < y+m*(x6-x):
        print('Tortuga6')
        return True

    else:
        return False


def orientate(xgoal, ygoal):

    global x
    global y
    global theta

    velocity_message = Twist()
    cmd_vel_topic = '/turtle5/cmd_vel'

    while(True):
        if theta < 0:
            theta = theta + 2*math.pi
        ka = 1.0
        desired_angle_goal = math.atan2(ygoal-y, xgoal-x)

        if desired_angle_goal < 0:
            desired_angle_goal = desired_angle_goal + 2*math.pi
            dtheta = desired_angle_goal - theta
            
        else:
            desired_angle_goal = desired_angle_goal
            dtheta = desired_angle_goal - theta
            
        if (abs(dtheta) < 0.005):
            print('angle', theta*360.00/6.2831, 'reached')
            time.sleep(1)
            break

        angular_speed = ka * dtheta

        velocity_message.linear.x = 0.0
        velocity_message.angular.z = angular_speed
        velocity_publisher.publish(velocity_message)
        


def go_to_goal(xgoal, ygoal, radius):

    global x
    global y
    global theta

    velocity_message = Twist()
    cmd_vel_topic = '/turtle5/cmd_vel'

    while(True):
        ka = 5.0
        desired_angle_goal = math.atan2(ygoal+0.01-y, xgoal+0.01-x)
        

        if (desired_angle_goal < 0.0):
            desired_angle_goal = desired_angle_goal + 6.2831
            
        else:
            desired_angle_goal = desired_angle_goal
            

        dtheta = desired_angle_goal-theta
        
        angular_speed = ka * (dtheta)

        if (abs(angular_speed) < 0.5):
            angular_speed = angular_speed
        else:
            angular_speed = 0.0

        kv = 1
        distance = abs(math.sqrt(((xgoal-x)**2)+((ygoal-y)**2)))
        linear_speed = kv * distance

        if (distance < 0.1):
            print('point (', x, ',',  y, ') reached')
            time.sleep(1)
            break
        turtleFront = checkTurtleRadiusFront(radius)
        turtleBack = checkTurtleRadiusBack(radius)
        if(turtleFront and turtleBack):
            velocity_message.linear.x = 0
            print('Alto')
        elif(turtleFront):
            velocity_message.linear.x = -1*linear_speed
            print('Atras')

        else:
            velocity_message.linear.x = linear_speed
        velocity_message.angular.z = angular_speed
        velocity_publisher.publish(velocity_message)
        


if __name__ == '__main__':
    try:

        rospy.init_node('turtlesim_motion_pose', anonymous=True)

        cmd_vel_topic = '/turtle5/cmd_vel'
        velocity_publisher = rospy.Publisher(
            cmd_vel_topic, Twist, queue_size=10)

        position_topic = "/turtle5/pose"
        pose_subscriber = rospy.Subscriber(position_topic, Pose, poseCallback)

        position_topic1 = "/turtle1/pose"
        pose_subscribe1 = rospy.Subscriber(
            position_topic1, Pose, poseCallback1)

        position_topic2 = "/turtle2/pose"
        pose_subscribe2 = rospy.Subscriber(
            position_topic2, Pose, poseCallback2)

        position_topic3 = "/turtle3/pose"
        pose_subscribe3 = rospy.Subscriber(
            position_topic3, Pose, poseCallback3)

        position_topic4 = "/turtle4/pose"
        pose_subscribe4 = rospy.Subscriber(
            position_topic4, Pose, poseCallback4)

        position_topic6 = "/turtle6/pose"
        pose_subscribe6 = rospy.Subscriber(
            position_topic6, Pose, poseCallback6)

        time.sleep(2.0)

        orientate(10.0, 10.0)
        time.sleep(0.5)
        go_to_goal(10.0, 10.0, 1)
        time.sleep(0.5)

        orientate(1.0, 4.0)
        time.sleep(0.5)
        go_to_goal(1.0, 4.0, 1)
        time.sleep(0.5)

        orientate(3.5, 7.0)
        time.sleep(0.5)
        go_to_goal(3.5, 7.0, 1)
        time.sleep(0.5)


        orientate(8.0, 1.0)

    except rospy.ROSInterruptException:
        pass
~~~
