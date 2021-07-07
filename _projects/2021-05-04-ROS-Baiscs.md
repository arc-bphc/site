---
title: ROS Basics
date: 2021-05-04 16:17:25 +/-0530
tags: [ros,topics,services,actions,packages,launch]     # TAG names should always be lowercase
layout: article
article_header:
  type: cover
  image:
    src: /screenshot.jpg
cover: /assets/images/fish.jpg
---
## Packages
ROS uses packages to orgnaize its program, you can think of a package as all the files that a specific ROS program needs to run sucessfully. 
A few common items inside a package:

- **launch** - contains launch files
- **src** - contains the source files
- **CMakeLists.txt** - contains the rules for compilation
- **package.xml** - package info and depends

You can use roscd to go to any package in ROS
`roscd <package_name>`

### Creating ROS Packages
All packages must be created inside `~/catkin_ws/src`

**To create a package the following synatx can be used:**

`catkin_create_pkg <package_name> <package_depends>`

### Compiling ROS Packages 
Once a package has been created, it needs to be compiled in order for it to work.

`catkin_make` - Will compile the entire src directory and needs to be issued only in the catkin_ws directory.
`catkin_make --only-pkg-with-deps <package_name>` - Will only compile the selected package.


## Nodes
Nodes are individual ROS programs that together with other nodes form a working structure.

**To launch a node from the terminal:**
`rosrun <package_name> <node_name> __name:=new_node_name __ns:=name_space topic:=new_topic`

**To get a list of nodes that are currently active:**
`rosnode list`

**To get more information about a paticular node:**
`rosnode info /node_name`


## Launch Files
All launch files are contained inside the `<launch>` tags. Launch files are used to "launch" nodes/programs in ROS. One of the major advantages of launch files is the fact that you can launch multiple nodes at once.
```html
<launch>  
    <include file="$(find package_where_launch_is)/launch/my_launch_file.launch"/>  
    <node pkg="package_name" type="script_name.py" name="node_name" output="screen" respawn="false" ns="w">
        <remap from="/current_topic" to="/needed_topic"/>
    </node>
</launch>
```

## Parameter Server
A parameter server is a dictonary that ROS uses to store parameters. Any ROS program can access these parameters during runtime to customize itself accordingly. The following commands can be used to interact with the parameter server.

`rosparam list` - Gets a list of parameter names that can be accessed
`rosparam get <parameter_name>` - Gets the current value of that parameter
`rosparam set <parameter_name> <value>` - Updates the parameter value


## Topics

ROS Nodes communicate with each other via communication channels called "Topics", further messages are passed between nodes through topics. Every topic has a message type that it supports communication over. Nodes can subscribe to a topic to listen to data from other nodes or publish to topics to send data to other nodes which are subscribed to a given topic.

**To check for active topics:**

`rostopic list`

**For more information about a topic:**

`rostopic info /topic_name`

**To publish to a topic at a rate of x Hz:**

`rostopic pub -r x /topic_name /message_type args`

**To Listen to a topic:**

`rostopic echo /topic_name`

### Simple Publisher
```python
#! /usr/bin/env python

import rospy
from std_msgs.msg import String

rospy.init_node('node_name')
pub = rospy.Publisher('/topic_name', String, latch=True, queue_size=10)

r = rospy.Rate(10) # 10hz

while not rospy.is_shutdown():
   pub.publish("hello world")
   r.sleep()
```
### Simple Subscriber
```python
#! /usr/bin/env python

import rospy
from std_msgs.msg import String

def callback_function(data):
    result = data.data
    print(result)

rospy.init_node('node_name')
rospy.Subscriber('/topic_name',String,callback_function)
rospy.spin()
```

## Messages
As explained before data is sent via messages inside topics. ROS has a rich set of predefined messages that can be used.

**To find out more infomation about a paticular message:**

`rosmsg show <package_name>/<message>`

You can get more information about what message type is used by a paticular node by using `rosnode info`. Messages can contain premitive datatypes or can be composed of multiple primitve datatypes. Here is an example `rosmsg show geometry_msgs/PointStamped`

```
[geometry_msgs/PointStamped]:
std_msgs/Header header

uint32 seq  
time stamp  
string frame_id  

geometry_msgs/Point point

float64 x  
float64 y  
float64 z  
```

