---

# 🌦️ Weather Station Hardware Platform  
*A mixed‑signal embedded system designed in Altium Designer, featuring STM32L4, nRF24L01, and a fully modeled PDN.*

---

![3D Board View](Pictures\STM32RF_Altium.PNG)

---

## 📘 Overview  
This project is a custom **Weather Station hardware platform** designed from scratch in **Altium Designer**. It integrates:

- **STM32L432** Microcontroller  
- **nRF24L01+** 2.4 GHz RF transceiver  
- **BME280** Temperature, humidity, pressure sensor  
- **MCP73871** Battery charger + power‑path management 
- **Micro USB Connector** USB FS interface   

The goal was to showcase Altium Designer use while developing professional‑grade skills in:

- PCB architecture and layout  
- PDN modeling and simulation  
- RF‑aware routing  
- Decoupling strategy and capacitor selection  
- Altium Designer workflows  
- Hardware bring‑up planning  
- Documentation and reproducibility  

This README documents the design, the engineering decisions, and the lessons learned.

---

## 🧩 System Architecture  
The board is organized into clear functional blocks:

| Block | Description |
|-------|-------------|
| **MCU Core** | STM32L432 with SWD, clocking, boot config, and GPIO expansion |
| **RF Module** | nRF24L01+ with matched impedance routing and local decoupling |
| **Sensors** | I²C environmental sensors (BME280 or similar) |
| **Power** | AMS1117‑3.3 LDO, Li‑ion charger, power‑path, USB input |
| **PDN** | Multi‑stage decoupling network with modeled ESR/ESL |
| **Debug** | SWD header, UART breakout, test points |
| **Expansion** | GPIO header for future peripherals |

---

## 🛠️ Altium Designer Workflow  
This project was built using a professional Altium workflow:

### **Schematic Design**
- Hierarchical sheets for MCU, RF, sensors, and power  
- Parameterized components with manufacturer part numbers  
- ERC‑clean schematic with design rules enforced  
- Consistent net naming and signal hierarchy  

### **PCB Layout**
- 4‑layer board
	-L1: Signal, Power, GND pours
	-L2: GND plane
	-L3: Power plane
	-L4: Signal, GND pours 
- RF‑aware routing for nRF24L01+   
- Controlled‑return‑path routing  
- Decoupling capacitors placed with **minimum loop area**  
- USB FS differential pair routing  
- Thermal relief and copper balancing  

### **Outputs Generated**
- Fabrication drawings  
- Assembly drawings  
- Gerbers + drill files  
- 3D STEP model  
- BOM with sourcing information  

---

## 📡 RF Layout Considerations  
The nRF24L01+ section was routed with RF best practices:

- Short, direct supply routing  
- Local high‑frequency decoupling  
- Clean return paths  
- Isolation from noisy digital switching  
- Avoiding stubs and discontinuities  
- Ground stitching vias around RF section  

---

## 🔌 Power System  
The board includes:

- MCP73871 Li‑ion charger IC  
- USB 5 V input  
- AMS1117‑3.3 LDO  
- Power‑good indicators  


---

## 🧪 Bring‑Up & Validation Plan  
A structured bring‑up plan was created:

### **Electrical Bring‑Up**
- Verify 3.3 V rail stability  
- Measure PDN impedance and transient response  
- Validate USB power path  
- Check SWD connectivity  
- Confirm oscillator startup  

### **Firmware Bring‑Up**
- Blink test  
- UART console  
- Sensor enumeration  
- RF link test  
- Power measurement  

### **RF Testing**
- RSSI stability  
- Packet error rate  
- Noise coupling from PDN  

---

## 📚 What I Learned  
This project was a deep dive into real‑world hardware engineering:

### **Altium Designer**
- Hierarchical schematic design  
- Professional PCB layout practices  
- Design rule management  
- Output generation for fabrication  

### **PDN Engineering**
- How MLCCs behave under DC bias  
- Why mixed‑value decoupling is essential  
- How anti‑resonance forms and how to damp it  
- How to model LDO output impedance  
- How to extract inductance vs frequency  
- How to interpret transient droop and ringing  

### **RF & Mixed‑Signal Design**
- Routing strategies for RF modules  
- Managing return paths  
- Minimizing coupling between digital and RF domains  

### **General Hardware Skills**
- Creating testable, debuggable boards  
- Designing for manufacturability  
- Building reproducible simulation workflows  
- Documenting engineering decisions  

---

## 🚀 Future Improvements  
- Add polymer/tantalum bulk capacitor for better damping  
- Move to a 4‑layer stackup for improved PDN and RF performance  
- Add onboard debugger  
- Add solar charging option  
- Improve RF matching network  

---

## 📝 License  
MIT License — feel free to use this design as a reference.

---
