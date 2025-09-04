# Ethyl Benzene Production Optimization: Statics & Dynamics

## Project Overview

This project presents a comprehensive simulation study on **Ethyl Benzene (EB) production optimization** using Aspen Plus software. The work encompasses static optimization for minimum Total Annualized Cost (TAC) and dynamic process control analysis for an industrial-scale ethyl benzene production plant.

**Student:** Bhavishya Gupta  
**Roll Number:** 220295  
**Course:** CHE352 - Simulation Lab  

***

## 🎯 **Project Objectives**

1. **Static Optimization:** Minimize Total Annualized Cost (TAC) through systematic sensitivity analysis
2. **Dynamic Control:** Implement and tune process control systems for stable operation
3. **Process Analysis:** Evaluate material and energy balances across the production facility
4. **Economic Evaluation:** Calculate capital costs, operating costs, and payback periods

***

## 🏭 **Process Description**

The ethyl benzene production process consists of:

### **Main Equipment:**
- **2 CSTR Reactors** (200 µm³ each) - Alkylation reaction
- **3 Distillation Columns** - Product separation and purification
- **Heat Integration System** - Energy optimization

### **Key Streams:**
- **Feed Stream:** Ethylene (95 mol%) + Ethane (5 mol%) - 105.26 kmol/h
- **Benzene Makeup:** Fresh benzene feed for reaction
- **Product Stream:** High-purity ethyl benzene (99.9+ mol%)
- **Recycle Streams:** Benzene recovery and unreacted materials

***

## 📊 **Static Optimization Results**

### **Sensitivity Analysis Sequence:**

#### **1. Entrainer Rate Optimization**
- **Optimal Benzene Recycle Rate:** 193.507 kmol/h
- **Fresh Benzene Makeup:** 100.207 kmol/h
- **Energy Consumption:** 3690.219 kW

#### **2. Distillate Rate Optimization (Column 2)**
- **Benzene Purity in Recycle:** 0.989 mol fraction
- **Energy Reduction:** 3689.311 kW

#### **3. Reboiler Duty Optimization (Column 2)**
- **Benzene Impurity in C2 Bottoms:** 6.86 × 10⁻⁵
- **Significant Energy Reduction:** 3484.453 kW

#### **4. Distillate Ratio Optimization (Column 3)**
- **EB Impurity in Recycle:** 0.0012214
- **Final Optimized Energy:** 3483.458 kW

### **Material Balance Summary:**
| Stream | Flow Rate (kmol/h) | Key Components |
|--------|-------------------|----------------|
| Feed | 105.26 | Ethylene (95%), Ethane (5%) |
| Benzene Makeup | 100.207 | Pure Benzene |
| Product (C3 Distillate) | 99.9106 | Ethyl Benzene (99.9%) |
| C1 Distillate | 5.56054 | Light Components |

### **Energy Balance:**
| Equipment | Duty (kW) | Utility |
|-----------|-----------|---------|
| C1 Reboiler | 636.028 | High Pressure Steam |
| C2 Reboiler | 1011.8 | Medium Pressure Steam |
| C3 Reboiler | 1835.631 | High Pressure Steam |
| **Total Heating** | **3483.459** | - |
| **Total Cooling** | **-3804.491** | Cooling Water |

***

## 💰 **Economic Analysis**

### **Capital Cost Breakdown:**
| Component | Cost (×10⁶ $) |
|-----------|---------------|
| Column C1 | 0.2586 |
| Column C2 | 1.9992 |
| Column C3 | 4.4117 |
| **Total Capital Cost (TCC)** | **6.6696** |

### **Operating Costs:**
- **Yearly Operating Cost (YOC):** $1.0686 × 10⁶
- **Payback Period (PBP):** 3 years
- **Total Annualized Cost (TAC):** $3.2918 × 10⁶

***

## 🔧 **Advanced Optimization using fmincon**

### **Optimization Variables:**
- **br_p:** Benzene mole purity in recycle stream (0.9883)
- **deb_p:** Ethyl benzene impurity in C3 bottoms (0.0216)  
- **br_fr:** Benzene flow rate in recycle (209.9439 kmol/h)