### Custom Messages
In situations where standard messages don't do the job, you can create your own message types using the following steps.

- **Create a `msg` folder in your package directory**
- **Create a new file named `YourMessage.msg` inside the msg folder.**
- **`Age.msg` should contain the message structure for example**

	```
	Float32 Years   
	Float32 Months
	Float32 Days
	```
- **Edit the CMakeLists.txt - find_package()**
This is where all the packages required to COMPILE the messages of the topics, services, and actions go. In package.xml, you have to state them as build_depend.
	```
	find_package(catkin REQUIRED COMPONENTS
		 rospy
		 std_msgs
		 message_generation   # Add message_generation here, after the other packages
	)
	```
- **Edit the CMakeLists.txt - add_message_files()** This function includes all of the messages of this package (in the msg folder) to be compiled. The file should look like this.
	```
	add_message_files(
		FILES
		Age.msg
	  ) # Dont Forget to UNCOMENT the parenthesis and add_message_files TOO
	```
- **Edit the CMakeLists.txt - generate_messages()** Here is where the packages needed for the messages compilation are imported.
	```
	generate_messages(
		DEPENDENCIES
		std_msgs
	) # Dont Forget to uncoment here TOO
	```
- **Edit the CMakeLists.txt - catkin_package()** State here all of the packages that will be needed by someone that executes something from your package. All of the packages stated here must be in the package.xml as exec_depend.
	```
	catkin_package(
		CATKIN_DEPENDS rospy message_runtime   # This will NOT be the only thing here
	)
	```
- **Edit the package.xml**
Just add these 3 lines to the package.xml file.
	```
	<build_depend>message_generation</build_depend> 
	<build_export_depend>message_runtime</build_export_depend>
	<exec_depend>message_runtime</exec_depend>
	```
- **Compile**
	```
	roscd; cd ..
	catkin_make
	source devel/setup.bash
	```
- **Verification**
	`rosmsg show Age`       
	  
	```
	[topic_ex/Age]
	float32 years   
	float32 months   
	float32 days
	```
- Using these in ROS Nodes
```python
from package_name.msg import Age
```


## Services
Messages over topics are not the only way nodes communicate with each other, Services are a synchronous way of commincation where a ROS program calls a service, and waits until it receives a result from the service before continuing.

**To view what services are currently being offered:**

`rosservice list`

**For more information about a service:**

`rosservice info /service_name`

This will return you the `name_of_the_package/Name_of_Service_message`

**To call a service via terminal:**

`rosservice call /service_name /message_type arguments`

### Client
This is what CALLS the functionality provided by the Service Server. That is, it CALLS the Service Server.

```python
#! /usr/bin/env python

import rospy
# Import the service message used by the service /trajectory_by_name
from trajectory_by_name_srv.srv import TrajByName, TrajByNameRequest
import sys

rospy.init_node('service_client')

rospy.wait_for_service('/trajectory_by_name')
traj_by_name_service = rospy.ServiceProxy('/trajectory_by_name', TrajByName)
traj_by_name_object = TrajByNameRequest()

traj_by_name_object.traj_name = "release_food"
result = traj_by_name_service(traj_by_name_object)
print result
```
### Service Messages
ROS Services are defined by srv files, which contains a request message and a response message. These are identical to the messages used with ROS Topics (see rospy message overview). rospy converts these srv files into Python source code and creates three classes that you need to be familiar with: service definitions, request messages, and response messages. The names of these classes come directly from the srv filename:

`my_package/srv/Foo.srv → my_package.srv.Foo`

`my_package/srv/Foo.srv → my_package.srv.FooRequest`

`my_package/srv/Foo.srv → my_package.srv.FooResponse`

Service message files have the extension `.srv`. Remember that Topic message files have the extension `.msg`. Service message files are defined inside a srv directory. Remember that Topic message files are defined inside a msg directory.

**To see the structure of a srv message:**

`rossrv show name_of_the_package/Name_of_Service_message`

**Service messages have TWO parts:**

**REQUEST**

The REQUEST is the part of the service message that defines HOW you will do a call to your service. This means, what variables you will have to pass to the Service Server so that it is able to complete its task.

**---**

**RESPONSE**

The RESPONSE is the part of the service message that defines HOW your service will respond after completing its functionality. If, for instance, it will return an string with a certaing message saying that everything went well, or if it will return nothing, etc...

