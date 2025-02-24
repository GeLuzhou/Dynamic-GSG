
<p align="center">

  <h1 align="center">DynamicGSG: Dynamic 3D Gaussian Scene Graphs for Environment Adaptation</h1>
  <h3 align="center"></h3>
  <p align="center">
    <strong>Luzhou Ge</strong>
    ·
    <strong>Xiangyu Zhu</strong>
    ·
    <strong>Zhuo Yang</strong>
    ·
    <strong>Xuesong Li</strong>
  </p>
  <p align="center">
    <strong>Beijing Institute of Technology</strong>
  </p>
  <h3 align="center"><a href="https://arxiv.org/abs/2502.15309">Paper</a> | <a href="https://youtu.be/9QftApGbcSA">Video</a> </h3>
  <div align="center"></div>
</p>


<p align="center">
  <a href="">
    <img src="./assets/teaser.png" alt="Logo" width="100%">
  </a>
</p>

### Overview
> In real-world scenarios, the environment changes caused by agents or human activities make it extremely challenging for robots to perform various long-term tasks. To effectively understand and adapt to dynamic environments, the perception system of a robot needs to extract instance-level semantic information, reconstruct the environment in a fine-grained manner, and update its environment representation in memory according to environment changes. To address these challenges, We propose \textbf{DynamicGSG}, a dynamic, high-fidelity, open-vocabulary scene graph generation system leveraging Gaussian splatting. Our system comprises three key components: (1) constructing hierarchical scene graphs using advanced vision foundation models to represent the spatial and semantic relationships of objects in the environment, (2) designing a joint feature loss to optimize the Gaussian map for incremental high-fidelity reconstruction, and (3) updating the Gaussian map and scene graph according to real environment changes for long-term environment adaptation. Experiments and ablation studies demonstrate the performance and efficacy of the proposed method in terms of semantic segmentation, language-guided object retrieval, and reconstruction quality. Furthermore, we have validated the dynamic updating capabilities of our system in real laboratory environments.

### Installation


### TODO List
- [ ]  Realese supplementary experimental materials of Language-guided Object Retrieval on the Replica dataset.
- [ ]  Update detailed tutorial for DynamicGSG.
- [ ]  Open source deployment code using realsense d455.


# Dynamic Update Demo
<p align="center">
  <a href="">
    <img src="./assets/rgb_update.gif" width="50%">
    <img src="./assets/sem_update.gif" width="50%">
  </a>
</p>


### Acknowledgement

This work is built on many amazing research works and open-source projects, thanks a lot to all the authors for sharing!
- [SplaTAM](https://github.com/spla-tam/SplaTAM)
- [ConceptGraphs](https://github.com/concept-graphs/concept-graphs)
- [Vins-Fusion](https://github.com/HKUST-Aerial-Robotics/VINS-Fusion)

### Citation
If you find our paper and code useful, please cite us:
```bibtex
@misc{ge2025dynamicgsgdynamic3dgaussian,
      title={DynamicGSG: Dynamic 3D Gaussian Scene Graphs for Environment Adaptation}, 
      author={Luzhou Ge and Xiangyu Zhu and Zhuo Yang and Xuesong Li},
      year={2025},
      eprint={2502.15309},
      archivePrefix={arXiv},
      primaryClass={cs.RO},
      url={https://arxiv.org/abs/2502.15309}, 
}
```
