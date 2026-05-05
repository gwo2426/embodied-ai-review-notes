# Embodied Perception: Challenges and Design Principles

This repository contains my research notes and summaries for the review paper **"Embodied Perception: Challenges and Design Principles"**. 

As part of a collaborative research project, I was responsible for **Section 2**, which systematically analyzes the core challenges of embodied perception and proposes fundamental design principles for next-generation robotic systems.

## 📄 Source Document

The original review paper is included in this repository:
* [Review Paper (PDF)](./review.pdf)

## 🎯 Research Focus: Section 2

My research focused on the intersection of physical constraints and perception algorithms in humanoid and legged robots. The traditional "perception-planning-control" paradigm often fails in dynamic, real-world physical interactions. My work systematically summarized the following aspects:

### Five Core Challenges in Embodied Perception

1. **Physical Constraints and Self-Occlusion**: The robot's own morphology and actions frequently occlude its vision during physical interaction.
2. **High-Frequency Impact and Dynamic Environments**: Locomotion (e.g., walking, parkour) introduces severe physical impacts, leading to sensor noise and drift.
3. **Real-time Requirements under Limited Compute**: Embodied perception demands extreme real-time processing with limited onboard computational resources to ensure control stability.
4. **Asynchronous and Heterogeneous Multimodal Data**: Significant disparities exist in sampling rates and data structures across vision, proprioception (joint angles, torques), and tactile sensors.
5. **The Sim-to-Real Gap**: The discrepancy between idealized sensor models in simulation and physical noise/friction in the real world hinders direct policy transfer.

### Four Key Design Principles

1. **Proprioception-grounded Egocentric Perception**: When visual information is unreliable (due to occlusion or lighting) or delayed, proprioception serves as the ground truth and the last line of defense for maintaining physical balance.
2. **Controllable Multimodal Redundancy**: Building redundant perception channels and dynamically adjusting modality weights (e.g., relying on vision on flat ground, but shifting weight to proprioception/tactile sensing on snow or grass).
3. **Morphology-aware Representation**: Perception systems must be tightly coupled with the robot's physical morphology (DoF, dynamics). Perception is action-conditioned.
4. **Internal Model as a Bridge**: Establishing internal dynamic models of the physical world to compensate for sensor delays and missing data through future state prediction.

## 🛠️ Key Takeaways

The fundamental difference between embodied perception and traditional computer vision lies in its **activeness** and **physical interactivity**. Robots do not passively receive images; they actively acquire information through actions (Active Perception) and verify perception through physical contact. This deep coupling of "perception as action, action as perception" is the key to achieving Artificial General Intelligence (AGI) in the physical world.