### Server
This is what PROVIDES the functionality. Whatever you want your Service to do, you have to place it in the Service Server.

```python
#! /usr/bin/env python

import rospy
from std_srvs.srv import Empty, EmptyResponse

def my_callback(request):
    print "My_callback has been called"
    return EmptyResponse() # the service Response class, in this case EmptyResponse

rospy.init_node('service_server') 
my_service = rospy.Service('/my_service', Empty , my_callback) # create the Service called my_service with the defined callback
rospy.spin() # maintain the service open.
```
### Custom Service Messages
In order to create a service message, you will have to follow the next steps 
- **Create a `srv` folder in your package directory**
- **Create a new file named `MyCustomServiceMessage.srv` inside the srv folder.**
- `MyCustomServiceMessage.srv` should contain the message structure for example
	```
	int32 duration  
	---
	bool success
	```
- **Edit the CMakeLists.txt - find_package()**
This is where all the packages required to COMPILE the messages of the topics, services, and actions go. In package.xml, you have to state them as build_depend.
```
find_package(catkin REQUIRED COMPONENTS
     rospy
     std_msgs
     message_generation   # Add message_generation here, after the other packages
)
```
- **Edit the CMakeLists.txt - add_service_files()** 
This function includes all of the service messages of this package (in the srv folder) to be compiled. The file should look like this.
	```
	add_service_files(
		FILES
		MyCustomServiceMessage.srv
	  ) # Dont Forget to UNCOMENT the parenthesis and add_message_files TOO
	```
- **Edit the CMakeLists.txt - generate_messages()** 
Here is where the packages needed for the service messages compilation are imported.
	```
	generate_messages(
		DEPENDENCIES
		std_msgs
	) # Dont Forget to uncoment here TOO
	```
- **Edit the CMakeLists.txt - catkin_package()** 
State here all of the packages that will be needed by someone that executes something from your package. All of the packages stated here must be in the package.xml as exec_depend.
	```
	catkin_package(
		CATKIN_DEPENDS rospy message_runtime   # This will NOT be the only thing here
	)
	```
- **Edit the package.xml**
Just add these 3 lines to the package.xml file.
	```
	<build_depend>message_generation</build_depend> 
	<build_export_depend>message_runtime</build_export_depend>
	<exec_depend>message_runtime</exec_depend>
	```
- **Compile**
	```
	roscd; cd ..
	catkin_make
	source devel/setup.bash
	```
- **Verification**
`rossrv show package_name/MyCustomServiceMessage`        
  ```
  [package_name/MyCustomServiceMessage]:   
  int32 duration
  ---
  bool success
  ```
- **Using these in ROS Nodes**
	
	```python
	from package_name.srv import MyCustomServiceMessage, MyCustomServiceRequest/Responce
	```


## Actions
Actions are like asynchronous calls to services, therefore are very similar to services. When you call an action, you are calling a functionality that another node is providing. Just the same as with services. The difference is that when your node calls a service, it must wait until the service finishes. When your node calls an action, it doesn't necessarily have to wait for the action to complete.

Hence, an action is an asynchronous call to another node's functionality.

The node that provides the functionality has to contain an action server. The action server allows other nodes to call that action functionality.
The node that calls to the functionality has to contain an action client. The action client allows a node to connect to the action server of another node.

When a robot provides an action, you will see that in the topics list. There are 5 topics with the same base name, and with the subtopics **cancel, feedback, goal, result, and status.**

**For example, here the name of the action server is "ardrone_action_server":**

	```bash
	user ~ $ rostopic list
	...
	...
	/ardrone_action_server/cancel
	/ardrone_action_server/feedback
	/ardrone_action_server/goal
	/ardrone_action_server/result
	/ardrone_action_server/status
	...
	```
### Calling an Action Server
Calling an action server means sending a message to it. In the same way as with topics and services, it all works by passing messages around.

- The message of a topic is composed of a single part: the information the topic provides.
- The message of a service has two parts: the request and the response.
- The message of an action server is divided into three parts: the goal, the result, and the feedback.

For example, here is the message structure of an action server:

