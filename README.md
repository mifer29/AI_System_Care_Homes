# Intelligent System for Autonomous Assistance in Elderly Care Homes

This repository contains the full implementation of an intelligent monitoring system designed for elderly care environments. The system processes heterogeneous sensor data, predicts resident behavioral states, and generates safety alerts under simulated real time conditions.

The project follows a hybrid architecture that combines supervised learning, deterministic heuristic rules, and a language-based decision-making agent. The main objective is to prioritize interpretability, safety, and real-time operation rather than end-to-end black box modeling.

This project has been developed with the collaboration of the company NFOQUE.



## Project structure

The repository is organized around a single executable notebook that contains the complete pipeline.

```text
├── Final_Code_Project_NFOQUE.ipynb # Main notebook with full implementation
├── Data/
│ └── Datasets
│ └── best_lstm_attention_model.pt
├── README.md
```


## Phase 1 – Exploration and unsupervised analysis

This phase focuses on understanding resident behavior without relying on labeled data.

Main components:
- Data loading and preprocessing
- Exploratory data analysis
- Resident-specific baseline computation
- Behavioral state definition
- Unsupervised detection of unusual patterns

The goal of this phase is to provide a structured understanding of normal behavior and support later alert definition.



## Phase 2 – Supervised modeling and alert design

### Behavioral state prediction
- An LSTM-based neural network with an attention mechanism is trained to predict resident behavioral states from sequential sensor data.
- The architecture is intentionally simple to ensure robustness and stability.
- Model evaluation focuses on F1 score due to class imbalance.

### Heuristic alert system
- Deterministic rules classify situations into four alert levels: GREEN, YELLOW, ORANGE, and RED.
- Rules combine physiological signals, motion indicators, environmental variables, time context, and resident-specific baselines.
- Most situations are handled at this level in an interpretable and computationally efficient way.

### Decision-making agent
- Observations that cannot be confidently classified by heuristic rules are marked as ambiguous.
- These cases are escalated to a language-model-based agent.
- Two interchangeable backends are supported:
  - OpenAI API
  - Local LLM executed via Ollama (integrated using LangChain)
- The agent receives a structured semantic summary and is constrained to return a single alert level and action, prioritizing safety.



## Phase 3 – Real-time operation and visualization

### Real-time simulation
- Sensor data is processed sequentially, minute by minute, without access to future information.
- A generator simulates a live data stream.
- At each time step:
  - Resident states are updated
  - Alerts are generated
  - Ambiguous cases are escalated to the agent
  - Decisions are logged in memory

### Interactive dashboard
- Implemented using Gradio
- Provides:
  - A global overview of residents through color-coded indicators
  - Detailed views per resident
  - Short-term time-series plots (heart rate and accelerometer)
  - Behavioral state timeline visualization
  - Recent alert log

The dashboard is designed to support supervision and system evaluation rather than autonomous intervention.

---

## Design principles

- Safety-first decision making
- Interpretability over black-box complexity
- Hybrid heuristics + agent architecture
- Causal real-time processing
- Modular and extensible system design



## Requirements

Main dependencies include:
- Python 3.10+
- PyTorch
- Pandas, NumPy
- Scikit-learn
- Gradio
- LangChain
- Ollama (optional, for local LLM execution)



## How to run

1. Clone the repository
2. Install the required dependencies
3. Open and run `Final_Code_Project_NFOQUE.ipynb`
4. Execute all cells to train or load the model and launch the dashboard



## Notes

- The dataset used is simulated and intended for academic evaluation.
- Persistent logging and deployment infrastructure are out of scope.
- The system is presented as a proof of concept.




