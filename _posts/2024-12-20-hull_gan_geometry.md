---
title:  "Revolutionizing Hull Design with GANs: Exploring Engineering's Future"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/ship_gan_cover.png" alt="gan cover" style="width: 800px; height: auto;">
</div>

## Introduction

Modern engineering thrives on innovation, and ship design is no exception. Traditionally, creating ship hulls has been a meticulous and resource-intensive process. However, advancements in **Generative Adversarial Networks (GANs)** are revolutionizing this domain, offering unprecedented efficiency and creativity in hull geometry generation.

This blog explores a groundbreaking project conducted at **MARIN** in collaboration with the **University of Strathclyde**, where we developed a GAN-based framework to generate 3D ship hull geometries. By merging AI with engineering, we're taking a leap towards automated, innovative design solutions.

---

## Understanding the Challenge: Hull Design

Designing a ship hull requires balancing **hydrodynamics, and manufacturability**. Traditional methods often involve:
- Iterative adjustments by designers.
- Computationally expensive simulations.
- Limited exploration of diverse design possibilities.

Our goal? To streamline and amplify this process by using **Deep Convolutional GANs (DCGANs)**. Unlike typical image-based GAN applications, we adapted the framework to generate complex **3D geometries** represented by structured point clouds. This approach bridges the gap between classical methods and modern AI-driven solutions.

---

## How It Works: A Dive Into GANs

GANs consist of two neural networks:
1. **Generator**: Creates realistic outputs (in this case, hull geometries).
2. **Discriminator**: Differentiates between real and generated geometries.

Through iterative adversarial training, the generator learns to create increasingly convincing geometries, while the discriminator sharpens its evaluation skills. The result? A harmonious system producing high-quality hull designs.

### Key Features of Our DCGAN Framework
- **Structured Point Clouds**: Hull geometries encoded into 3D data for seamless processing.
- **Loss Functions**: Implemented advanced metrics for optimization:
  - **Binary Cross-Entropy Loss (BCE)** for adversarial training:

    $$L_D = -\mathbb{E}_{x \sim p_{\text{data}}}[\log(D(x))] - \mathbb{E}_{z \sim p_z}[\log(1 - D(G(z)))]$$

    $$L_G = -\mathbb{E}_{z \sim p_z}[\log(D(G(z)))]$$
    
  - **Space-Filling Loss** to ensure diversity:
    
    $$S = \sum_{i=1}^{m-1} \sum_{j=i+1}^m \frac{1}{\|\mathbf{x}_j - \mathbf{x}_i\|^2}$$
    
    where $$(\mathbf{x}_i, \mathbf{x}_j)$$ are generated designs, and $$( m )$$ is the total number of designs.
  - **Laplace Loss** to reduce noise and improve smoothness:

    $$L_{\text{lap}} = \sum_{i} |\Delta x_i|$$

    where $$( \Delta x_i )$$ is the Laplacian for point $$( i )$$.

- **Post-Processing**: Applied Gaussian smoothing and symmetry enforcement for refinement:
    \[
    x_{\text{smoothed}} = x \ast G(\mu, \sigma^2)
    \]
    where \( G(\mu, \sigma^2) \) is a Gaussian kernel.

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/proposed_gan_pipeline.png" alt="gan pipeline" style="width: 800px; height: auto;">
</div>

---

## From Concept to Results: The Journey

### Data Preparation
Our dataset included **12,000 geometries** from six vessel classes (e.g., sailing yachts, motor yachts). Each geometry was encoded using a **Rhino Grasshopper pipeline**, enabling automated and scalable processing.

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/various_vessel_classes.png" alt="Vessel Classes" style="width: 800px; height: auto;">
</div>

### GAN Architecture
- **Generator**: Mapped latent vectors (\( z \sim \mathcal{N}(0, I) \)) to 3D hull geometries using transposed convolutional layers:
    \[
    h_{l+1} = \text{ReLU}(\text{BatchNorm}(W_l^T h_l + b_l))
    \]
- **Discriminator**: Processed geometries to classify them as real or fake using convolutional layers:
    \[
    h_{l+1} = \text{LeakyReLU}(\text{BatchNorm}(W_l h_l + b_l))
    \]

### Results
The DCGAN successfully generated realistic and diverse hull designs. However, challenges like irregularities in the **forebody** and dataset limitations highlighted areas for improvement.

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/hull_gan_geometries.gif" alt="Hull GAN Geometries" style="width: 800px; height: auto;">
</div>

---

## Beyond Hulls: The Broader Impact of AI in Engineering

This project isn't just about ships—it showcases how AI can transform engineering:
- **Rapid Prototyping**: Generate designs in seconds.
- **Optimized Performance**: Integrate hydrodynamic metrics for enhanced designs.
- **Creative Exploration**: Discover innovative hull forms beyond human imagination.

---

## Future Directions

While the current DCGAN model demonstrated promise, there’s room for advancement:
1. **Improved Architectures**: Explore StyleGAN or Diffusion Models for higher fidelity.
2. **Enhanced Datasets**: Incorporate more diverse geometries, including challenging features like bulbous bows.
3. **Physics Integration**: Embed hydrodynamic properties directly into the model.

---

## Conclusion

The fusion of GANs and engineering is more than a technical milestone—it's a paradigm shift. At MARIN, in collaboration with the University of Strathclyde, we've laid the groundwork for AI-driven ship design. By leveraging **Generative Adversarial Networks**, we've demonstrated the potential for rapid, automated, and innovative hull geometry generation.

While the current model showed significant promise, there’s still room to expand—improving datasets, refining architectures, and integrating physical constraints will further enhance its utility in real-world applications.

---

### Explore the Code

For those eager to dive deeper into the technical side, we've made the training script for a **GAN model** open-source. This script includes the core DCGAN architecture, loss functions, and training workflows used in this project. While the dataset remains proprietary (For now...), the script provides a robust starting point for exploring similar applications in your domain.

[Access the training script on GitHub](to be added) 

As technology evolves, so does our capacity to innovate, optimize, and redefine what's possible in engineering. Join us on this journey to unlock new frontiers in design and automation!
