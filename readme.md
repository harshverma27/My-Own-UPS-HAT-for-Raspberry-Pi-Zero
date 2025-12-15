# 🔋 Raspberry Pi Zero 2 UPS (TP4056 + DW01A + TPS61236)

## 📌 Overview

This project is a **budget-friendly UPS (Uninterruptible Power Supply)** designed specifically for the **Raspberry Pi Zero 2**.

I built this because I personally use a **Pi Zero 2**, and I needed a **reliable battery backup (UPS)** for it.
Most ready-made UPS solutions available are either:

* Too expensive
* Overkill for Pi Zero
* Poorly designed or unreliable

So instead of buying one, **I designed my own UPS PCB from scratch**.

This design uses **commonly available and low-cost ICs** while still following **proper battery safety and power design practices**.

---

## 🧩 Project Architecture

The PCB is divided into **three main functional blocks**:

1. **Battery Protection Circuit**
2. **Battery Charging Circuit**
3. **Boost Converter (5V Output for Raspberry Pi)**

Each block is electrically separated but works together as a complete system.

---

## 🔋 1. Battery Protection (DW01A + MOSFETs)

Lithium-ion batteries must **never** be:

* Over-discharged
* Over-charged
* Short-circuited

To ensure safety, this design uses the **DW01A battery protection IC** along with external MOSFETs.

### What this block does:

* Cuts off the load if battery voltage drops too low (low-voltage cutoff)
* Protects against over-current and short-circuit
* Protects the battery during charging and discharging

This ensures the 18650 cell is always operating within safe limits.

---

## 🔌 2. Battery Charging Circuit (TP4056)

Charging is handled by the **TP4056**, a popular and reliable **single-cell Li-ion charger IC**.

### Why TP4056:

* Simple linear charger
* Constant Current / Constant Voltage (CC/CV) charging
* Reliable and widely used
* Easy to configure charging current

### Important design choice:

The **TP4056 is used only for charging**.
It does **not power the load directly**.

The battery is always protected by the **DW01A**, and the charger connects safely through the protection circuit.

---

## ⚡ 3. Boost Converter (TPS61236)

The Raspberry Pi Zero 2 requires a **stable 5V supply**.

Since a single 18650 battery provides **3.0V–4.2V**, a boost converter is required.

This project uses the **TPS61236** boost converter.

### What this block does:

* Boosts battery voltage to a stable **5V**
* Provides enough current for Raspberry Pi Zero 2
* Designed with proper layout considerations for efficiency and stability

The boost converter draws power **only through the protected battery path**, ensuring the battery is never over-discharged.

---

## 🔁 How Everything Works Together

1. **Battery powers the system** through the protection circuit
2. **Boost converter generates 5V** for Raspberry Pi Zero 2
3. **TP4056 charges the battery** when external power is available
4. If external power is removed:

   * Battery instantly takes over
   * Pi continues running without reboot
5. If battery voltage becomes too low:

   * DW01A disconnects the load to protect the battery

This makes the system act like a **true UPS**.

---

## 🎯 Why I Built This Project

* I own a **Raspberry Pi Zero 2**
* I needed a **low-cost, reliable UPS**
* Commercial solutions were expensive or poorly suited
* I wanted:

  * Battery safety
  * Proper power design
  * Full control over the hardware
* This project was also a **learning experience in power electronics and PCB design**

---

## 🛠️ Features

* Li-ion battery support (3.7V)
* Battery protection (LVC, OCP, SCP)
* Safe and reliable charging
* 5V regulated output for Raspberry Pi Zero 2
* Budget-friendly and open-source
* Designed as a **PCB**, not a breadboard hack

---

## 📂 Repository Contents

* `Kicad Projtect/` – Full Kicad Projtect
* `gerbers/` – Manufacturing-ready files
* `README.md` – Project documentation

---

## ⚠️ Disclaimer

This project involves **lithium-ion batteries**.
Improper handling or incorrect assembly can cause damage or injury.

Build and use at your own risk.
Always verify connections before inserting a battery.

---

## ⭐ Future Improvements

* Battery percentage monitoring
* Load current measurement
* Power-fail detection GPIO for Raspberry Pi
* Multiple-cell support
