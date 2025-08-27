# PID Temperature Control Simulation

This is a simple simulation of a PID (Proportional-Integral-Derivative) temperature controller that I built using the Wokwi online simulator. Since I didn’t have real hardware for this project, I used a slide potentiometer to act as a mock temperature sensor and an LED as a heater. The system runs a PID loop that tries to keep the "temperature" close to a setpoint of 25°C.  

The OLED display shows the current temperature, the setpoint, and the PWM output in real time.  

---

## Project Setup

### Components
- Arduino Uno  
- Slide Potentiometer (mock temperature input)  
- Red LED (acts as heater)  
- SSD1306 OLED Display (I2C)  
- Jumper Wires  

### Circuit Connections
Potentiometer  
- Left pin → GND  
- Middle pin → A0  
- Right pin → 5V  

LED (Heater)  
- Anode → Pin 9  
- Cathode → GND  

OLED (SSD1306, I2C)  
- VCC → 5V  
- GND → GND  
- SDA → A4  
- SCL → A5  

---

## How It Works

- The potentiometer gives an analog value that I map to a temperature range of 0°C to 50°C.  
- The Arduino calculates the PID output based on the error between this value and the setpoint (25°C).  
- The PID output controls the LED brightness using PWM. Bright LED means the system is "heating" more.  
- The OLED updates every 200ms with live temperature, setpoint, and output values.  

---

## PID Algorithm

The PID formula is:  output = Kp * error + Ki * integral + Kd * derivative


- error = setPoint - currentTemp  
- integral += error  
- derivative = error - previousError  

The output is constrained to 0–255 so it fits the PWM range.  

The values I found stable in simulation were:  
- Kp = 2.0  
- Ki = 0.5  
- Kd = 1.0  

---

## Testing

- At low temperatures (potentiometer at minimum), the LED is fully bright.  
- As the temperature gets close to the setpoint, the LED brightness gradually drops.  
- At high temperatures (potentiometer maxed), the LED is almost off.  
- The system doesn’t just switch abruptly; it reacts smoothly because of the PID tuning.  

---

## What’s Included

- Folder `Code` contains the Arduino Embedded C code I used in Wokwi.  
- Folder `Videos` has screen recordings of the simulation running.  
- A direct link to the Wokwi simulation is here:  
  [Wokwi Project Link](https://wokwi.com/projects/434551894932194305)  

---

## Conclusion

This project was a fun way to practice implementing a PID controller without needing physical components. Using Wokwi, I could visualize how the PID reacts to changes in temperature and fine-tune the parameters until it felt realistic.  

