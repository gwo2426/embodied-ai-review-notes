# Embodied Perception: Challenges and Design Principles

This repository contains my research notes and summaries for the review paper **"Embodied Perception: Challenges and Design Principles"**.

As part of a collaborative research project, I was responsible for **Section 2**, which systematically analyzes the embodiment-induced challenges of humanoid perception and distills the design principles that increasingly shape modern humanoid perception systems.

## 📄 Source Document

The original review paper is included in this repository:
* [Review Paper (PDF)](./review.pdf)

---

## 🎯 Research Focus: Section 2 — Embodied Perception: Challenges and Design Principles

The anthropomorphic form of humanoid robots creates a fundamental tension for perception. Human-like morphology allows robots to operate in human-designed environments, but it also makes perception tightly coupled with the robot's own body, motion, and hardware constraints. Perception in humanoids should therefore be treated as an **embodied systems problem** rather than an isolated sensing module.

### A. Embodiment-Induced Challenges

**1. Self-Occlusion and Action-Conditioned Observability**

Unlike static manipulators or external camera setups, humanoid robots frequently occlude their own sensors with their arms, legs, or torso during manipulation and locomotion. As a result, observability is not fixed but depends on the robot's current pose and action. The same scene may be easy or difficult to perceive depending on how the body moves relative to the camera and the task.

**2. Dynamic Motion and State-Estimation Drift**

Bipedal locomotion introduces repeated impacts, head motion, and rapid viewpoint changes, all of which degrade visual stability. Motion blur, feature loss, and inertial integration errors can accumulate into odometry drift and geometric misalignment, especially on rough terrain or during agile transitions. Perception noise directly affects foothold selection, balance recovery, and terrain-aware control.

**3. Onboard Compute, Latency, and Power Constraints**

Humanoid robots carry their compute hardware onboard, which imposes strict limits on power consumption, thermal budget, memory footprint, and inference latency. Perception systems must not only be accurate but also stable under real-time constraints and compatible with downstream control frequencies.

**4. Sensor Heterogeneity and Transfer Gaps**

There is still no standard sensor configuration for humanoid platforms. Camera placement, field of view, lens type, and auxiliary modalities such as tactile sensing, radar, or LiDAR vary widely across systems. This heterogeneity produces platform-specific data distributions and weakens the direct transferability of perception models, especially when those models are pretrained on data from other robot forms or third-person viewpoints.

**5. Partial Observability over Time**

Humanoid perception is rarely based on a single stable snapshot. Useful information is often distributed across time because of occlusion, body motion, and limited field of view. Reliable perception therefore requires temporal integration, short-term memory, and consistency across observations, rather than frame-wise recognition alone.

---

### B. Methodological Design Principles

To address these challenges, humanoid perception systems are shifting from passive pipelines toward embodied, feedback-driven designs. Four principles recur across recent systems:

**1. From Passive Sensing to Active Perception**

Perception should not be treated as a passive process that merely consumes whatever observations are available. In humanoid systems, sensing quality can often be improved by changing head pose, torso orientation, viewpoint, or contact state. This motivates active perception, where visibility and information gain become part of the control objective rather than a fixed precondition for perception. Body motion can both create and resolve occlusion.

**2. Egocentric Perception with Proprioceptive Grounding**

Because global maps and long-horizon state estimates are easily degraded by drift, humanoid perception often benefits from egocentric representations tied to the robot's body frame. Fusing vision with proprioception and inertial sensing provides a more stable estimate of body state, contact, and traversability under motion. Recent perceptive locomotion systems increasingly rely on this combination to stabilize terrain understanding and action selection under noisy exteroceptive input.

**3. Controllable Multimodal Redundancy**

Vision remains the dominant sensing modality, but vision alone is often insufficient in low light, heavy occlusion, high-speed motion, or contact-rich manipulation. A robust humanoid perception stack should therefore include complementary modalities — tactile sensing for near-field contact, IMU for high-rate ego-motion, and radar or depth sensing for adverse conditions. The goal is not redundancy for its own sake, but **controllable redundancy** that allows graceful degradation when one modality becomes unreliable.

**4. Morphology-Aware Representation and Decision Coupling**

Representations for humanoid perception should be aware of the robot's embodiment — encoding not only scene content, but also body pose, kinematic constraints, visibility structure, and action relevance. More broadly, perception should be coupled with decision making: the value of a representation depends on whether it supports locomotion, manipulation, navigation, or interaction under the robot's specific physical constraints.

---

### C. Internal Models as the Bridge from Perception to Action

A key implication of the above principles is that humanoid perception requires **internal models** that persist beyond the current frame. These may take the form of short-term memory buffers, body-centric spatial maps, semantic world models, or predictive latent states. Their role is to maintain object permanence under occlusion, smooth perceptual instability caused by locomotion, and support action selection when the current observation is incomplete.

For humanoid robots, internal models should ideally satisfy three requirements: they should be *body-aware*, *temporally coherent*, and *decision-relevant*. Under this perspective, the perception system is not a front-end that passively feeds downstream modules, but a **dynamic component of the full embodied control loop**.
