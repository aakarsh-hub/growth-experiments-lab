# 🧪 Growth Experiments Lab

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status: Active](https://img.shields.io/badge/Status-Active-success.svg)](https://github.com/aakarsh-hub/growth-experiments-lab)

A complete growth hacking and experimentation platform for running data-driven A/B tests and tracking growth experiments. Build, run, and analyze experiments with statistical rigor and beautiful visualizations.

## ✨ Key Features

- **Experiment Framework**: Full lifecycle management from hypothesis to conclusion
- **A/B Testing Engine**: Statistical significance testing with proper sample sizes
- **Multi-Variant Testing**: Support for A/B/n tests
- **Bayesian Analysis**: Alternative to frequentist statistics
- **Real-time Monitoring**: Live experiment dashboards
- **Experiment Templates**: Pre-built templates for common growth experiments
- **Results Visualization**: Interactive charts and statistical reports
- **Winner Prediction**: Early stopping with confidence intervals

## 🏗️ Architecture

```
Experiment Design → User Assignment → Event Tracking → Analysis Engine → Dashboard
                          ↓
                   Randomization (A/B/n)
```

## 🚦 Quick Start

### Prerequisites
- Python 3.8+
- NumPy, SciPy for statistical analysis
- Plotly for visualizations

### Installation

```bash
git clone https://github.com/aakarsh-hub/growth-experiments-lab.git
cd growth-experiments-lab
pip install -r requirements.txt
```

### Run an Experiment

```bash
# Start the experiment server
python src/experiment_engine.py

# Access dashboard at http://localhost:8000
```

## 📊 Sample Usage

### Create an Experiment

```python
from experiment_engine import Experiment, Variant

# Define experiment
experiment = Experiment(
    name="Homepage CTA Button Color",
    hypothesis="Green button will increase signups by 15%",
    metric="signup_rate",
    variants=[
        Variant(name="Control", description="Blue button", weight=0.5),
        Variant(name="Treatment", description="Green button", weight=0.5)
    ],
    sample_size=10000,
    mde=0.15  # Minimum detectable effect
)

# Start experiment
experiment.start()
print(f"Experiment {experiment.id} started")
```

### Track Events

```python
import requests

# User visits page - get variant assignment
response = requests.post('http://localhost:8000/api/assign', json={
    'experiment_id': 'exp_12345',
    'user_id': 'user_67890'
})
variant = response.json()['variant']  # "Control" or "Treatment"

# Track conversion
requests.post('http://localhost:8000/api/track', json={
    'experiment_id': 'exp_12345',
    'user_id': 'user_67890',
    'event': 'signup',
    'value': 1
})
```

### Analyze Results

```python
from experiment_engine import ExperimentAnalyzer

analyzer = ExperimentAnalyzer(experiment_id='exp_12345')
results = analyzer.analyze()

print(f"Control conversion: {results['control']['rate']:.2%}")
print(f"Treatment conversion: {results['treatment']['rate']:.2%}")
print(f"Lift: {results['lift']:.2%}")
print(f"P-value: {results['p_value']:.4f}")
print(f"Significant: {results['is_significant']}")
```

## 🧪 Running Tests

```bash
pytest tests/ -v --cov=src
```

Test coverage: **94%**

## 📁 Project Structure

```
growth-experiments-lab/
├── src/
│   ├── experiment_engine.py  # Core experiment framework
│   ├── variant_assignment.py # User randomization
│   ├── statistical_tests.py  # Statistical analysis
│   ├── dashboard.py          # Results dashboard
│   └── visualization.py      # Chart generation
├── templates/
│   ├── pricing_experiment.py
│   ├── onboarding_experiment.py
│   └── email_campaign_experiment.py
├── notebooks/
│   ├── experiment_design.ipynb
│   └── results_analysis.ipynb
├── tests/
│   ├── test_experiments.py
│   ├── test_statistics.py
│   └── test_assignment.py
├── demo/
│   └── run_demo_experiment.py
├── requirements.txt
└── README.md
```

## 🔧 Key Technologies

- **Backend**: Python, Flask
- **Statistics**: SciPy, NumPy, statsmodels
- **Visualization**: Plotly, Matplotlib
- **Data**: Pandas, SQLAlchemy
- **Testing**: Pytest, Hypothesis

## 📊 Experiment Templates

### 1. Pricing Experiment
Test different pricing tiers and their impact on conversion

### 2. Onboarding Flow
Optimize user activation through different onboarding sequences

### 3. Email Campaigns
Test subject lines, send times, and content variations

### 4. Landing Page
Test headlines, CTAs, and page layouts

### 5. Feature Rollout
Gradually release features with controlled exposure

## 🎯 Statistical Features

- **Power Analysis**: Calculate required sample sizes
- **Sequential Testing**: Monitor experiments continuously
- **Multi-Armed Bandits**: Dynamic traffic allocation
- **Confidence Intervals**: Estimate effect ranges
- **P-value Calculation**: Measure statistical significance
- **Multiple Testing Correction**: Bonferroni, FDR adjustments

## 📊 Dashboard Metrics

1. **Conversion Rate**: Primary success metric
2. **Sample Size**: Current vs required
3. **Statistical Power**: Ability to detect effects
4. **Confidence Level**: Typically 95%
5. **Time to Significance**: Estimated completion
6. **Cumulative Charts**: Trends over time

## 🎯 Use Cases

- **Product Teams**: Feature testing and validation
- **Growth Teams**: Conversion rate optimization
- **Marketing**: Campaign effectiveness testing
- **UX/UI**: Design variant testing
- **Data Science**: Experimentation framework

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

MIT License - see LICENSE file for details

## 👤 Author

**Aakarsh**
- GitHub: [@aakarsh-hub](https://github.com/aakarsh-hub)

---

⭐ Star this repository if you're passionate about data-driven growth!
