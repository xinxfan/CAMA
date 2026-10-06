## 1. Overview
This artifact supports the experimental results reported in the paper and includes:
- Implementations of **three collusive adversarial attacks**:
  - CMA:Collective Malicious Agents
  - DMA:Disguised Malicious Agents
  - SMA:Disguised Malicious Agents
- A unified **training and execution pipeline**
- Reproducible experiment configurations and result aggregation

## 2. Repository Structure
The repository is organized as follows:
    cama_smac/
    ├── results/ # Experiment outputs
    │ ├── models/ # Saved model checkpoints
    │ ├── sacred/ # Sacred experiment logs
    │ └── tb_logs/ # TensorBoard logs
    ├── smac/ # SMAC environment wrapper
    │ ├── smac/
    │ │ ├── bin/ # SMAC binaries (excluded in anonymous release)
    │ │ └── env/ # Environment definitions
    │ └── examples/ # Example scripts
    ├── src/ # Core implementation
      ├── components/ # Core data structures and buffers
      ├── config/ # Algorithm and environment configurations
      ├── controllers/ # Multi-agent controllers (MACs)
      ├── envs/ # Environment interfaces
      ├── learners/ # Learning algorithms 
      ├── modules/ # The agent networks
      ├── runners/ # Parallel runners
      ├── utils/ # Utility functions
      ├── main.py # Entry point for experiments
      └── run.py # Training and evaluation pipeline

## 3. Environment Setup
All required Python dependencies are listed in `requirements.txt`.

## 4. Running Experiments
### 4.1 Training
#### Step 1: Install SMAC

      ```bash
      cd ami_smac/smac/
      pip install -e .
      ```
#### Step 2: Install Python Dependencies

      ```bash
      pip install -r requirements.txt
      ```
#### Step 3: Install StarCraft II

      ```bash
      sh install_sc2.sh
      ```
#### Step 4: Training Normal Policies

      ```bash
      python -u src/main.py --config=mappo --env-config=sc2
      ```
#### Step 5: Training CMA

      ```bash
      python -u src/main.py --config=mappo_cama --env-config=sc2_policy
      ```
#### Step 6: Training DMA and SMA (Stealth Model)
  Before training, set the following configuration options:
    - `train_stealth_model: True`
    - `use_stealth_model: False`
    

    ```bash
      python -u src/main.py --config=mappo_cama --env-config=sc2_policy
    ```

### 4.2 Evaluation
  Before evaluation, set the following configuration option:
    - `evaluate: True`
#### Evaluating CMA
  Set the following configuration option:
    - `train_stealth_model: False`
    - `use_stealth_model: False`

    ```bash
    python -u src/main.py --config=mappo_cama --env-config=sc2_policy
    ```
#### Evaluating DMA
  Set the following configuration option:
    - `train_stealth_model: False`
    - `use_stealth_model: True`
    - `attack_level: L2`

    ```bash
    python -u src/main.py --config=mappo_cama --env-config=sc2_policy
    ```
#### Evaluating SMA
  Set the following configuration option:
    - `train_stealth_model: False`
    - `use_stealth_model: True`
    - `attack_level: L3`

    ```bash
    python -u src/main.py --config=mappo_cama --env-config=sc2_policy


 #### Citation
  Men Niu, Xinxin Fan, Quanliang Jing, Shaoye Luo, Yunfeng Lu. CAMA: Exploring Collusive Adversarial Attacks in c-MARL. arXiv:2603.20390, 2026.
