# iot_agent_ros2

<h2 dir="auto"><a id="user-content-usage" class="anchor" aria-hidden="true" href="#usage"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a><a id="user-content-getting-started" href="#usage"></a>Installation</h2>

<h3>
 Run the following commands in terminal.
</h3>


<h4>
 Source ROS2 setup files.
</h4>

<p>
source /opt/ros/humble/setup.bash
</p>

<h4>
 Execute nodejs code.
</h4>

<p>
node index.js
</p>

<h2 dir="auto"><a id="user-content-usage" class="anchor" aria-hidden="true" href="#usage"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a><a id="user-content-getting-started" href="#usage"></a>Usage</h2>

<h4>
 This agent uses the <a href="https://github.com/RobotWebTools/rclnodejs">rclnodejs library</a> combined with the <a href="https://github.com/telefonicaid/iotagent-node-lib"> Fiware iotagent-node-lib</a>. The agent creates the following
</h4>
 <ol> 
  <li>Subscriptions and Publishers for ROS Machines</li>
  <li>ROS2 Client</li>
  <li>GPIO Action Client for Legacy CNC Machines</li>
 </ol>
 
 <h4>
 Subscriptions and Publishers
</h4>

<p>
The function "initROSDevice" was created to initialize or create new subscribers or publishers. When the agent starts, it locates the already registered/created devices and initializes the existing ROS2 publishers and subscribers for each device. Additionally the agent handles new registrations/creations of publishers and subscribers when a new device is created.
</p>

<h4>
 ROS2 Client
</h4>

<p>
You can send your commands and be redirected to your ROS2 device with the rclnodejs Client/Server. The server runs on the actual hardware device and the agent handles in the function called "updateContextHandler" the creation of the ROS2 Client and sends the message to the device.
</p>

<h4>
 GPIO Action Client for Legacy CNC Machines
</h4>

<p>
You can send your commands and be redirected to your ROS2 device with the rclnodejs Action Client/Server. The action server runs on the actual hardware device and the agent handles in the function called "updateContextHandler" the creation of the ROS2 Action Client (class called "GPIOActionClient") and sends the message to the device.
</p>


<h4>
 Data Models
</h4>

<p>
ROS2 System
</p>

<pre>
{
    "devices": [
        {
            "device_id": "turtle001",
            "entity_name": "urn:ngsiv2:ROS2System:Turtle001",
            "entity_type": "ROS2System",
            "transport": "HTTP",
            "lazy": [
                {"object_id": "pose_lazy", "name": "turtlePoseLazy", "type":"object"},
                {"object_id": "cmd_vel", "name":"setVelocity", "type": "object"}
            ],
            "internal_attributes": [
                {"turtlePoseLazy": {"ros2Interface": {"type":"string","value":"subscriber"},
                                    "topicType":{ "type":"string","value":"turtlesim/msg/Pose"},
                                    "topicName": {"type":"string","value":"/turtle1/pose"},
                                    "throttlingInMilliseconds": {"type":"number", "value": 200 }}
                },
                {"setVelocity": {"ros2Interface": {"type":"string","value":"publisher"},
                                    "topicType":{ "type":"string","value":"geometry_msgs/msg/Twist"},
                                    "topicName": {"type":"string","value":"/turtle1/cmd_vel"},
                                    "throttlingInMilliseconds": {"type":"number", "value": 200 }}
                }
            ],
            "attributes": [
                {
                    "object_id": "pose", "name": "turtlePoseActive", "type": "object",
                    "metadata": {"ros2Interface": {"type":"string", "value":"subscriber"},
                                 "topicType": {"type":"string", "value":"turtlesim/msg/Pose"},
                                 "topicName": {"type":"string", "value":"/turtle1/pose"},
                                 "throttlingInMilliseconds": {"type":"number", "value":200}
                                 }
                }
            ],
            "commands":[
                {
                    "object_id":"start",
                    "name":"start",
                    "type":"command"
                },
                {
                    "object_id":"stop",
                    "name":"stop",
                    "type":"command"
                }
            ]
        }
    ]
}
</pre>


<p>
CNC Legacy Devices
</p>

<pre>
{
    "devices": [
        {
            "device_id":"axis001",
            "entity_name":"urn:ngsi-ld:Axis:001",
            "entity_type":"IOT",
            "endpoint":"https://dihweb.conveyor.cloud/api/api/ThreeAxisEndpoint",
            "transport":"HTTP",
            "attributes":[
                {
                    "object_id":"Status",
                    "name":"Status",
                    "type":"Text"
                }
            ],
            "commands":[
                {
                    "object_id":"start",
                    "name":"start",
                    "type":"command"
                },
                {
                    "object_id":"stop",
                    "name":"stop",
                    "type":"command"
                },
                {
                    "object_id":"auto",
                    "name":"auto",
                    "type":"command"
                }
            ]
        }
    ]
}
</pre>
