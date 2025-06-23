# 🧮 Solar System Calculation Methodology

This document explains the mathematical formulas and methodology used in the Off-Grid Solar Calculator.

## 📊 Overview

The calculator uses industry-standard formulas with safety margins to ensure reliable off-grid solar system operation. All calculations follow electrical engineering principles and real-world solar installation practices.

## ⚡ Energy Consumption Calculations

### Basic Power Calculation
```
Actual Wattage = Rated Wattage / (Efficiency / 100)
```

### Daily Energy Consumption
```
Daytime Energy (Wh) = Σ(Device Wattage × Quantity × Daytime Hours)
Nighttime Energy (Wh) = Σ(Device Wattage × Quantity × Nighttime Hours)
Total Daily Energy (Wh) = Daytime Energy + Nighttime Energy
```

### Peak Power Demand
```
Peak Power (W) = Σ(Device Actual Wattage × Quantity)
```

## 🌞 Solar Panel Sizing

### Energy with System Losses
```
Energy with Losses = Total Daily Energy / System Efficiency
```

### Generation Pattern Factors
- **Linear Pattern**: Standard sun hours
- **Gaussian Pattern**: Sun hours × 1.15 (accounts for peak generation)
- **Custom Pattern**: User-defined distribution

### Solar Panel Capacity
```
Minimum Solar Watts = Energy with Losses / (Effective Sun Hours × Panel Derating)
Recommended Solar Watts = Minimum Solar Watts × (1 + Safety Margin)
```

**Where:**
- **Panel Derating**: Accounts for temperature, dust, aging (typically 80%)
- **Safety Margin**: Additional capacity for reliability (typically 25%)

## 🔋 Battery Bank Sizing

### Net Battery Energy Requirement
```
Net Battery Energy = Nighttime Energy + max(0, Daytime Energy - Available Solar Energy)
```

### Battery Capacity Calculation
```
Battery Energy Needed = (Net Battery Energy × Autonomy Hours / 24) / Depth of Discharge
Battery Ah Needed = Battery Energy Needed / System Voltage
```

**Autonomy Periods:**
- **Days**: Converted to hours (days × 24)
- **Hours**: Direct input

**Depth of Discharge (DOD) Guidelines:**
- Lead-Acid batteries: 50% (longer life)
- AGM batteries: 70%
- Lithium batteries: 80-90%

## 🔌 Inverter Sizing

### Inverter Capacity
```
Inverter Capacity = Peak Power Demand × (1 + Safety Margin)
```

**Safety Margin**: Typically 25% to handle startup surges and future expansion.

## ⚙️ Charge Controller Sizing

### Controller Current Rating
```
Controller Current = (Solar Panel Watts / System Voltage) × (1 + Safety Margin × 0.5)
```

**Note**: MPPT controllers are recommended for maximum efficiency.

## 🎯 Safety Factors and Derating

### System Efficiency Factors
- **Inverter Efficiency**: 85-95%
- **Battery Efficiency**: 85-95%
- **Wiring Losses**: 2-5%
- **Overall System Efficiency**: Typically 80%

### Panel Derating Factors
- **Temperature losses**: 10-15%
- **Dust and soiling**: 5%
- **Aging**: 2-3%
- **Shading**: Variable
- **Overall Derating**: Typically 80%

## 📈 Advanced Calculations

### Generation Pattern Analysis

#### Gaussian Distribution (Peak at Midday)
```
Generation(hour) = exp(-0.5 × ((hour - 12) / (sun_hours / 4))²)
```

This models realistic solar generation where peak power occurs around noon.

#### Linear Distribution
```
Generation(hour) = constant between sunrise and sunset, zero otherwise
```

### Autonomy Calculations

#### Battery Reserve Calculation
```
Reserve Energy = (Autonomy Hours / 24) × Daily Energy Consumption
Total Battery Capacity = Reserve Energy / Depth of Discharge
```

## 🔧 System Voltage Selection

### Voltage Guidelines
- **12V**: Small systems (<400W)
- **24V**: Medium systems (400W-1500W)
- **48V**: Large systems (>1500W)

### Current Calculations
```
DC Current = Power / Voltage
AC Current = Power / (Voltage × Power Factor)
```

## 📋 Example Calculation

### System Requirements
- Location: Colombo, Sri Lanka (5.8 sun hours)
- Load: 100W LED lights × 6 hours
- System Voltage: 24V
- Autonomy: 2 days

### Step-by-Step Calculation

1. **Daily Energy**: 100W × 6h = 600 Wh/day
2. **Energy with Losses**: 600 Wh / 0.8 = 750 Wh
3. **Solar Panel Size**: 750 Wh / (5.8h × 0.8) = 161W minimum
4. **With Safety Margin**: 161W × 1.25 = 201W recommended
5. **Battery Capacity**: (600 Wh × 48h / 24h) / 0.5 = 2400 Wh = 100 Ah at 24V
6. **Inverter Size**: 100W × 1.25 = 125W minimum

## 🌍 Location-Specific Data

### Solar Irradiance Database
The calculator includes average annual solar data for major cities:

```javascript
const solarData = {
    'colombo': { sunHours: 5.8, lat: 6.9271, lon: 79.8612 },
    'new_york': { sunHours: 4.2, lat: 40.7128, lon: -74.0060 },
    // ... more cities
};
```

### GPS-Based Estimation
For unknown locations, solar hours are estimated using latitude:
```
Estimated Sun Hours = 6 - |latitude| × 0.05
```

## ⚠️ Important Notes

1. **Professional Consultation**: These calculations provide estimates. Consult qualified professionals for actual installations.

2. **Local Variations**: Actual solar irradiance varies by season, weather, and microclimate.

3. **Load Variations**: Real-world energy consumption may differ from calculated values.

4. **Component Specifications**: Always verify actual component specifications with manufacturers.

5. **Safety Codes**: Follow local electrical codes and safety standards.

## 📚 References

- IEEE Standards for Solar Power Systems
- National Electrical Code (NEC) Article 690
- International Electrotechnical Commission (IEC) Standards
- Solar Power Your Home For Dummies (Rik DeGunther)
- Solar Electricity Handbook (Michael Boxwell)

---

*This methodology ensures reliable, safe, and efficient off-grid solar system designs suitable for real-world applications.*