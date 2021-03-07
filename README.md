# learning_moveit

## learning moveit config

![IMG_1348](https://github.com/Van23Li/learning_moveit/tree/main/Images/IMG_1348.JPG)

~~~bash
rostopic type /move_group/fake_controller_joint_states
->sensor_msgs/JointState

rosmsg show sensor_msgs/JointState
->
std_msgs/Header header
	uint32 seq
	time stamp
	string frame_id
string[] name
float64[] position
float64[] velocity
float64[] effort

rostopic type /joint_states
->sensor_msgs/JointState
~~~

~~~
demo.launch
	-> planning_context.launch: load the URDF, SRDF, and other .yaml configuration filters on the param server
		-> probot_description/urdf/probot_anno.xacro: 加载URDF
		-> probot_anno_moveit_config/config/probot_anno.srdf: 加载URDF语义描述，即配置时设置的chains, pose,碰撞检测等
		-> probot_anno_moveit_config/config/joint_limits.yaml: 各关节的速度、加速度限制
		-> probot_anno_moveit_config/config/kinematics.yaml:加载运动学的默认配置，可以在namespace中覆盖
	-> 启动node "joint_state_publisher"
	-> move_group.launch: 运行moveit
		-> planning_context.launch
		-> planning_pipline.launch.xml: Planning functionality，此处使用OMPL
		-> trajectory_execution.launch.xml: Trajectory execution functionality
		-> sensor_manager.launch.xml: Sensors functionality
		-> 启动node "move_group"
	-> moveit_rviz.launch: Rviz
~~~



