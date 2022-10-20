# WEEK 4 : 

# Turtlesim and RQT
# Using colcon to build packages

## Turtlesim and RQT

Before starting a Turtlesim installation we have to make sure that the Terminal is in ROS2 DISTRO.

to check our Terminal's path we need following command.

```
printenv | grep -i ROS
```
![image](https://user-images.githubusercontent.com/92859942/194726415-ebd46ed1-0e2d-431c-a31b-57087042ac9c.png)

## 1. Install Turtlesim

After making sure that you are in ROS2 Distro, install Turtlesim package.for this process command are below

```
sudo apt update
sudo apt install ros-foxy-turtlesim
```
![image](https://user-images.githubusercontent.com/92859942/194727517-30694e69-6829-4e96-a39b-5e2b84630406.png)

to check list of installed packages 

```
ros2 pkg executables turtlesim
```
![image](https://user-images.githubusercontent.com/92859942/194727573-3207423f-2291-4659-8890-385f12f388e9.png)

## 2. Start Turtlesim

to start turtlesim , we need following command 

```
ros2 run turtlesim turtlesim_node
```
the new window will appear 

![image](https://user-images.githubusercontent.com/92859942/194727640-1b2c9a6c-248c-4efe-96fd-4dd24693eb2e.png)

in the terminal we see following message 
![image](https://user-images.githubusercontent.com/92859942/194727704-769480f1-c725-45f8-b744-922378728257.png)

## 3. Use Turtlesim

firstly ,Open a new terminal
secondly, Make sure you are in ROS2 Distro

```
printenv | grep -i ROS
```
![image](https://user-images.githubusercontent.com/92859942/194727808-5736050c-a378-4d4f-9644-f5d0ebe49d2e.png)

after sourcing our files run a new node to control the turtle in the first mode 

```
ros2 run turtlesim turtle_teleop_key
```
![image](https://user-images.githubusercontent.com/92859942/194727871-6ddf4b2b-b704-4f2a-928b-1886b74212c6.png)



## 4. Install RQT

in a new terminal install the required rqt and its plugins
 
 ```
 sudo apt update
sudo apt install ~nros-foxy-rqt*
```

to run rqt 
```
rqt
```
![image](https://user-images.githubusercontent.com/92859942/194727999-4e9f1913-e417-4870-88db-aead15354ff6.png)

## 5. USE RQT 
plugins>services> service celler 
we can see service clear 

for spawn , in service we need to chooose spawn which will create another turtle 
![image](https://user-images.githubusercontent.com/92859942/194728255-6503e9ee-e989-4e9d-b890-12f2f35cf3ba.png)

give new name to the turtle and enter new coordinates,new turtle is appear in the screen 

![image](https://user-images.githubusercontent.com/92859942/194758469-1901d141-1485-47a0-b8c5-1201286a8e46.png)


## Try the set_pen service

give turtle2 a unique pen using the /set_pen service:

we changed the value r=255 and width=5 , if we press arrow key in terminal the size will changes as following 

![image](https://user-images.githubusercontent.com/92859942/194758717-9062b53e-c315-4eaf-a556-2fdc106a6fbb.png)

## 6.Remapping

after entering the following command we can move the turtle2 bye arrows keys 

```
ros2 run turtlesim turtle_teleop_key --ros-args --remap turtle1/cmd_vel:=turtle2/cmd_vel
```


![image](https://user-images.githubusercontent.com/92859942/194758876-eda8b3fe-9687-47d3-9cc6-ebbb58599488.png)

## 7.Close Turtlesim
To stop the simulation, you can enter Ctrl + C in the turtlesim_node terminal, and q in the teleop terminal.

# Using colcon to build packages 

## Background

Iterations of the ROS build tools like catkin make, catkin make isolated, catkin tools, and ament tools include colcon.  

## Prerequisites 

## Install colcon

```
sudo apt install python3-colcon-common-extensions
```
![image](https://user-images.githubusercontent.com/92859942/194816252-1e986b97-08cb-43bf-a8d9-e3c5c32080a8.png)


## Install ROS

 in order to build the example we must set ROS 2.

## Create a workspace 

To build  our workspace, we need to create the directory ros2 ws:

```
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```
![image](https://user-images.githubusercontent.com/92859942/194816321-06ff339f-7c9b-4506-b21b-393db63612a1.png)


The workspace currently only has the empty directory src. 

## Add some sources

![image](https://user-images.githubusercontent.com/92859942/194818010-3435dcd9-77e7-4dab-8397-4896b5978a68.png):

```
git clone https://github.com/ros2/examples src/examples -b foxy
```
![image](https://user-images.githubusercontent.com/92859942/194816461-82c17358-5274-48d0-8b05-d61509fdde86.png)

The source code for the ROS 2 examples should now be in the workspace:

```
└── src
    └── examples
        ├── CONTRIBUTING.md
        ├── LICENSE
        ├── rclcpp
        ├── rclpy
        └── README.md

4 directories, 3 files
```

## Build the workspace

```
colcon build --symlink-install
```
![image](https://user-images.githubusercontent.com/92859942/194816739-d2ecf741-9fd8-42c3-94ac-097e6f9c07cf.png)


We should see the build, install, and log directories once the build is complete:
```
.
├── build
├── install
├── log
└── src

4 directories, 0 files
```
## Run tests
Test the newly created packages by executing the following:

```
colcon test
```
![image](https://user-images.githubusercontent.com/92859942/194817137-4a08ae4a-18a4-441a-8397-d2b3a692a27d.png)

## Source the environment

```
. install/setup.bash
```

# Try a demo

Colcon's executables can be run using the provided environment. Let's examine one of the subscriber nodes in the examples:

```
ros2 run examples_rclcpp_minimal_subscriber subscriber_member_function
```
![image](https://user-images.githubusercontent.com/92859942/194817394-f67439fd-6fe3-46d1-98bb-200cac8dd941.png)


now we are ready tolaunch a publisher node in another terminal 

```
ros2 run examples_rclcpp_minimal_publisher publisher_member_function
```
![image](https://user-images.githubusercontent.com/92859942/194817458-0e69eae8-a75c-4e4a-b9be-0c855c530f8e.png)

we can see a messages from the publisher and subscriber with numbers incrementing.

# Create your own package
```
echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc
echo "export _colcon_cd_root=/opt/ros/foxy/" >> ~/.bashrc
```

## Setup colcon tab completion

```
echo "source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash" >> ~/.bashrc
```
![image](https://user-images.githubusercontent.com/92859942/194817643-8d97107c-fbcc-46f9-b585-0d5843560be2.png)

----------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------

# WEEK-5 : 
    ## A Simple Publisher and Subscriber
    ## A Simple Service and Client
    ## Creating custom msg and srv files
    ## Test the new interfaces
    ## Implementing custom interfaces

# A Simple Publisher and Subscriber

## 1. Create a package

in the ros2 ws/src Run the package creation

```
ros2 pkg create --build-type ament_python py_pubsub
```
 terminal will display a message confirming the creation of package py pubsub and all of its necessary files and folders.
 
 ## 2. Write the publisher node
 
 we can download the example talker code by going to ros2 ws/src/py pubsub/py pubsub and typing the following command:
 
 ```
wgethttps://raw.githubusercontent.com/ros2/examples/foxy/rclpy/topics/minimal_publisher/examples_rclpy_minimal_publisher/publisher_member_function.py
```
![image](https://user-images.githubusercontent.com/92859942/194820798-ebd90a9c-5f13-46cb-b3a9-35fa0644946b.png)


 Open the file in your preferred text editor. The __init.py file will now be followed by a new one called publisher member function.py.
 
 ```
 import rclpy
from rclpy.node import Node

from std_msgs.msg import String


class MinimalPublisher(Node):

    def __init__(self):
        super().__init__('minimal_publisher')
        self.publisher_ = self.create_publisher(String, 'topic', 10)
        timer_period = 0.5  # seconds
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = String()
        msg.data = 'Hello World: %d' % self.i
        self.publisher_.publish(msg)
        self.get_logger().info('Publishing: "%s"' % msg.data)
        self.i += 1


def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_publisher.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
 ```
 
 ## 2.1 Add dependencies
    
Setup.py, setup.cfg, and package.xml files already produced for you in ros2 ws/src/py pubsub will be returned.
    
Be sure to fill in all the tags in package.xml, including description>, maintainer>, and license>.
    
 ```
   <description>Examples of minimal publisher/subscriber using rclpy</description>
<maintainer email="you@email.com">Your Name</maintainer>
<license>Apache License 2.0</license>
```

we need to add the following dependencies after the import declarations for your node

```
<exec_depend>rclpy</exec_depend>
<exec_depend>std_msgs</exec_depend>
```
![image](https://user-images.githubusercontent.com/92859942/194821468-308e1455-b9fd-42e2-9f6c-72132ecc902e.png)

To run the package's code, rclpy and standard messages are required.
make sure to save the file 

## 2.2 Add an entry point

Check setup.py.Double-check package.xml to be sure its maintainer, maintainer email, description, and license columns are correct.

```
maintainer='YourName',
maintainer_email='you@email.com',
description='Examples of minimal publisher/subscriber using rclpy',
license='Apache License 2.0',
```
Add the next line to the entry points field between the console scripts brackets:

```
entry_points={
        'console_scripts': [
                'talker = py_pubsub.publisher_member_function:main',
        ],
},
```
![image](https://user-images.githubusercontent.com/92859942/194822682-d2169521-7ba9-49d9-9853-cade3406f1b8.png)

we need to save here as well 


## 2.3 Check setup.cfg

the following command should use first 

```
[develop]
script-dir=$base/lib/py_pubsub
[install]
install-scripts=$base/lib/py_pubsub
```

So that ros2 run knows where to find your executables, tell setuptools to place them in the lib directory.If you wanted to see the full system in operation, you could create your package and source the local setup files right now.The subscriber node needs to be established first, however.

## 3 Write the subscriber node

we should create node using following command 

```
wgethttps://raw.githubusercontent.com/ros2/examples/foxy/rclpy/topics/minimal_subscriber/examples_rclpy_minimal_subscriber/subscriber_member_function.py
```
![image](https://user-images.githubusercontent.com/92859942/194822885-ca202986-9f67-4f33-addf-5132a3d63121.png)

below mentioned lines should be in directory 

```
__init__.py  publisher_member_function.py  subscriber_member_function.py
```

in the text editor navigate to subscriber member function.py.

```
import rclpy
from rclpy.node import Node

from std_msgs.msg import String


class MinimalSubscriber(Node):

    def __init__(self):
        super().__init__('minimal_subscriber')
        self.subscription = self.create_subscription(
            String,
            'topic',
            self.listener_callback,
            10)
        self.subscription  # prevent unused variable warning

    def listener_callback(self, msg):
        self.get_logger().info('I heard: "%s"' % msg.data)


def main(args=None):
    rclpy.init(args=args)

    minimal_subscriber = MinimalSubscriber()

    rclpy.spin(minimal_subscriber)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_subscriber.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```
    
    
## 3.1 Add an entry point

Delete the entry point for the publisher and reopen setup.py with an entry point for the subscriber below it.You should now see the following entry points in the entry points field:

```
entry_points={
        'console_scripts': [
                'talker = py_pubsub.publisher_member_function:main',
                'listener = py_pubsub.subscriber_member_function:main',
        ],
},
```
![image](https://user-images.githubusercontent.com/92859942/194823251-a29af71b-984f-4f13-be9c-207eb35d4dba.png)

after saving the system should function

# 4 Build and Run

after rclpy and std mags already installed, we need first to check the any indepencies are missing or not 

```
rosdep install -i --from-path src --rosdistro foxy -y
```

Still in the root of your workspace, ros2_ws, build your new package:

```
colcon build --packages-select py_pubsub
```
![image](https://user-images.githubusercontent.com/92859942/194831334-30912a35-4222-4503-95da-64f6a0b27871.png)


Navigate to ros2 ws in a new terminal, then source the setup files and run the talker mode 

```
. install/setup.bash
```
```
ros2 run py_pubsub talker
```

we can see the terminal sending the following message 

```
[INFO] [minimal_publisher]: Publishing: "Hello World: 0"
[INFO] [minimal_publisher]: Publishing: "Hello World: 1"
[INFO] [minimal_publisher]: Publishing: "Hello World: 2"
[INFO] [minimal_publisher]: Publishing: "Hello World: 3"
[INFO] [minimal_publisher]: Publishing: "Hello World: 4"
```
![image](https://user-images.githubusercontent.com/92859942/194831442-81b91ccf-496c-4675-8bfb-5b3c08752c45.png)


in short time, the terminal starts the informational messages as below and listener begins writing message to the console starting at the publisher's current message count as follows:

```
ros2 run py_pubsub listener
```

```
[INFO] [minimal_subscriber]: I heard: "Hello World: 10"
[INFO] [minimal_subscriber]: I heard: "Hello World: 11"
[INFO] [minimal_subscriber]: I heard: "Hello World: 12"
[INFO] [minimal_subscriber]: I heard: "Hello World: 13"
[INFO] [minimal_subscriber]: I heard: "Hello World: 14"
```
in this cace , ctrl+c will stop the nodes progress.



# A Simple Service and Client

## 1. create package

in terminal we need to run package creation command 

```
ros2 pkg create --build-type ament_python py_srvcli --dependencies rclpy example_interfaces
```
we will see the conformation 

![image](https://user-images.githubusercontent.com/92859942/194831723-14c1d311-ba4b-42ae-8a20-9668b390675c.png)

## 1.1 update(package.xml) 

we should always remember to include the description, license information, and the name and email of the maintainer in package.xml. but we dont need to manually add dependencies to package.xml.

```
<description>Python client server tutorial</description>
<maintainer email="you@email.com">Your Name</maintainer>
<license>Apache License 2.0</license>
```
![image](https://user-images.githubusercontent.com/92859942/194832328-009297dc-0f7f-432f-a1f5-fd0af93e63db.png)


## 1.2 Update (setup.py)


details should be added to the setup.py file's description, maintainer, maintainer email, and license fields

```
maintainer='Your Name',
maintainer_email='you@email.com',
description='Python client server tutorial',
license='Apache License 2.0',
```
![image](https://user-images.githubusercontent.com/92859942/194832769-09ef8dcf-d327-4dcd-81a9-7538533b961b.png)

# 2 Write the service node

we need to make new file called function.py, and run the following code. 

```
from example_interfaces.srv import AddTwoInts

import rclpy
from rclpy.node import Node


class MinimalService(Node):

    def __init__(self):
        super().__init__('minimal_service')
        self.srv = self.create_service(AddTwoInts, 'add_two_ints', self.add_two_ints_callback)

    def add_two_ints_callback(self, request, response):
        response.sum = request.a + request.b
        self.get_logger().info('Incoming request\na: %d b: %d' % (request.a, request.b))

        return response


def main(args=None):
    rclpy.init(args=args)

    minimal_service = MinimalService()

    rclpy.spin(minimal_service)

    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

## 2.1 Add an entry point

the entry point must be added to be able to run node located in the ros2 ws/src/py srvcli directory

insert the code between the "console scripts" brackets

```
'service = py_srvcli.service_member_function:main',
```
![image](https://user-images.githubusercontent.com/92859942/194835145-5bbfd63b-8a31-4a22-a966-e19c06c8241b.png)

## 3 Write the client node

![image](https://user-images.githubusercontent.com/92859942/194834297-f7060b85-519d-4226-8945-16f92a5b1ad1.png)

again we need to make new file called client member  function.py  and use the code mentioned below .

```
import sys

from example_interfaces.srv import AddTwoInts
import rclpy
from rclpy.node import Node


class MinimalClientAsync(Node):

    def __init__(self):
        super().__init__('minimal_client_async')
        self.cli = self.create_client(AddTwoInts, 'add_two_ints')
        while not self.cli.wait_for_service(timeout_sec=1.0):
            self.get_logger().info('service not available, waiting again...')
        self.req = AddTwoInts.Request()

    def send_request(self, a, b):
        self.req.a = a
        self.req.b = b
        self.future = self.cli.call_async(self.req)
        rclpy.spin_until_future_complete(self, self.future)
        return self.future.result()


def main(args=None):
    rclpy.init(args=args)

    minimal_client = MinimalClientAsync()
    response = minimal_client.send_request(int(sys.argv[1]), int(sys.argv[2]))
    minimal_client.get_logger().info(
        'Result of add_two_ints: for %d + %d = %d' %
        (int(sys.argv[1]), int(sys.argv[2]), response.sum))

    minimal_client.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

## 3.1 Add an entry point


In the same way that the service node requires an entry point, the client node also does.It is important to format your setup.py file's entry points column the following way:


```
entry_points={
    'console_scripts': [
        'service = py_srvcli.service_member_function:main',
        'client = py_srvcli.client_member_function:main',
    ],
},
```
![image](https://user-images.githubusercontent.com/92859942/194835869-1e8769e6-78d4-4991-97aa-c202e0f99867.png)


## 4 Build and Run
we need to check any dependencies are missing or not 

```
rosdep install -i --from-path src --rosdistro foxy -y
```

now we able to create own package 

```
colcon build --packages-select py_srvcli
```

in the new terminal source the setup files and run the service node right after 

```
. install/setup.bash
```

```
ros2 run py_srvcli service
```

![image](https://user-images.githubusercontent.com/92859942/194839726-e1ab4c3d-89c7-44d5-8dc7-66072ae7343f.png)

Until a request is made by the client, the node will hold off.Open a new terminal and re-source the setup files from ros2 ws.Two integers, separated by a space, and the client node.


```
ros2 run py_srvcli client 2 3
```
![image](https://user-images.githubusercontent.com/92859942/194839816-d0790efd-8156-4660-ab6e-87da06bd0928.png)

the customer will receive the response if we choose 2 or 3 option 

```
[INFO] [minimal_client_async]: Result of add_two_ints: for 2 + 3 = 5
```

in servive node running terminal it will published the following log statements after receiving the request

```
[INFO] [minimal_service]: Incoming request
a: 2 b: 3
```

to stop the nodes from rotating ctrl+c command is used. 


# Creating custom msg and srv files

## 1 Create a new package

Navigate into ros2_ws/src and run the package creation command:

```
ros2 pkg create --build-type ament_cmake tutorial_interfaces
```

Upon establishing your package tutorial interfaces and all necessary files and folders, a message will appear on your terminal.It should be noted that this is a CMake package since Python packages are unable to generate .msg or .srv files.A Python node can use a custom interface you create in a CMake package, which will be discussed in the last section.

The directories should be made in the ros2 ws/src/tutorial interfaces.

```
mkdir msg

mkdir srv
```
![image](https://user-images.githubusercontent.com/92859942/194840895-69308228-2cd5-4356-a9ce-7685bb1ae08f.png)

## 2 Create custom definitions

## 2.1 msg definition

in new file named Num.msg add single line of code which describe the data structure 

```
int64 num
```

This custom message sends a single value, the 64-bit integer num.

In the directory we just created for the tutorial interfaces/msg, make a new file called Sphere.msg and use command :

```
geometry_msgs/Point center
float64 radius
```

A message from a different message package—in this case, geometry msgs/Point—is used in this custom message.

## 2.2 srv definition

In the instructional interfaces/srv directory, new file should created named 
AddThreeInts.srv with following structure 

```
int64 a
int64 b
int64 c
---
int64 sum
```
This custom service accepts the three integers a, b, and c and provides the answer's integer sum.

![image](https://user-images.githubusercontent.com/92859942/194843782-cf0f9aa2-ba12-4161-99b6-6b0a983cf65d.png)

## 3 CMakeLists.txt

The following lines in CMakeLists.txt will translate the interfaces you created into code that can be used in C++ and Python:

```
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/Num.msg"
  "msg/Sphere.msg"
  "srv/AddThreeInts.srv"
  DEPENDENCIES geometry_msgs # Add packages that above messages depend on, in this case geometry_msgs for Sphere.msg
)
```
![image](https://user-images.githubusercontent.com/92859942/194844391-17978213-b921-437b-9307-7e3ded38d936.png)

## 4 package.xml

```
<depend>geometry_msgs</depend>

<build_depend>rosidl_default_generators</build_depend>

<exec_depend>rosidl_default_runtime</exec_depend>

<member_of_group>rosidl_interface_packages</member_of_group>
```


here in package.xml, added a above command .

## 5 Build the tutorial_interfaces package


we may now construct our own interfaces package as all of its components are in place. In the workspace's root directory (/ros2 ws), issue the following command:
and other ROS2 application will be able to locate the interface 

```
colcon build --packages-select tutorial_interfaces
```

![image](https://user-images.githubusercontent.com/92859942/194845223-490653a2-c8f6-4b92-8d80-d4b6b9c84f20.png)

## 6 Confirm msg and srv creation

Use the following command from within your workspace (ros2 ws) to source it in a new terminal, after that next command helps to check your interface creation was successful .

```
. install/setup.bash
```

```
ros2 interface show tutorial_interfaces/msg/Num
```

use the command one by one which should return and so on . 

```
int64 num
```

```
ros2 interface show tutorial_interfaces/msg/Sphere
```

```
geometry_msgs/Point center
        float64 x
        float64 y
        float64 z
float64 radius
```
```
ros2 interface show tutorial_interfaces/srv/AddThreeInts
```
```
int64 a
int64 b
int64 c
---
int64 sum
```
![image](https://user-images.githubusercontent.com/92859942/194845600-f4f03c68-4b68-4112-a8bd-8ea2f00477f1.png)


## 7 Test the new interfaces

here we can make use of package created earlier, the process to enable package file to use new interface is by adjustments to the nodes, CMakeLists .

# 7.1 Testing Num.msg with pub/sub
we  can see Num.msg in action by making a few minor adjustments to the publisher/subscriber package developed in a prior course (in C++ or Python). our decision to switch from the default textual message to a numerical one will somewhat alter the outcome.

publisher : 

```
import rclpy
from rclpy.node import Node

from tutorial_interfaces.msg import Num    # CHANGE


class MinimalPublisher(Node):

    def __init__(self):
        super().__init__('minimal_publisher')
        self.publisher_ = self.create_publisher(Num, 'topic', 10)     # CHANGE
        timer_period = 0.5
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = Num()                                           # CHANGE
        msg.num = self.i                                      # CHANGE
        self.publisher_.publish(msg)
        self.get_logger().info('Publishing: "%d"' % msg.num)  # CHANGE
        self.i += 1


def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    minimal_publisher.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

subscriber :

```
import rclpy
from rclpy.node import Node

from tutorial_interfaces.msg import Num        # CHANGE


class MinimalSubscriber(Node):

    def __init__(self):
        super().__init__('minimal_subscriber')
        self.subscription = self.create_subscription(
            Num,                                              # CHANGE
            'topic',
            self.listener_callback,
            10)
        self.subscription

    def listener_callback(self, msg):
            self.get_logger().info('I heard: "%d"' % msg.num) # CHANGE


def main(args=None):
    rclpy.init(args=args)

    minimal_subscriber = MinimalSubscriber()

    rclpy.spin(minimal_subscriber)

    minimal_subscriber.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```
CMakeLists.txt:

Add the following lines (C++ only):

```
#...

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(tutorial_interfaces REQUIRED)                         # CHANGE

add_executable(talker src/publisher_member_function.cpp)
ament_target_dependencies(talker rclcpp tutorial_interfaces)         # CHANGE

add_executable(listener src/subscriber_member_function.cpp)
ament_target_dependencies(listener rclcpp tutorial_interfaces)     # CHANGE

install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME})

ament_package()
```
![image](https://user-images.githubusercontent.com/92859942/194846662-082ca9de-f5dd-481d-b6c7-3d09aa018aee.png)

package.xml:
after adding the below mentioned line we can create the package after making adjustment and save the work.

```
<exec_depend>tutorial_interfaces</exec_depend>
```

```
colcon build --packages-select py_pubsub
```

in the new window we can add following command followed by opening the two terminal and run the ros2 ws in each by using given command 

```
colcon build --merge-install --packages-select py_pubsub
```

```
ros2 run py_pubsub talker
```
![image](https://user-images.githubusercontent.com/92859942/194846960-86ce7059-12e0-4168-81cd-f773d82e3707.png)

```
ros2 run py_pubsub listener

```

The talker should only be transmitting integer values, as opposed to the text it previously broadcast as Num.msg only transmits an integer:

![image](https://user-images.githubusercontent.com/92859942/194846859-adb6cb76-ad08-4ffb-8a55-43d1f0dbc0f3.png)

```
[INFO] [minimal_publisher]: Publishing: '0'
[INFO] [minimal_publisher]: Publishing: '1'
[INFO] [minimal_publisher]: Publishing: '2'
```

## 7.2 Testing AddThreeInts.srv with service/client

By making a few minor adjustments to the service/client package developed in a prior lesson (in C++ or Python), AddThreeInts.srv may be utilized. The outcome will be very different because you'll be switching from the first two integer request srv to a three integer request srv.

service : 

```
from tutorial_interfaces.srv import AddThreeInts     # CHANGE

import rclpy
from rclpy.node import Node


class MinimalService(Node):

    def __init__(self):
        super().__init__('minimal_service')
        self.srv = self.create_service(AddThreeInts, 'add_three_ints', self.add_three_ints_callback)        # CHANGE

    def add_three_ints_callback(self, request, response):
        response.sum = request.a + request.b + request.c                                                  # CHANGE
        self.get_logger().info('Incoming request\na: %d b: %d c: %d' % (request.a, request.b, request.c)) # CHANGE

        return response

def main(args=None):
    rclpy.init(args=args)

    minimal_service = MinimalService()

    rclpy.spin(minimal_service)

    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

client: 

```
from tutorial_interfaces.srv import AddThreeInts       # CHANGE
import sys
import rclpy
from rclpy.node import Node


class MinimalClientAsync(Node):

    def __init__(self):
        super().__init__('minimal_client_async')
        self.cli = self.create_client(AddThreeInts, 'add_three_ints')       # CHANGE
        while not self.cli.wait_for_service(timeout_sec=1.0):
            self.get_logger().info('service not available, waiting again...')
        self.req = AddThreeInts.Request()                                   # CHANGE

    def send_request(self):
        self.req.a = int(sys.argv[1])
        self.req.b = int(sys.argv[2])
        self.req.c = int(sys.argv[3])                  # CHANGE
        self.future = self.cli.call_async(self.req)


def main(args=None):
    rclpy.init(args=args)

    minimal_client = MinimalClientAsync()
    minimal_client.send_request()

    while rclpy.ok():
        rclpy.spin_once(minimal_client)
        if minimal_client.future.done():
            try:
                response = minimal_client.future.result()
            except Exception as e:
                minimal_client.get_logger().info(
                    'Service call failed %r' % (e,))
            else:
                minimal_client.get_logger().info(
                    'Result of add_three_ints: for %d + %d + %d = %d' %                               # CHANGE
                    (minimal_client.req.a, minimal_client.req.b, minimal_client.req.c, response.sum)) # CHANGE
            break

    minimal_client.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```
CMakeLists.txt:

Add the following lines (C++ only):

```
#...

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(tutorial_interfaces REQUIRED)        # CHANGE

add_executable(server src/add_two_ints_server.cpp)
ament_target_dependencies(server
  rclcpp tutorial_interfaces)                      #CHANGE

add_executable(client src/add_two_ints_client.cpp)
ament_target_dependencies(client
  rclcpp tutorial_interfaces)                      #CHANGE

install(TARGETS
  server
  client
  DESTINATION lib/${PROJECT_NAME})

ament_package()
```

package.xml:
Add the following command :

```
<exec_depend>tutorial_interfaces</exec_depend>
```
After making the aforementioned alterations and saving your work, create the package .

```
colcon build --packages-select py_srvcli
```
![image](https://user-images.githubusercontent.com/92859942/194849463-af6ff6fc-4e55-4b22-a9c1-a535f25f381f.png)

on windows: 

```
colcon build --merge-install --packages-select py_srvcli
```

now we able to luvch two terminal and excute the work 

```
ros2 run py_srvcli service
```
![image](https://user-images.githubusercontent.com/92859942/194849406-373e8c42-7434-42b1-a090-e0cdbcd62fac.png)

```
ros2 run py_srvcli client 2 3 1
```
![image](https://user-images.githubusercontent.com/92859942/194849177-572c320e-ff9e-4ea8-96e2-85592506777c.png)




--------------------------------------------------------------------
------------------------------------------------------------------

# WEEK-6

CONTENT :

 MANAGING DEPENDENCIES WITH ROSDEP
 
 CREATING AN ACTION
 
 WRITING AN ACTION SERVER AND CLIENT 
 
 COMPOSING MULTIPLE NODES IN A SINGLE PROCESS
 
 LAUNCH :
 
     - Creating a launch file.
     -Launching and monitoring multiple nodes
     - Using substitutions
     - Using event handlers


# 1. Managing Dependencies with rosdep

How does the rosdep tool work? We can utilize the software now that we understand the basics of rosdep, package.xml, and rosdistro. Before using rosdep for the first time, it must first be initialized using:

```
sudo rosdep init
rosdep update
```
![image](https://user-images.githubusercontent.com/92859942/196242453-4be81214-cb9e-487e-b88f-176c703afb11.png)


Finally, we could use rosdep install to install dependencies. In a workspace with multiple packages, this is frequently done just once to install all dependencies. If the directory src holding the source code was present in the workspace's root, a call for it may appear as follows.

```
rosdep install --from-paths src -y --ignore-src
```
![image](https://user-images.githubusercontent.com/92859942/196242601-8a0e88f7-56c3-4273-b687-2045933547c1.png)

# creating an action 

## requirenment 

we should have ROS 2 and colcon installed.

Set up a workspace and create a package named action_tutorials_interfaces:

(Remember to source your ROS 2 installation first.)

```
mkdir -p ros2_ws/src #you can reuse existing workspace with this naming convention
cd ros2_ws/src
ros2 pkg create action_tutorials_interfaces
```
![image](https://user-images.githubusercontent.com/92859942/196243171-fb28e9f2-120a-4b66-ace2-d75173749068.png)


# task 

# 1. defining an action 

Actions are described in .action files with the following format:
```
# Request
---
# Result
---
# Feedback
```

n instance of an action is typically referred to as a goal.

Say we want to define a new action “Fibonacci” for computing the Fibonacci sequence.

Create an action directory in our ROS 2 package action_tutorials_interfaces:

```
cd action_tutorials_interfaces
mkdir action
```
![image](https://user-images.githubusercontent.com/92859942/196244819-c8de7edc-47a9-41f1-bb43-d3192b8c9e1a.png)


# 2. Building an Action 
To use the new Fibonacci action in our code, we must send the definition to the Rosidl code. To achieve this, we must insert the lines below before the ament package() line in the action tutorials interfaces of our CMakeLists.txt file.

```
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
  "action/Fibonacci.action"
)
```

![image](https://user-images.githubusercontent.com/92859942/196399859-1850b216-e41d-4f50-b839-eae66b37e20c.png)

We must also include the necessary dependencies in our package.xml file:

```
<buildtool_depend>rosidl_default_generators</buildtool_depend>

<depend>action_msgs</depend>

<member_of_group>rosidl_interface_packages</member_of_group>
```
![image](https://user-images.githubusercontent.com/92859942/196400072-98a5e077-6d92-4968-b69a-72f93def9c51.png)

After all these, we will be able to build the package containing the Fibonacci action definition as follows:

```
# Change to the root of the workspace
cd ~/ros2_ws
# Build
colcon build
```
![image](https://user-images.githubusercontent.com/92859942/196400205-679c41c4-2cfe-4043-a82e-6cb7a2582beb.png)

Using the command line tool, we can verify that our action was built successfully:

```
# Source our workspace
# On Windows: call install/setup.bat
. install/setup.bash
# Check that our action definition exists
ros2 interface show action_tutorials_interfaces/action/Fibonacci
```
![image](https://user-images.githubusercontent.com/92859942/196400347-d41749e6-8623-40e8-ae21-7ca92a9eb7d4.png)

# Writing an action server and client

Here, were create a new file named: fibonacci_action_server.py in the home directory and added the following code:

## A. Writing an Action Server

Here, were create a new file named: fibonacci_action_server.py in the home directory and added the following code:

```
import rclpy
from rclpy.action import ActionServer
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionServer(Node):

    def __init__(self):
        super().__init__('fibonacci_action_server')
        self._action_server = ActionServer(
            self,
            Fibonacci,
            'fibonacci',
            self.execute_callback)

    def execute_callback(self, goal_handle):
        self.get_logger().info('Executing goal...')
        result = Fibonacci.Result()
        return result


def main(args=None):
    rclpy.init(args=args)

    fibonacci_action_server = FibonacciActionServer()

    rclpy.spin(fibonacci_action_server)


if __name__ == '__main__':
    main()
```
![image](https://user-images.githubusercontent.com/92859942/196408665-05016d5a-1579-48c0-89a8-82281b4c7b84.png)

Now lets run our server:

```
python3 fibonacci_action_server.py
```
![image](https://user-images.githubusercontent.com/92859942/196408828-3dca3ca2-da5a-4213-a7bd-1088c66a1c65.png)


We can communicate a goal via the command line interface to another terminal:

```
ros2 action send_goal fibonacci action_tutorials_interfaces/action/Fibonacci "{order: 5}"
```
![image](https://user-images.githubusercontent.com/92859942/196408915-ec7e1ec2-b5f9-4de1-850c-5c0759ad2a0a.png)

In the terminal that is running the action server, you should see the logged message "Executing objective..." followed by a warning that the goal state was not established. If the goal handle state is not set in the execute callback, the aborted state is assumed by default.

To demonstrate that the objective was accomplished, use the successfully() function on the goal handle:

```
def execute_callback(self, goal_handle):
    self.get_logger().info('Executing goal...')

    goal_handle.succeed()

    result = Fibonacci.Result()
    return result
```

![image](https://user-images.githubusercontent.com/92859942/196409881-5735d95b-e904-48c3-a96d-60b1fa6fa9af.png)


You should see the goal completed with the status SUCCEED if you restart the action server and send another goal at this point.

![image](https://user-images.githubusercontent.com/92859942/196410744-0ce7dc67-5180-40c7-bd02-c676b583876c.png)

![image](https://user-images.githubusercontent.com/92859942/196411241-935ba425-5d25-4269-a02f-955dfa40e930.png)

Let's now make sure that our target execution computes and returns the specified Fibonacci sequence:
```
def execute_callback(self, goal_handle):
    self.get_logger().info('Executing goal...')


    sequence = [0, 1]



    for i in range(1, goal_handle.request.order):

        sequence.append(sequence[i] + sequence[i-1])


    goal_handle.succeed()

    result = Fibonacci.Result()

    result.sequence = sequence

    return result
```
![image](https://user-images.githubusercontent.com/92859942/196412099-3ec2fe82-38f2-474d-aea8-ec6b3cc2d3c9.png)


The sequence is calculated, put in the result message field, and we move on to the return.

Restart the action server and send a new goal. The objective must be fulfilled with the anticipated outcomes appearing in the appropriate order. The successfully() function on the goal handle can be used to demonstrate the goal's accomplishment:

![image](https://user-images.githubusercontent.com/92859942/196419464-3c0803f0-cecc-40be-8b14-bbacd0626d8a.png)

![image](https://user-images.githubusercontent.com/92859942/196419527-44e35601-b4a5-455c-900c-454fed01979c.png)


## A.1 publishing feedback: 

By invoking the publsih feedback() function on the goal handle, we can force our action server to publish feedback for action clients.

after using a feedback message to save the sequence in place of the sequence variable. We broadcast the feedback message with each update to the for-loop feedback message:

```
import time


import rclpy
from rclpy.action import ActionServer
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionServer(Node):

    def __init__(self):
        super().__init__('fibonacci_action_server')
        self._action_server = ActionServer(
            self,
            Fibonacci,
            'fibonacci',
            self.execute_callback)

    def execute_callback(self, goal_handle):
        self.get_logger().info('Executing goal...')


        feedback_msg = Fibonacci.Feedback()

        feedback_msg.partial_sequence = [0, 1]


        for i in range(1, goal_handle.request.order):

            feedback_msg.partial_sequence.append(

                feedback_msg.partial_sequence[i] + feedback_msg.partial_sequence[i-1])

            self.get_logger().info('Feedback: {0}'.format(feedback_msg.partial_sequence))

            goal_handle.publish_feedback(feedback_msg)

            time.sleep(1)


        goal_handle.succeed()

        result = Fibonacci.Result()

        result.sequence = feedback_msg.partial_sequence

        return result


def main(args=None):
    rclpy.init(args=args)

    fibonacci_action_server = FibonacciActionServer()

    rclpy.spin(fibonacci_action_server)


if __name__ == '__main__':
    main()
```
After restarting the action server, it is confirmed that feedback is now published by using the command line tool with the --feedback option:

```
ros2 action send_goal --feedback fibonacci action_tutorials_interfaces/action/Fibonacci "{order: 5}"
```
![image](https://user-images.githubusercontent.com/92859942/196525373-16375850-54d0-4876-bd85-3c1dde1780de.png)

![image](https://user-images.githubusercontent.com/92859942/196423218-b616c53d-b6d8-41f0-9ba0-ac8505eedad5.png)


## B. Writing an action client

The action client will also be limited to a single file. Next, create a new file with the name fibonacci action client.py. To the new file, add the following boilerplate code:

![image](https://user-images.githubusercontent.com/92859942/196526351-b9ed22d2-30c1-4e63-914e-1804b06a44a3.png)


```
import rclpy
from rclpy.action import ActionClient
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionClient(Node):

    def __init__(self):
        super().__init__('fibonacci_action_client')
        self._action_client = ActionClient(self, Fibonacci, 'fibonacci')

    def send_goal(self, order):
        goal_msg = Fibonacci.Goal()
        goal_msg.order = order

        self._action_client.wait_for_server()

        return self._action_client.send_goal_async(goal_msg)


def main(args=None):
    rclpy.init(args=args)

    action_client = FibonacciActionClient()

    future = action_client.send_goal(10)

    rclpy.spin_until_future_complete(action_client, future)


if __name__ == '__main__':
    main()
```

![image](https://user-images.githubusercontent.com/92859942/196526226-ecab7673-e459-4bc6-87d5-93fa4b44172f.png)


Let's test our action client by first launching the earlier-built action server:

```
python3 fibonacci_action_server.py
```

Run the action client in an other terminal.

```
python3 fibonacci_action_client.py
```

he action server executes the goal and we are able to see the messages successfully.

The action client start up and quickly finish but we don't get any feedback.

```
[INFO] [fibonacci_action_server]: Executing goal...
[INFO] [fibonacci_action_server]: Feedback: array('i', [0, 1, 1])
[INFO] [fibonacci_action_server]: Feedback: array('i', [0, 1, 1, 2])
[INFO] [fibonacci_action_server]: Feedback: array('i', [0, 1, 1, 2, 3])
[INFO] [fibonacci_action_server]: Feedback: array('i', [0, 1, 1, 2, 3, 5])
# etc.
```

![image](https://user-images.githubusercontent.com/92859942/196529165-c1e40929-d9aa-4d1e-b268-6d1c88cf6b83.png)

## B.1 getting the result 

We need to set a goal handle for the goal we sent and hence here is the complete code for this:

```
import rclpy
from rclpy.action import ActionClient
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionClient(Node):

    def __init__(self):
        super().__init__('fibonacci_action_client')
        self._action_client = ActionClient(self, Fibonacci, 'fibonacci')

    def send_goal(self, order):
        goal_msg = Fibonacci.Goal()
        goal_msg.order = order

        self._action_client.wait_for_server()

        self._send_goal_future = self._action_client.send_goal_async(goal_msg)

        self._send_goal_future.add_done_callback(self.goal_response_callback)

    def goal_response_callback(self, future):
        goal_handle = future.result()
        if not goal_handle.accepted:
            self.get_logger().info('Goal rejected :(')
            return

        self.get_logger().info('Goal accepted :)')

        self._get_result_future = goal_handle.get_result_async()
        self._get_result_future.add_done_callback(self.get_result_callback)

    def get_result_callback(self, future):
        result = future.result().result
        self.get_logger().info('Result: {0}'.format(result.sequence))
        rclpy.shutdown()


def main(args=None):
    rclpy.init(args=args)

    action_client = FibonacciActionClient()

    action_client.send_goal(10)

    rclpy.spin(action_client)


if __name__ == '__main__':
    main()
```

Try running our Fibonacci action client while an action server is active on a different terminal.

```
python3 fibonacci_action_client.py
```

![image](https://user-images.githubusercontent.com/92859942/196529909-83fa97db-60aa-4829-a23f-3aa5cdb0d2c3.png)


## B.2 getting feedback 

Here is the whole code for collecting some feedback regarding the goals we provide from the action server once the action client is allowed to communicate the objectives:

```
import rclpy
from rclpy.action import ActionClient
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionClient(Node):

    def __init__(self):
        super().__init__('fibonacci_action_client')
        self._action_client = ActionClient(self, Fibonacci, 'fibonacci')

    def send_goal(self, order):
        goal_msg = Fibonacci.Goal()
        goal_msg.order = order

        self._action_client.wait_for_server()

        self._send_goal_future = self._action_client.send_goal_async(goal_msg, feedback_callback=self.feedback_callback)

        self._send_goal_future.add_done_callback(self.goal_response_callback)

    def goal_response_callback(self, future):
        goal_handle = future.result()
        if not goal_handle.accepted:
            self.get_logger().info('Goal rejected :(')
            return

        self.get_logger().info('Goal accepted :)')

        self._get_result_future = goal_handle.get_result_async()
        self._get_result_future.add_done_callback(self.get_result_callback)

    def get_result_callback(self, future):
        result = future.result().result
        self.get_logger().info('Result: {0}'.format(result.sequence))
        rclpy.shutdown()

    def feedback_callback(self, feedback_msg):
        feedback = feedback_msg.feedback
        self.get_logger().info('Received feedback: {0}'.format(feedback.partial_sequence))


def main(args=None):
    rclpy.init(args=args)

    action_client = FibonacciActionClient()

    action_client.send_goal(10)

    rclpy.spin(action_client)


if __name__ == '__main__':
    main()
```

Everything is ready for us. Your screen should display feedback if we run our action client.

```
python3 fibonacci_action_client.py
```

![image](https://user-images.githubusercontent.com/92859942/196530529-f7db7fc6-4050-4ab1-909a-a81f8d353c00.png)

we created an action. 

# 3. Composing multiple nodes in a single process

## To discover avilable components

In order to check the available components in the workspace, we run the following commands.

```
ros2 component types
```

![image](https://user-images.githubusercontent.com/92859942/196531590-83d5f202-93df-427a-8510-f329d24088c9.png)

## Run-time composition using ROS services with a publisher and subscriber

Run-time composition using ROS services with a publisher and subscriber

```
ros2 run rclcpp_components component_container
```
Using the ros2 command-line tools, we run the following command in the second terminal to show the name of the component as an output and confirm that the container is operating.

```
ros2 component list
```
![image](https://user-images.githubusercontent.com/92859942/196532868-bef5e720-419d-412b-96e7-5a385d98277c.png)

After this step, in the second terminal, we load the talker component:

```
ros2 component load /ComponentManager composition composition::Talker
```

After this, we run following code in the second terminal in order to load the listener component:

```
ros2 component load /ComponentManager composition composition::Listener
```
![image](https://user-images.githubusercontent.com/92859942/196533209-376650cb-b9cc-40b3-afeb-a41394c1b62f.png)


![image](https://user-images.githubusercontent.com/92859942/196533016-73b99ccb-e614-4452-923e-2bcdc1f0b252.png)

This command will return the node name and the distinctive ID of the loaded component:

Finally we can run the ros2 command line utility to inspect the state of the container:

```
ros2 component list
```
We can see the result as follows:

```
/ComponentManager
   1  /talker
   2  /listener
```
## Run-time composition using ROS services with a server and client
The steps are pretty similar to what we performed with the talker and listener.

Our first terminal is where we execute:

```
ros2 run rclcpp_components component_container
```
and after that, in the second terminal, we run following commands to see server and client source code:


```
ros2 component load /ComponentManager composition composition::Server
ros2 component load /ComponentManager composition composition::Client
```

![image](https://user-images.githubusercontent.com/92859942/196535552-bf513e3b-85ae-4f5d-b0dd-806cdade9c13.png)


![image](https://user-images.githubusercontent.com/92859942/196535376-146ee3c7-31fb-4220-8e91-8fa1448f901f.png)

## Compile-time composition using ROS services

This example demonstrates how the same shared libraries may be used to create a single executable that runs a number of different components.

All four of the aforementioned parts—talker, listener, server, and client—are present in the executable.

in one terminal 

```
ros2 run composition manual_composition
```
![image](https://user-images.githubusercontent.com/92859942/196536062-320156c7-c06f-4b5e-9d73-6a22e88c7dda.png)

## Run-time composition using dlopen

By constructing a generic container process and explicitly passing the libraries to load without using ROS interfaces, this demonstration provides an alternative to run-time composition. Each library will be opened by the procedure, and one instance of each "rclcpp::Node" class will be created in the library's source code.


```
ros2 run composition dlopen_composition `ros2 pkg prefix composition`/lib/libtalker_component.so `ros2 pkg prefix composition`/lib/liblistener_component.so
```

![image](https://user-images.githubusercontent.com/92859942/196536362-d01b5815-4470-4c80-8315-1a8a79b8a98f.png)

## Composition using launch actions

While the command line tools are helpful for troubleshooting and diagnosing component setups, starting a group of components at once is frequently more practical. We can make use of ros2 launch's functionality to automate this process.


```
ros2 launch composition composition_demo.launch.py
```

![image](https://user-images.githubusercontent.com/92859942/196536675-9ed0ad18-9eae-44ed-afd6-8390c876428e.png)


# 4. Creating a launch file

We use the rqt graph and turtlesim packages that we previously installed in order to produce a launch file.

## setup and writing the lunch file 

we should make new directory and create new file named turtlesim_mimic_launch.py and use the mention code in the file

```
mkdir launch
```

![image](https://user-images.githubusercontent.com/92859942/196538918-5213acd4-e1a3-42c7-aa12-9138c1a4668a.png)

code:
```
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        Node(
            package='turtlesim',
            namespace='turtlesim1',
            executable='turtlesim_node',
            name='sim'
        ),
        Node(
            package='turtlesim',
            namespace='turtlesim2',
            executable='turtlesim_node',
            name='sim'
        ),
        Node(
            package='turtlesim',
            executable='mimic',
            name='mimic',
            remappings=[
                ('/input/pose', '/turtlesim1/turtle1/pose'),
                ('/output/cmd_vel', '/turtlesim2/turtle1/cmd_vel'),
            ]
        )
    ])
```
![image](https://user-images.githubusercontent.com/92859942/196539540-b2972fdf-9eba-40fb-b565-f38c457bc884.png)

## ros2 launch

In order to run the launch file created, we enter into the earlier created directory and run the following commands:

```
cd launch
ros2 launch turtlesim_mimic_launch.py
```

![image](https://user-images.githubusercontent.com/92859942/196540724-cc3ee018-c4b9-4db1-923a-4cdae1009647.png)



To see the system in action, open a new terminal and run the ros2 topic pub command on the /turtlesim1/turtle1/cmd_vel topic to get the first turtle moving:

```
ros2 topic pub -r 1 /turtlesim1/turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: -1.8}}"
```

![image](https://user-images.githubusercontent.com/92859942/196543152-454bb774-8a15-4f21-a07c-772d8c91fc03.png)


## Introspect the system with rqt_graph
Open the new terminal without closing the system and we run rqt_graph.

```
rqt_graph
```
![image](https://user-images.githubusercontent.com/92859942/196543919-a18b22f0-45ac-46ce-8562-56c5bf725dac.png)

# 5. Integrating launch files into ROS2 packages

## Creating a package

Firstly, we create a workspace for the package:

```
mkdir -p launch_ws/src
cd launch_ws/src
```
and create a python package:

```
ros2 pkg create py_launch_example --build-type ament_python
```
![image](https://user-images.githubusercontent.com/92859942/196546845-3949bfdc-369c-4fe0-8592-2e0b0276c8c9.png)

##  Creating the structure to hold launch files


After creating the packages, it should be looking as follows for python package:

![image](https://user-images.githubusercontent.com/92859942/196548000-b2ecafcd-c546-4302-95a7-ba26d89a1e3e.png)


And utilizing the data files setup argument, we must tell Python's setup tools about our launch files in order to colcon to launch files.

We enter these codes in the setup.py file:

```
import os
from glob import glob
from setuptools import setup

package_name = 'py_launch_example'

setup(
    # Other parameters ...
    data_files=[
        # ... Other data files
        # Include all launch files.
        (os.path.join('share', package_name), glob('launch/*launch.[pxy][yma]*'))
    ]
)
```
## Writing the launch file

Inside your launch directory, create a new launch file called my_script_launch.py. _launch.py is recommended, but not required, as the file suffix for Python launch files.

Your launch file should define the generate_launch_description() function which returns a launch.LaunchDescription() to be used by the ros2 launch verb.

```
import launch
import launch_ros.actions

def generate_launch_description():
    return launch.LaunchDescription([
        launch_ros.actions.Node(
            package='demo_nodes_cpp',
            executable='talker',
            name='talker'),
  ])
```
## Building and running the launch file

We go to top-level of the workspace and build the file using:
```
colcon build
```
After the colcon build has been successful and you’ve sourced the workspace, you should be able to run the launch file as follows:

```
ros2 launch py_launch_example my_script_launch.py
```

# 6. Using Substitutions


We create a new package of build_type ament_python named launch_tutorial :

```
ros2 pkg create launch_tutorial --build-type ament_python
```
and inside of that package, we create a directory called launch.

```
mkdir launch_tutorial/launch
```
The setup.py file is then modified and adjustments are included to ensure a successful installation of the launch file.

```
import os
from glob import glob
from setuptools import setup

package_name = 'launch_tutorial'

setup(
    # Other parameters ...
    data_files=[
        # ... Other data files
        # Include all launch files.
        (os.path.join('share', package_name), glob('launch/*launch.[pxy][yma]*'))
    ]
)
```
## Parent Launch File

After the above steps, we created a launch file named : example_main.launch.py in the launch folder of the launch_tutorial directory with the following codes in it:

```
from launch_ros.substitutions import FindPackageShare

from launch import LaunchDescription
from launch.actions import IncludeLaunchDescription
from launch.launch_description_sources import PythonLaunchDescriptionSource
from launch.substitutions import PathJoinSubstitution, TextSubstitution


def generate_launch_description():
    colors = {
        'background_r': '200'
    }

    return LaunchDescription([
        IncludeLaunchDescription(
            PythonLaunchDescriptionSource([
                PathJoinSubstitution([
                    FindPackageShare('launch_tutorial'),
                    'example_substitutions.launch.py'
                ])
            ]),
            launch_arguments={
                'turtlesim_ns': 'turtlesim2',
                'use_provided_red': 'True',
                'new_background_r': TextSubstitution(text=str(colors['background_r']))
            }.items()
        )
    ])
```

## Substitutions example launch file

The same folder gains a new document called example substitutions.launch.py.

```
from launch_ros.actions import Node

from launch import LaunchDescription
from launch.actions import DeclareLaunchArgument, ExecuteProcess, TimerAction
from launch.conditions import IfCondition
from launch.substitutions import LaunchConfiguration, PythonExpression


def generate_launch_description():
    turtlesim_ns = LaunchConfiguration('turtlesim_ns')
    use_provided_red = LaunchConfiguration('use_provided_red')
    new_background_r = LaunchConfiguration('new_background_r')

    turtlesim_ns_launch_arg = DeclareLaunchArgument(
        'turtlesim_ns',
        default_value='turtlesim1'
    )
    use_provided_red_launch_arg = DeclareLaunchArgument(
        'use_provided_red',
        default_value='False'
    )
    new_background_r_launch_arg = DeclareLaunchArgument(
        'new_background_r',
        default_value='200'
    )

    turtlesim_node = Node(
        package='turtlesim',
        namespace=turtlesim_ns,
        executable='turtlesim_node',
        name='sim'
    )
    spawn_turtle = ExecuteProcess(
        cmd=[[
            'ros2 service call ',
            turtlesim_ns,
            '/spawn ',
            'turtlesim/srv/Spawn ',
            '"{x: 2, y: 2, theta: 0.2}"'
        ]],
        shell=True
    )
    change_background_r = ExecuteProcess(
        cmd=[[
            'ros2 param set ',
            turtlesim_ns,
            '/sim background_r ',
            '120'
        ]],
        shell=True
    )
    change_background_r_conditioned = ExecuteProcess(
        condition=IfCondition(
            PythonExpression([
                new_background_r,
                ' == 200',
                ' and ',
                use_provided_red
            ])
        ),
        cmd=[[
            'ros2 param set ',
            turtlesim_ns,
            '/sim background_r ',
            new_background_r
        ]],
        shell=True
    )

    return LaunchDescription([
        turtlesim_ns_launch_arg,
        use_provided_red_launch_arg,
        new_background_r_launch_arg,
        turtlesim_node,
        spawn_turtle,
        change_background_r,
        TimerAction(
            period=2.0,
            actions=[change_background_r_conditioned],
        )
    ])
```
## Building the package

We run the build command in the root of the workspace.

```
colcon build
```
## Launching Example

Now we can use the ros2 launch command to execute the example main.launch.py file.

```
ros2 launch launch_tutorial example_main.launch.py
```

![image](https://user-images.githubusercontent.com/92859942/196817954-cefdc716-4489-4e12-b119-6576ff9e1d2b.png)

A blue backdrop is used while starting a turtlesim node. Following that, a second turtle hatches, and the backgrounds are purple and pink, respectively.

# 7. Using Event Handlers
 
 Event handler example launch file
 
 We created a new file named: example_event_handlers.launch.py in the same directory.. i.e. inside launch folder of launch_tutorial package.

```
from launch_ros.actions import Node

from launch import LaunchDescription
from launch.actions import (DeclareLaunchArgument, EmitEvent, ExecuteProcess,
                            LogInfo, RegisterEventHandler, TimerAction)
from launch.conditions import IfCondition
from launch.event_handlers import (OnExecutionComplete, OnProcessExit,
                                OnProcessIO, OnProcessStart, OnShutdown)
from launch.events import Shutdown
from launch.substitutions import (EnvironmentVariable, FindExecutable,
                                LaunchConfiguration, LocalSubstitution,
                                PythonExpression)


def generate_launch_description():
    turtlesim_ns = LaunchConfiguration('turtlesim_ns')
    use_provided_red = LaunchConfiguration('use_provided_red')
    new_background_r = LaunchConfiguration('new_background_r')

    turtlesim_ns_launch_arg = DeclareLaunchArgument(
        'turtlesim_ns',
        default_value='turtlesim1'
    )
    use_provided_red_launch_arg = DeclareLaunchArgument(
        'use_provided_red',
        default_value='False'
    )
    new_background_r_launch_arg = DeclareLaunchArgument(
        'new_background_r',
        default_value='200'
    )

    turtlesim_node = Node(
        package='turtlesim',
        namespace=turtlesim_ns,
        executable='turtlesim_node',
        name='sim'
    )
    spawn_turtle = ExecuteProcess(
        cmd=[[
            FindExecutable(name='ros2'),
            ' service call ',
            turtlesim_ns,
            '/spawn ',
            'turtlesim/srv/Spawn ',
            '"{x: 2, y: 2, theta: 0.2}"'
        ]],
        shell=True
    )
    change_background_r = ExecuteProcess(
        cmd=[[
            FindExecutable(name='ros2'),
            ' param set ',
            turtlesim_ns,
            '/sim background_r ',
            '120'
        ]],
        shell=True
    )
    change_background_r_conditioned = ExecuteProcess(
        condition=IfCondition(
            PythonExpression([
                new_background_r,
                ' == 200',
                ' and ',
                use_provided_red
            ])
        ),
        cmd=[[
            FindExecutable(name='ros2'),
            ' param set ',
            turtlesim_ns,
            '/sim background_r ',
            new_background_r
        ]],
        shell=True
    )

    return LaunchDescription([
        turtlesim_ns_launch_arg,
        use_provided_red_launch_arg,
        new_background_r_launch_arg,
        turtlesim_node,
        RegisterEventHandler(
            OnProcessStart(
                target_action=turtlesim_node,
                on_start=[
                    LogInfo(msg='Turtlesim started, spawning turtle'),
                    spawn_turtle
                ]
            )
        ),
        RegisterEventHandler(
            OnProcessIO(
                target_action=spawn_turtle,
                on_stdout=lambda event: LogInfo(
                    msg='Spawn request says "{}"'.format(
                        event.text.decode().strip())
                )
            )
        ),
        RegisterEventHandler(
            OnExecutionComplete(
                target_action=spawn_turtle,
                on_completion=[
                    LogInfo(msg='Spawn finished'),
                    change_background_r,
                    TimerAction(
                        period=2.0,
                        actions=[change_background_r_conditioned],
                    )
                ]
            )
        ),
        RegisterEventHandler(
            OnProcessExit(
                target_action=turtlesim_node,
                on_exit=[
                    LogInfo(msg=(EnvironmentVariable(name='USER'),
                            ' closed the turtlesim window')),
                    EmitEvent(event=Shutdown(
                        reason='Window closed'))
                ]
            )
        ),
        RegisterEventHandler(
            OnShutdown(
                on_shutdown=[LogInfo(
                    msg=['Launch was asked to shutdown: ',
                        LocalSubstitution('event.reason')]
                )]
            )
        ),
    ])
```

![image](https://user-images.githubusercontent.com/92859942/196819121-44a0f48f-af1e-4c63-b295-b701ad84adf5.png)

## Building and Running the Command
 
 After adding the file, we go back to the root of the workspace and run the build command there.

```
colcon build
```
 
 
It is crucial to source the package and execute the following commands for the output after building:

ros2 launch example event handlers.launch.py launch tutorial Use provided red:=True, turtlesim ns:='turtlesim3', and new background r:=200

![image](https://user-images.githubusercontent.com/92859942/196819215-88d3c78d-2b44-4e8c-b7b5-4685f6a5a414.png)


It spawns the second turtle and starts a turtlesim node with a blue backdrop. The background color then changes to pink and then purple. When the turtlesim window closes, the launch file also shuts down.

          THANK YOU 