```bash
user ~ $ roscd ardrone_as/action; cat Ardrone.action
#goal for the drone
int32 nseconds  # the number of seconds the drone will be taking pictures
---
#result
sensor_msgs/CompressedImage[] allPictures # an array containing all the pictures taken along the nseconds
---
#feedback
sensor_msgs/CompressedImage lastImage  # the last image taken
```
### Feedback
Due to the fact that calling an action server does not interrupt your thread, action servers provide a message called the feedback. The feedback is a message that the action server generates every once in a while to indicate how the action is going (informing the caller of the status of the requested action). It is generated while the action is in progress.

### Working Explained
So, whenever an action server is called, the sequence of steps are as follows:

1) When an **action client** calls an **action server** from a node, what actually happens is that the **action client** sends to the **action server** the goal requested through the **/ardrone_action_server/goal** topic.

2) When the **action server** starts to execute the goal, it sends to the **action client** the feedback through the **/ardrone_action_server/feedback** topic.

3) Finally, when the **action server** has finished the goal, it sends to the **action client** the result through the **/ardrone_action_server/result** topic.

### Sending Goals via terminal
Each one of those three topics have their own type of message. The type of the message is built automatically by ROS from the .action file.

For example, in the case of the **ardrone_action_server** the action file is called **Ardrone.action**.

When you compile the package (with catkin_make), ROS will generate the following types of messages from the **Ardrone.action** file:
- ArdroneActionGoal
- ArdroneActionFeedback
- ArdroneActionResult
- ArdroneAction
- ArdroneGoal
- ArdroneResult
- ArdroneFeedback

Each topic of the action server uses its associated type of message accordingly.

**To send goals via the terminal:**

`rostopic pub /name_of_action_server/goal /type_of_the_message_used_by_the_topic parameters`

### Client
```python
#! /usr/bin/env python
import rospy
import time
import actionlib
from ardrone_as.msg import ArdroneAction, ArdroneGoal, ArdroneResult, ArdroneFeedback

nImage = 1

# definition of the feedback callback. This will be called when feedback
# is received from the action server
# it just prints a message indicating a new message has been received
def feedback_callback(feedback):
	global nImage
	print('[Feedback] image n.%d received'%nImage)
	nImage += 1

# initializes the action client node
rospy.init_node('drone_action_client')

# create the connection to the action server
client = actionlib.SimpleActionClient('/ardrone_action_server', ArdroneAction)
# waits until the action server is up and running
client.wait_for_server()

# creates a goal to send to the action server
goal = ArdroneGoal()
goal.nseconds = 10 # indicates, take pictures along 10 seconds

# sends the goal to the action server, specifying which feedback function
# to call when feedback received
client.send_goal(goal, feedback_cb=feedback_callback)

# Uncomment these lines to test goal preemption:
#time.sleep(3.0)
#client.cancel_goal()  # would cancel the goal 3 seconds after starting

# wait until the result is obtained
# you can do other stuff here instead of waiting
# and check for status from time to time 
# status = client.get_state()
# check the client API link below for more info

client.wait_for_result()

print('[Result] State: %d'%(client.get_state()))
```
### How to perform other tasks while the Action is in progress
So, the SimpleActionClient objects have two functions that can be used for knowing if the action that is being performed has finished, and how:

1) **wait_for_result():** This function is very simple. When called, it will wait until the action has finished and returns a true value. As you can see, it's useless if you want to perform other tasks in parallel because the program will stop there until the action is finished.

2) **get_state():** This function is much more interesting. When called, it returns an integer that indicates in which state is the action that the SimpleActionClient object is connected to.

- 0 ==> PENDING
- 1 ==> ACTIVE
- 2 ==> DONE
- 3 ==> WARN
- 4 ==> ERROR

This allows you to create a while loop that checks if the value returned by get_state() is 2 or higher. If it is not, it means that the action is still in progress, so you can keep doing other things.

### Preempting a goal
It happens that you can cancel a goal previously sent to an action server prior to its completion. Cancelling a goal while it is being executed is called preempting a goal

You may need to preempt a goal for many reasons, like, for example, the robot went mad about your goal and it is safer to stop it prior to the robot doing some harm.

In order to preempt a goal, you send the cancel_goal to the server through the client connection.

`client.cancel_goal()`

### The axclient
The axclient is, basically, a GUI tool provided by the actionlib package, that allows you to interact with an Action Server in a very easy and visual way.

**The command used to launch the axclient is the following:**

`rosrun actionlib axclient.py /name_of_action_server`

