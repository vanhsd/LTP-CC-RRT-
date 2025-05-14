# Trajectory Prediction Comparison for Autonomous UAVs

This repository contains MATLAB code for comparing different trajectory prediction models in autonomous UAV navigation scenarios. The framework evaluates various deep learning-based prediction models in complex 3D environments with both static and dynamic obstacles.

![Trajectory Comparison 3D View](figures/trajectory_comparison_3d.png)



## Overview

The main script implements a comprehensive comparison framework for evaluating several trajectory prediction methods:

- Traditional LSTM
- LSTM with Kalman Filter (LSTM-KF)
- Attention-based LSTM
- Bidirectional LSTM
- Graph Neural Network (GNN)
- Multi-Modal Prediction Transformer (MMPT)
- Social LSTM
- Constant Velocity (baseline)
- No Prediction (baseline)

The evaluation is done in a 3D environment with terrain features, static obstacles (cylinders and walls), and dynamic obstacles (other moving agents).

![3D Environment with Terrain and Obstacles](figures/environment.png)

## Key Features

- **Modular Prediction Models**: Includes implementation for various state-of-the-art trajectory prediction models
- **Chance-constrained RRT Planning**: Path planning with probabilistic collision checking
- **3D Environment Simulation**: Realistic environment with terrain, obstacles, and dynamic agents
- **Comprehensive Evaluation Metrics**: Based on the SAEPSO paper constraints and fitness functions
- **Publication-ready Visualizations**: Generates high-quality figures for analysis and presentation

## Requirements

- MATLAB (tested on R2021a or newer)
- Deep Learning Toolbox
- Statistics and Machine Learning Toolbox

## Usage

1. Place all model files (`.mat` files) in the same directory as the main script
2. Run the main script:
   ```matlab
   run_model_comparison
   ```
3. Results will be saved to:
   - `trajectory_prediction_comparison_results.mat`: Results structure with metrics
   - `basic_metrics.csv`, `constraint_metrics.csv`, `fitness_metrics.csv`: Metrics in CSV format
   - `figures/`: Directory with publication-ready figures

### Example Results

The framework generates several visualizations to help analyze the results:

#### Trajectory Comparison (Top View)
![Trajectory Comparison Top View](figures/trajectory_comparison_top.png)

#### Performance Metrics Comparison
![Metrics Comparison](figures/metrics_comparison.png)

#### LSTM Prediction Visualization
![LSTM Prediction with Uncertainty](figures/lstm_prediction.png)

## Model Structure

Each model file should contain the pretrained neural network and possibly additional metadata. The expected format varies by model type, but generally includes:

- `net`: The trained neural network
- `metadata`: Structure with information like input/output dimensions
- Model-specific fields (e.g., `kf` for Kalman filter parameters in LSTM-KF)

## Metrics

The framework evaluates trajectories using several metrics:

### Basic Metrics
- Goal reached rate (%)
- Path length (m)
- Execution time (s)
- Computation time (s)
- Minimum clearance (m)
- Average clearance (m)
- Smoothness (rad)

### Constraint Violation Metrics
- Height violation (%)
- Turn angle violation (%)
- Climb angle violation (%)

### Fitness Components (SAEPSO)
- Path cost (F1)
- Safety cost (F2)
- Height variation cost (F3)
- Angle variation cost (F4)
- Combined fitness cost

![Performance Metrics Visualization](figures/metrics_visualization.png)

## Environment Configuration

The simulated environment includes:

- 3D terrain with variable height
- Static obstacles (cylinders and walls)
- Dynamic obstacles with different motion models
- Start and goal positions
- UAV constraints (speed, acceleration, safety margins)

## Functions Overview

The code is organized into several key functions:

- `runComparison`: Main comparison loop running multiple trials
- `predictObstacleTrajectory`: Dispatcher for different prediction models
- `chanceConstrainedRRTPlanner`: Path planning with uncertainty
- `computeTrajectoryMetrics`: Compute comprehensive metrics
- `visualizeResults`: Visualize results in 3D
- `generatePublicationFigures`: Create publication-quality figures

## Prediction Models

### Traditional LSTM
Basic LSTM model that predicts future positions sequentially.

### LSTM-KF
Hybrid approach combining LSTM prediction with Kalman filter refinement.

### Attention LSTM
LSTM with attention mechanism to focus on relevant parts of trajectory history.

### Bidirectional LSTM
LSTM that processes trajectory history in both forward and backward directions.

### GNN (Graph Neural Network)
Uses graph structure to model interactions between multiple agents.

### MMPT (Multi-Modal Prediction Transformer)
Transformer-based model that predicts multiple possible trajectories with confidences.

### Social LSTM
LSTM variant that models social interactions between agents.

## Citation

If you use this code in your research, please cite our work:

```bibtex
@article{author2023trajectory,
  title={Trajectory Prediction Comparison for Autonomous UAVs},
  author={Author, A.},
  journal={Journal of Autonomous Robots},
  year={2023}
}
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Converting PDF Figures to PNG for GitHub

Since GitHub's markdown doesn't directly render PDF files in README displays, you'll need to convert the generated PDF figures to PNG format for proper display. You can do this:

### In MATLAB:
Add these lines at the end of `generatePublicationFigures` function:

```matlab
% Also save figures as PNG for GitHub
print(fig1, '-dpng', '-r300', 'figures/environment.png');
print(fig2, '-dpng', '-r300', 'figures/trajectory_comparison_top.png');
print(fig3, '-dpng', '-r300', 'figures/trajectory_comparison_3d.png');
print(fig4, '-dpng', '-r300', 'figures/metrics_comparison.png');
print(fig5, '-dpng', '-r300', 'figures/lstm_prediction.png');
```

### Using Command Line Tools:
You can use tools like `pdftoppm` or `convert` (from ImageMagick):

```bash
# Using pdftoppm
pdftoppm -png -r 300 figures/environment.pdf figures/environment

# Using ImageMagick
convert -density 300 figures/environment.pdf figures/environment.png
```

### Update Image References
After converting to PNG, update the README image references from `.pdf` to `.png`:

```markdown
![3D Environment](figures/environment.png)
```

## Showcase of Results

Here's an example of how the different trajectory prediction methods compare:

![Trajectories Comparison](figures/trajectory_comparison.png)

## Acknowledgments

- Based on research in trajectory prediction for autonomous navigation
- Incorporates metrics from the SAEPSO paper for comprehensive evaluation
