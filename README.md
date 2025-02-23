
# Renewable Energy Potential Analysis for Ethiopia
## Project Overview
This project analyzes renewable energy potential in Ethiopia through two complementary approaches:

1. **National Annual Analysis**: Land availability assessment for wind/PV across Ethiopia

2. **City Diurnal Analysis**: Optimization model for PV+battery systems in Arsi Negele city

## Key Features
- Land Availability Analysis

  - Exclusion layers: Population density, protected areas, elevation

  - Capacity potential calculation using Atlite

  - Spatial visualization of eligible areas

  - Energy System Optimization

  - Hourly resolution optimization model

  - PV + battery storage system

  - Synthetic load profile generation

  - Performance metrics calculation
## Key Equations
### Objective Function (Minimize Total Cost):

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

- SOC(t) = SOC(t-1) + η<sub>ch</sub> × P<sub>ch</sub>(t) - (P<sub>dis</sub>(t)/η<sub>dis</sub>)
- SOC(0) = 0.1 × E<sub>batt</sub>
- 0 ≤ SOC(t) ≤ E<sub>batt</sub>

- *η<sub>ch</sub>, η<sub>dis</sub>* = 0.9 (efficiencies)



### Technical Constraints

P<sub>pv</sub> ≥ max(L(t)) / max(CF<sub>pv</sub>(t))

P<sub>dis</sub>(t) ≤ E<sub>batt</sub> - SOC(t-1)

## load-profile-generation

- Sector-Specific Patterns:

- Residential: Dual peaks (8 AM & 8 PM) with elevated base load

- Commercial: Midday peak (1 PM) with weekend reduction

- Agricultural: Dual daytime peaks (8 AM & 2 PM)

### Realistic Scaling:

- Peak demand ≈5-6.5 MW

- Average demand ≈3.5-4 MW

- Minimum nighttime demand ≈1.5-2 MW

### Demand Allocation:

- Residential: 50%

- Commercial: 30%

- Agricultural: 20%

### Real-World Considerations:

- Weekend commercial reduction (40% decrease)

- Agricultural activity limited to daylight hours

- Random variations in demand (±10-20%)



## Notation Key
| Symbol        | Description                      |
|---------------|----------------------------------|
| *CF<sub>pv</sub>* | PV capacity factor             |
| *SOC*         | State of Charge                  |
| *η<sub>ch</sub>*  | Charge efficiency              |
| *η<sub>dis</sub>* | Discharge efficiency           |
| *h(t)*        | Hour of day (0-23)              |
