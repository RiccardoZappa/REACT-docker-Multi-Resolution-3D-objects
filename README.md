# REACT-docker

Docker deployment for REACT.

Follow the instructions [here](https://github.com/aalto-intelligent-robotics/REACT?tab=readme-ov-file#-building-react) to get started with REACT.

If you find this code relevant for your work, please consider citing our paper. A bibtex entry is provided below:

```bibtex
@misc{nguyen2025reactrealtimeefficientattribute,
      title={REACT: Real-time Efficient Attribute Clustering and Transfer for Updatable 3D Scene Graph}, 
      author={Phuoc Nguyen and Francesco Verdoja and Ville Kyrki},
      year={2025},
      eprint={2503.03412},
      archivePrefix={arXiv},
      primaryClass={cs.RO},
      url={https://arxiv.org/abs/2503.03412}, 
}
```
# Multi-Resolution 3D Object Representation

This work introduces a significant enhancement to the Hydra framework, leveraging the perception node introduced by the REACT framework to obtain multiple and customizable resolution for the 3D object nodes.

## Configuration

The parameters for the object fusion and refinement process can be tuned in the `Hydra-Stretch repository`under `/config/flat_inst/hydra/frontend_config.yaml` file(simulation data) and `/config/flat_inst/hydra/frontend_config.yaml` file(real data).This allows you to adapt the process for different object categories, as a 'sofa' might need different settings than a 'cup'.

Here is an example of the configuration file structure:

```yaml
# config/flat_inst/hydra/frontend_config.yaml

  per_object_params:
    # Default values used for any object NOT listed below
    default:
      min_cluster_size: 40
      cloud_downsampling: 0.1 # downsampling resolution of the pointclouds for the objects
      matching_threshold: 0.01  #used for confrontation between centroid of cluster instance in the update graph function
      max_correspondence_distance: 0.05 # Max distance between points to be considered a correspondence in the iterative closest point algorithm that matches the point clouds over time (meters)
    # Override for Cup (Label 8)
    "8":
      min_cluster_size: 10
      cloud_downsampling: 0.0005
      matching_threshold: 0.0001
      max_correspondence_distance: 0.001
    # Override for Bed (Label 2)
    "2":
      min_cluster_size: 40
      cloud_downsampling: 0.05
    # Override for Floor Lamp (Label 13)
    "13":
      min_cluster_size: 40
      cloud_downsampling: 0.005
      matching_threshold: 0.05
    # Override for Coffee Table (Label 7)
    "7":
      min_cluster_size: 40
      cloud_downsampling: 0.05
    # Override for Chair (Label 6)
    "6":
      min_cluster_size: 40
      cloud_downsampling: 0.005
      matching_threshold: 0.0005
      max_correspondence_distance: 0.001
    # Override for Sofa (Label 20)
    "20":
      min_cluster_size: 40
      cloud_downsampling: 0.05
    # Override for journal (Label 14)
    "14":
      min_cluster_size: 20
      cloud_downsampling: 0.0005
      matching_threshold: 0.0001
      max_correspondence_distance: 0.001
