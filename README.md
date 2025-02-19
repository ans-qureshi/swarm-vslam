# Swarm-vSLAM: A Multi-agent Approach to Improve Visual SLAM Performance using Miniature Robots
Miniature UGVs provide a low-cost and scalable solution in the field of robotics. With a multi-agent formation, visual SLAM systems can provide a redundant and robust solution to failures caused by track loss or mechanical faults. In this paper, we have proposed a multi-agent approach to improve the visual SLAM performance using miniature robots. By allowing multiple miniature robots to perform the same SLAM task, we decrease the probability of SLAM failure caused in the mapping of an unknown environment. We have performed multi-agent SLAM with the help of indigenously developed miniature UGVs as small as the palm of our hand. Each of the UGVs are operating and sending data with the help of Robot Operating System (ROS) installed over a Linux based edge device. We have also demonstrated the integration of OAK-D camera, Nano Pi computer and an ATMega328 based miniature computer by using socket programming and ROS. The experimentation results show that the SLAM failure is minimized due to the redundancy demonstrated by multiple SLAM agents. A set of vision based obstacle avoidance techniques are also applied for smooth navigation of the multiple robots.

To cite our paper, please use the Bibtex:
## BibTex
```
@inproceedings{qureshi2022multi,
  title={A Multi-agent Approach to Improve Visual SLAM Performance using Miniature Robots},
  author={Qureshi, Ans Hussain and Khaliq, Saran and Shahzad, Muhammad Muzamal and Saeed, Muhammad Saad and Johar, Ahmed Husnain and Yousaf, Muhammad Haroon},
  booktitle={TENCON 2022-2022 IEEE Region 10 Conference (TENCON)},
  pages={1--6},
  year={2022},
  organization={IEEE}
}
```

## Video
https://github.com/ans-qureshi/swarm-vslam/assets/38855178/14181aed-e35c-4b65-b999-32b3b3d26ab7 


## Working
![Flowchart](https://github.com/srl-ncra/swarm-vslam/blob/main/Flowchart.jpg?raw=true)

## 1. Client Setup (over SIMBot)
We configured the client on a NanoPi NEO Plus 2 running Ubuntu Core 20.04 LTS. To set up a NanoPi, you can refer to this tutorial: [NanoPi NEO Plus2](https://wiki.friendlyarm.com/wiki/index.php/NanoPi_NEO_Plus2). 
After Ubuntu installation, assign an IP to the NanoPi and access it using ssh, then follow these commands:

1. Make sure that you are in root directory.

2. Run: `mkdir opencv_com`
3. Run: `cd opencv_com`

4. Run: `sudo nano requirements.txt`
	Copy the text from `requirements.txt` to this file and save.

5. Run: `pip install -r requirements.txt` (All libraries will be automatically installed)

6. Run: `sudo nano obs_pi.py`
	Copy content of obs_pi.py to this file.
	Save and close. (C+S then C+X)

### If you face following OpenCV error  
	
`Error: ImportError: libGL.so.1: cannot open shared object file: No such file or directory`

1. Run: `sudo apt-get update && apt-get install -y python3-opencv`

### Running Obstacle Detection 
This code will start moving the SIMBot while avoiding obstacles and publishing camera data on a ROS topic which the server will subscribe to
1. Make sure you are in opencv_com directory.
2. Run: `python3 obs_pi.py`

  
## 2. Server Setup (GUI for visualization) 
To setup the server, we need to install [CCM-SLAM](https://github.com/VIS4ROB-lab/ccm_slam) on the PC. After installation:
Make multiple copies of the Client.launch file according to the number of robots being used. 
2. Run `roslaunch ccmslam Client.launch`
3. Run `rviz` for visualization of the trajectories of multiple agents.
The final setup should look like this:
![SLAM](https://github.com/srl-ncra/swarm-vslam/blob/main/SLAM_setup.PNG?raw=true)
