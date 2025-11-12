# ARM - Challenge Project with RL and Diffusion Policy

[![SVG Banners](https://svg-banners.vercel.app/api?type=origin&text1=ARM-diffusion%20🤖&text2=🐨%20Diffusion%20Policy%20Based%20Robot%20Manipulator%20Grasping%20System&width=800&height=200)](https://github.com/Akshay090/svg-banners)

**Alternative Languages**

-🐉 简体中文 ([readme.zh-CN.md](readme.zh-CN.md))


This project aims to accomplish the ARM Challenge by integrating reinforcement learning (RL)–based grasping decision-making with trajectory planning through the Diffusion Policy framework. The “Autonomous Robot Manipulation Challenge” (ARM Challenge) is a competition affiliated with RoboCup, designed to attract young researchers and students to tackle challenging topics in autonomous robotic manipulation. It takes the form of an educational and scientific competition, technically supported by RoboCup, MathWorks, and Universal Robots.

<div align=center>
<image src="https://github.com/catowningengineer-cell/ARM-diffusion/blob/main/images/ARM-challenge.png">
</div>

Participating teams are required to complete a “Recycling Task” in a dynamic environment — using a robotic arm to grasp and manipulate various objects such as bottles, cans, and detergent pouches, and sort them into two separate collection bins according to their categories. Grasping and manipulation are fundamental skills for most robotic applications. The competition provides a fair platform for RoboCup participants and student teams to research and demonstrate perception and control algorithms for manipulation in a simulated environment, and to transfer these algorithms to commercial robotic platforms. In 2025, a new dynamic environment is introduced — where both the positions of objects and obstacles change randomly. This makes it especially important for robotic arms to possess autonomous reasoning capabilities.


ARM - Challenge website：[ARM-Challenge](https://arm.robocup.org/)

## 1. Theoretical Basis
Before getting familiar with this project, we strongly recommend that you review relevant papers and theoretical courses in fields such as reinforcement learning and diffusion models.

### 📊 Related Work：

 - Chi, C. et al. (2025) Diffusion policy: Visuomotor policy learning via action diffusion. *The International journal of robotics research.* [Online] 44 (10–11), 1684–1704. [[paper](https://arxiv.org/pdf/2303.04137)][[code](https://github.com/real-stanford/diffusion_policy.git)]
 - Ze, Y. et al. (2024) *3D Diffusion Policy: Generalizable Visuomotor Policy Learning via Simple 3D Representations.* [Online] [[paper](https://arxiv.org/pdf/2403.03954)][[code](https://github.com/YanjieZe/3D-Diffusion-Policy.git)]
 - Ren, A. Z. et al. (2024) *Diffusion Policy Policy Optimization.* [Online] [[paper](https://arxiv.org/pdf/2409.00588)][[code](https://github.com/irom-princeton/dppo)]

### 📖 Educational Resource：

- **Reinforcement Learning**：[Stanford CS234](https://www.youtube.com/watch?v=4ngb0IZTg8I&list=PLoROMvodv4rN4wG6Nk6sNpTEbuOSosZdX) by Prof. Emma Brunskill 
- **Flowing Match and Diffusion Model**：[MIT 6.S184](https://www.youtube.com/watch?v=3dz6qfjW20o&list=PL_1TbuIu65A9rac2dMLkvXvPS5YHtADRF) by Peter Holderrieth and Ezra Erives

### 📝 Assumption：
- The expert optimality assumption holds — the expert demonstration actions are considered reliable.
- The dataset is multi-modal, containing both **RGB** images and action data; the model can implicitly learn obstacle avoidance from RGB inputs.
- The Diffusion Policy possesses a certain level of generalization ability, which can be leveraged and enhanced through fine-tuning in this project.

It is interesting to notice that both two version of **Diffusion Policy** utilize *ResNet - 18* as **backbone**, and this actually simplified training process。Compared with the large-scale pre-training processes in both *SigLIP* and *DINOv2* in **OpenVLA**, **Diffusion Policy** are more friendly for end-to-end training, which is also supported by the article.

## 2. Environment Building and Data Collection

Before this project, we had already developed a complete ARM system based on Gazebo and MoveIt!.
This system uses a visual recognition module built upon YOLOv8 and an RGB-D depth camera to detect, segment, and locate objects on the table. Motion planning and execution are performed through MoveIt!, resulting in a highly mature system with excellent precision in sorting and obstacle avoidance — suitable to serve as an expert demonstrator.

In addition, we have precise knowledge of the object poses generated in the simulation world, allowing us to explicitly integrate these poses into the planning process during data collection.
To enhance generalization in dynamic environments, we defined five distinct object pose distributions, and for each distribution, conducted 50–100 expert demonstration trajectories to collect training data.
