# 基于 RL 决策和 Diffusion Policy 的 ARM - Challenge 项目

[![SVG Banners](https://svg-banners.vercel.app/api?type=origin&text1=ARM-diffusion%20🤖&text2=🐨%20Diffusion%20Policy%20Based%20Robot%20Manipulator%20Grasping%20System&width=800&height=200)](https://github.com/Akshay090/svg-banners)

**其他语言**

-🦄 English ([README.md](README.md))

本项目旨在通过**RL抓取决策**和**Diffusion Policy**的轨迹规划方式完成 **ARM -Challenge** 挑战赛。“自主机器人操作挑战赛”（ARM Challenge）是由 RoboCup 关联举办的一项赛事，旨在吸引青年研究者和学生，参与解决关于机器人自主操作的挑战性课题，形式为教育性科学竞赛。该赛事由 RoboCup 与 MathWorks、Universal Robots 提供技术支持。


<div align=center>
<image src="https://github.com/catowningengineer-cell/ARM-diffusion/blob/main/images/ARM-challenge.png">
</div>


参赛队伍需要在动态环境中使用机械臂完成“回收任务”——机器人抓取并操作瓶子、易拉罐和洗涤剂袋等物品，将其按类别分类至两个不同的收集箱。机器人抓取与操作能力是多数机器人应用的关键技能。赛事提供了一个公平的舞台，让 RoboCup 参与者及学生团队在模拟环境中研究和展示操作感知与控制算法，并将这些算法迁移至商用机器人平台。2025年新增了**动态环境** ——即物体位置和障碍物位置随机的变化，这使得使得机械臂具备自主推理能力尤为重要。

ARM - Challenge 的官网：[ARM-Challenge](https://arm.robocup.org/)

## 1. 理论基础
在熟悉本项目之前，我们强烈建议您跟进强化学习和扩散模型等领域的相关论文和理论课程。

相关论文：

 - Chi, C. et al. (2025) Diffusion policy: Visuomotor policy learning via action diffusion. *The International journal of robotics research.* [Online] 44 (10–11), 1684–1704. [[paper](https://arxiv.org/pdf/2303.04137)][[code](https://github.com/real-stanford/diffusion_policy.git)]

 - Ze, Y. et al. (2024) *3D Diffusion Policy: Generalizable Visuomotor Policy Learning via Simple 3D Representations.* [Online] [[paper](https://arxiv.org/pdf/2403.03954)][[code](https://github.com/YanjieZe/3D-Diffusion-Policy.git)]

 - Ren, A. Z. et al. (2024) *Diffusion Policy Policy Optimization.* [Online] [[paper](https://arxiv.org/pdf/2409.00588)][[code](https://github.com/irom-princeton/dppo)]


理论课程：

- 强化学习理论：[Stanford CS234](https://www.bilibili.com/video/BV1dWB2Y4EcG/?spm_id_from=333.1387.favlist.content.click&vd_source=367cdd85f2bb24f751f4c11cf9a0f8eb) by Emma Brunskill 教授
  
- 流匹配与扩散模型：[MIT 6.S184](https://www.bilibili.com/video/BV1gc8Ez8EFL/?spm_id_from=333.337.search-card.all.click&vd_source=367cdd85f2bb24f751f4c11cf9a0f8eb) by Peter Holderrieth 和 Ezra Erives

## 2. 环境搭建和数据采集

本项目的测试环境是 Ubuntu 20.04, ROS 版本为 ROS - noetic，仿真平台是 gazebo11。
