---
tags:
  - y2s3-MnT
status: Ongoing
---
To create a system that harvests energy from your microbial fuel cell (MFC) to power a GSM module and AM radio via a Li-ion battery, here's a detailed, actionable circuit design:

---

## **System Overview**

1. **MFC (400mV, unstable)** → **LTC3108** (boosts voltage) → **Supercapacitor** (energy buffer) → **Li-ion Charge Controller** → **Li-ion Battery** → **Load (GSM + Radio)**.
    
2. **Key Challenges**: Low/fluctuating MFC voltage, high GSM current spikes, and safe battery charging.
    

---

## **Step 1: Energy Harvesting with LTC3108**

- **LTC3108 Setup**:
    
    - Connect the MFC to the **transformer primary** (terminals SW and GND on the LTC3108).
        
    - Use a **1:50 transformer** (e.g., Coilcraft LPR6235) to boost 400mV to ~3.3V.
        
    - Configure **VS1=VAUX** and **VS2=GND** for **4.1V output** (ideal for charging Li-ion via a charge controller).
        
    - Add input/output capacitors per datasheet (e.g., 1µF on VAUX, 10µF on VOUT).
        
- **Output**:
    
    - **VOUT**: 4.1V (regulated) to charge a supercapacitor.
        
    - **VSTORE**: Connect a **10F, 5.5V supercapacitor** to buffer energy.
        

---

## **Step 2: Supercapacitor to Li-ion Battery**

- **Charge Controller (TP4056)**:
    
    - Connect the supercapacitor (4.1V) to the TP4056’s **input**.
        
    - The TP4056 regulates charging to **4.2V** for the Li-ion battery.
        
    - Set charging current to **100–200mA** (adjust via PROG resistor) to match MFC’s low power.
        
- **Battery Protection**:
    
    - Use a **DW01A** protection circuit to prevent overcharge/discharge.
        
    - Include a **FS8205A** dual MOSFET for load switching.
        

---

## **Step 3: Power Delivery to Load**

- **Voltage Regulation**:
    
    - Use a **3.3V LDO** (e.g., MCP1700) for the AM radio and microcontroller.
        
    - For GSM (3.4–4.4V), connect directly to the battery.
        
- **Power Management**:
    
    - Add a **load switch** (e.g., TPS22860) to enable/disable the GSM module via a microcontroller.
        
    - Use **deep-sleep modes** for the GSM/radio when idle.
        

---

## **Step 4: Circuit Diagram**

text
```
[MFC (0.4V)]      
│ 
▼   
[LTC3108 + Transformer] → [VOUT (4.1V)]      
│ 
▼   
[Supercapacitor (10F, 5.5V)] → [TP4056 Charge Controller] → [Li-ion Battery (3.7V, 2000mAh)]      
│  
▼   
[Loads: GSM Module, AM Radio, Piezo Speaker]
```


---

## **Component Selection Table**

|Component|Purpose|Example Part|
|---|---|---|
|**LTC3108**|Boosts 0.4V → 4.1V|DC1582B-A eval board|
|**Transformer**|Step-up ratio 1:50|Coilcraft LPR6235|
|**Supercapacitor**|Energy buffer|Eaton XL60-506R7107-R|
|**Charge Controller**|Safe Li-ion charging|TP4056 module|
|**Battery**|Energy storage|18650 Li-ion (3.7V)|
|**LDO Regulator**|4.1V → 3.3V for radio|MCP1700-3302E|

---

## **Key Considerations**

1. **MFC Stability**:
    
    - Add a **low-leakage diode** (e.g., BAT54) to prevent reverse current from the supercapacitor to the MFC.
        
    - Use a **buffer capacitor** (1000µF) at the MFC output to smooth fluctuations.
        
2. **Efficiency**:
    
    - The LTC3108 has ~40% efficiency at 0.4V input. Expect **~40µW** harvested from a typical MFC.
        
    - A 2000mAh Li-ion battery requires **7.4Wh**; charging it would take **~7.4Wh / 0.00004W ≈ 185,000 hours** (impractical).
        
    - **Solution**: Use a **smaller battery** (e.g., 100mAh) and prioritize duty-cycling the GSM/radio.
        
3. **GSM Current Spikes**:
    
    - The Li-ion battery must supply **2A peaks**. Use a high-drain cell (e.g., Samsung INR18650-25R).
        
    - Place a **100µF ceramic capacitor** near the GSM module to handle transient loads.
        

---

## **Expected Performance**

- **Daily Energy Harvested**: ~0.96mWh (40µW × 24h).
    
- **GSM Call Energy Use**: ~600mWh per 2-minute call (2A × 3.7V × 0.033h).
    
- **Conclusion**: This system can support **~1 short call every 2 months** under ideal conditions. For practical use, scale up the MFC or add solar assist.
    

---

## **Improvements**

- **MFC Stacking**: Connect multiple MFCs in series to increase voltage.
    
- **Hybrid Harvesting**: Add a small solar panel to supplement energy.
    
- **Ultra-Low-Power Design**: Use a Nordic nRF9160 (LTE-M/NB-IoT) instead of GSM for lower power.
    

Let me know if you need help refining specific sections!

---

Answer from Perplexity: pplx.ai/share