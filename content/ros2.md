Robotic Operating Systems - not an OS but a middleware communication framework

`colcon` to build packages
- build: intermediate files stored
- install: package installed to
- log: log info

## concepts
- nodes = vertices
- topics = edges
	- publisher/subscriber
	- msg types
- parameters - configs
	- `ros2 param list/get/set`
- services / clients - sync
	- `ros2 service list/call`
	- node communication model
	- call-and-response (client calls and service server responds)
	- request type, response type
- actions - async
	- `ros2 action list/send_goal`
	- for long running tasks
	- similar to services but *preemptable*
	- action client sends a goal to action server
	- server sends feedback stream to action client
	- server send result to client

to show documentation: `ros2 interface show [action/service]`