### Server
```python
#! /usr/bin/env python

import rospy
import time
from std_msgs.msg import Empty
from actions_quiz.msg import CustomActionMsgAction, CustomActionMsgGoal, CustomActionMsgFeedback
import actionlib

class DroneAction(object):
    feedbackM = CustomActionMsgFeedback()
    goalM = CustomActionMsgGoal()
    emp = Empty()

    def __init__(self):
        self.success = True
        self.pub_takeoff = rospy.Publisher('drone/takeoff',Empty,latch=True,queue_size=1)
        self.pub_land = rospy.Publisher('drone/land',Empty,latch=True,queue_size=1)
        self.server = actionlib.SimpleActionServer('/action_custom_msg_as',CustomActionMsgAction,self.goal_callback,False)
        self.server.start()


    def goal_callback(self,goal):

        if self.server.is_preempt_requested():
                rospy.loginfo('asked to quit')
                self.server.set_preempted()
                self.success = False

        else :
            if goal.goal == 'TAKEOFF':
                self.pub_takeoff.publish(self.emp)
            if goal.goal == 'LAND':
                self.pub_land.publish(self.emp)
            self.feedbackM.feedback = goal.goal
            self.server.publish_feedback(self.feedbackM)
            rospy.sleep(1)

        if self.success:
            self.result = self.emp
            self.server.set_succeeded(self.result)


if __name__ == '__main__':
  rospy.init_node('server_noder')
  DroneAction()
  rospy.spin()
```
Once the server is launched you should be able to see the following:

```bash
rostopic list | grep action_custom_msg_as
    /action_custom_msg_as/cancel
    /action_custom_msg_as/feedback
    /action_custom_msg_as/goal
    /action_custom_msg_as/result
    /action_custom_msg_as/status
```
### Custom Action Messages
In order to create a actiob message, you will have to follow the next steps:

- **Create a action folder in your package directory**
- **Create a new file named Name.action inside the action folder.**
- `Name.action` should contain the message structure for example
	```
	int32 duration #Goal   
	---   
	bool success #Result   
	---   
	int32 current_time #Feedback
	```
- **Edit the CMakeLists.txt - find_package()**
This is where all the packages required to COMPILE the messages of the topics, services, and actions go. In package.xml, you have to state them as build_depend.
	```
	find_package(catkin REQUIRED COMPONENTS
		 rospy
		 actionlib_msgs
	)
	```
- **Edit the CMakeLists.txt - add_action_files()** 
This function includes all of the action messages of this package (in the action folder) to be compiled. The file should look like this.
	```
	add_action_files(
		FILES
		Name.action
	  ) # Dont Forget to UNCOMENT the parenthesis
	```
- **Edit the CMakeLists.txt - generate_messages()**
Here is where the packages needed for the service messages compilation are imported.

	```
	generate_messages(
		DEPENDENCIES
		actionlib_msgs
	) # Dont Forget to uncoment here TOO
	```
- **Edit the CMakeLists.txt - catkin_package()** 
State here all of the packages that will be needed by someone that executes something from your package. All of the packages stated here must be in the package.xml as exec_depend.

	```
	catkin_package(
		CATKIN_DEPENDS rospy message_runtime   # This will NOT be the only thing here
	)
	```
- **Edit the package.xml**
Just add these 3 lines to the package.xml file.
	```
	<build_depend>actionlib</build_depend>
	<build_depend>actionlib_msgs</build_depend>
	<build_export_depend>actionlib</build_export_depend>
	<build_export_depend>actionlib_msgs</build_export_depend>
	<exec_depend>actionlib</exec_depend>
	<exec_depend>actionlib_msgs</exec_depend>
	```
- **Compile**
	```
	roscd; cd ..
	  catkin_make
	  source devel/setup.bash
	```
- **Verification**

	```
	rosmsg list | grep Name          
	  my_custom_action_msg_pkg/NameAction   
	  my_custom_action_msg_pkg/NameActionFeedback  
	  my_custom_action_msg_pkg/NameActionGoal  
	  my_custom_action_msg_pkg/NameActionResult  
	  my_custom_action_msg_pkg/NameFeedback  
	  my_custom_action_msg_pkg/NameGoal   
	  my_custom_action_msg_pkg/NameResult
	```
- **Using these in ROS Nodes**
```python
from my_custom_action_msg_pkg.msg import NameAction, NameGoal, NameFeedback, NameResult
```