### **Optimization Results:**
| Iteration | Initial Guess | Final TAC ($) |
|-----------|---------------|---------------|
| 1 | [0.96, 0.02, 190] | 1,747,200 |
| 2 | [0.96, 0.0222, 189.99] | 1,739,200 |
| 3 | [0.97, 0.0222, 189.99] | 1,732,100 |
| 4 | [0.98, 0.0222, 189.99] | 1,727,700 |
| 5 | [0.991, 0.0222, 189] | 1,724,500 |
| **6 (Final)** | **[0.991, 0.0222, 189]** | **1,723,900** |

**Final Optimized TAC: $1,723,900** (47.6% reduction from static cost analysis)

***

## 🎛️ **Dynamic Process Control**

### **Control Strategy Implementation:**

#### **Pressure Control (Ziegler-Nichols Tuning):**
| Controller | Gain (Kc) | Integral Time (τI) |
|------------|-----------|-------------------|
| C1_CondPC | 90.6326 | 1 min |
| C2_CondPC | 73.4499 | 1 min |
| C3_CondPC | 60.0014 | 1 min |

#### **Temperature Control (Tyreus-Luyben Tuning):**
| Controller | Gain (Kc) | Integral Time (τI) |
|------------|-----------|-------------------|
| CSTR1_TC | 14.5057 | 9.24 min |
| CSTR2_TC | 105.3682 | 11.88 min |
| C1_TopTC | 0.1133 | 11.88 min |
| C1_BotTC | 3.9789 | 7.92 min |
| C2_BotTC | 11.156 | 6.6 min |
| C3_BotTC | 83.53 | 3.96 min |

### **Disturbance Analysis:**

**Test Cases Evaluated:**
- ±10% Fresh ethylene flowrate changes
- ±4% Fresh ethylene composition changes

**Key Performance Indicators:**
- **Ethyl Benzene Purity:** Maintained at 99.9+ mol% despite disturbances
- **Temperature Control:** Stable reactor and column temperatures
- **Flow Control:** Effective manipulation of recycle streams

### **Control Performance:**
- **Settling Time:** < 40 hours for most disturbances
- **Overshoot:** Minimal for temperature and composition variables
- **Steady-State Error:** < 0.1% for critical process variables

***

## 🔬 **Technical Specifications**

### **Column Design Parameters:**
| Column | Trays | Diameter (m) | Reboiler Type | Condenser Type |
|--------|-------|--------------|---------------|----------------|
| C1 | 11 | 0.6695 | Partial | Partial |
| C2 | 24 | 1.2173 | Partial | Total |
| C3 | 29 | 1.3081 | Partial | Total |

### **Operating Conditions:**
- **CSTR Temperature:** 150°C (controlled)
- **Pressure:** Atmospheric operation
- **Heat Integration:** Steam levels (HP/MP/LP) and cooling water

***

## 💻 **Software & Methodology**

### **Simulation Environment:**
- **Aspen Plus:** Process simulation and optimization
- **MATLAB:** fmincon optimization algorithm implementation
- **Dynamic Simulation:** Controller tuning and disturbance analysis

### **Optimization Techniques:**
1. **Sequential Sensitivity Analysis:** Systematic parameter variation
2. **Constrained Optimization:** fmincon with multiple variables
3. **Controller Tuning:** Ziegler-Nichols and Tyreus-Luyben methods

***

## 📈 **Key Achievements**

✅ **47.6% TAC Reduction:** From $3.29M to $1.72M annually  
✅ **Robust Control System:** Stable operation under ±10% disturbances  
✅ **High Product Purity:** 99.9+ mol% ethyl benzene maintained  
✅ **Energy Integration:** Optimized heat exchange network  
✅ **Economic Viability:** 3-year payback period achieved  

***

*This project demonstrates comprehensive process systems engineering, combining steady-state optimization, dynamic control, and economic analysis for industrial ethyl benzene production.*
