## Table of Contents
- [Key Features](#key-features)
- [Methodology](#methodology)
- [Equations](#key-equations)
- [Assumptions](#key-assumptions)
- [Load Profile Creation](#load-profile-methodology)
- [Directory Structure](#directory-structure)
- [Dependencies](#dependencies)
- [Usage](#usage)



## Mathematical Formulation
Minimize: C<sub>total</sub> = C<sub>pv</sub> × P<sub>pv</sub> + C<sub>batt</sub> × E<sub>batt</sub>
- *C<sub>pv</sub>*: PV capital cost (€/kW)  
- *P<sub>pv</sub>*: PV capacity (kW)  
- *C<sub>batt</sub>*: Battery capital cost (€/kWh)  
- *E<sub>batt</sub>*: Battery energy capacity (kWh)

### Energy Balance (∀ t ∈ T)

P<sub>pv</sub> × CF<sub>pv</sub>(t) + P<sub>dis</sub>(t) = L(t) + P<sub>ch</sub>(t) + P<sub>curt</sub>(t)

- *CF<sub>pv</sub>(t)*: PV capacity factor [0-1]  
- *P<sub>dis</sub>(t)*: Discharge power (kW)  
- *L(t)*: Load demand (kW)  
- *P<sub>ch</sub>(t)*: Charge power (kW)  
- *P<sub>curt</sub>(t)*: Curtailed power (kW)

### Battery Dynamics

SOC(t) = SOC(t-1) + η<sub>ch</sub> × P<sub>ch</sub>(t) - (P<sub>dis</sub>(t)/η<sub>dis</sub>)
SOC(0) = 0.1 × E<sub>batt</sub>
0 ≤ SOC(t) ≤ E<sub>batt</sub>

- *η<sub>ch</sub>, η<sub>dis</sub>* = 0.9 (efficiencies)

### Load Profile Components

- Base Load = 1.2 + 0.8 × sin(2π×(h(t)-6)/24)
- Residential = 0.6 × [exp(-0.5×(h(t)-7)² + 0.8×exp(-0.3×(h(t)-19)²)]
- Commercial = 0.5 + 0.4 × exp(-0.2×(h(t)-13)²)
- Agricultural = 0.3 × (1 - exp(-0.5×h(t))) × [h(t) < 18]

Total Load(t) = 8 × [0.6(Base + Residential) + 0.3Commercial + 0.1Agricultural]
× (1 + 0.05ε) + 0.3ε


### Technical Constraints

P<sub>pv</sub> ≥ max(L(t)) / max(CF<sub>pv</sub>(t))

P<sub>dis</sub>(t) ≤ E<sub>batt</sub> - SOC(t-1)



## Notation Key
| Symbol        | Description                      |
|---------------|----------------------------------|
| *CF<sub>pv</sub>* | PV capacity factor             |
| *SOC*         | State of Charge                  |
| *η<sub>ch</sub>*  | Charge efficiency              |
| *η<sub>dis</sub>* | Discharge efficiency           |
| *h(t)*        | Hour of day (0-23)              |
