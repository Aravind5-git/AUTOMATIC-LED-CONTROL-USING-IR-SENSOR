# AUTOMATIC-LED-CONTROL-USING-IR-SENSOR
##  AIM
To design and implement a system using the **STM32 microcontroller** where an LED automatically turns ON or OFF based on the input from an **IR sensor**.

---

##  Components Required
- STM32 Nucleo or Discovery Board (e.g., **Nucleo-G071RB**)
- IR Sensor Module
- LED (5mm Green or any color)
- Jumper wires
- Breadboard

---

##  Theory
An **IR sensor** detects the presence of an object by emitting and receiving infrared light.

### IR Sensor Behavior
- When an **object is detected**, the IR sensor output goes **LOW (0V)**.
- When **no object is detected**, the output stays **HIGH (3.3V)**.

### Microcontroller Response
- If **IR output = LOW** → **LED ON**
- If **IR output = HIGH** → **LED OFF**
### **Procedure**

1. Open **STM32CubeIDE**.
<img width="1919" height="1145" alt="Screenshot 2025-11-11 001543" src="https://github.com/user-attachments/assets/bddf8300-e19c-4c0e-9f02-ac144d170fd5" />

2. Click **File → New STM32 Project**.
<img width="1919" height="1140" alt="Screenshot 2025-11-11 001724" src="https://github.com/user-attachments/assets/517bbeb6-334b-448f-9db9-a80636a0f1cd" />

3. Select the **target microcontroller** or board and click **Next**.
<img width="1919" height="1142" alt="Screenshot 2025-11-11 001903" src="https://github.com/user-attachments/assets/f5d5e158-dc0b-4e50-b7f5-ba7fa1057730" />



4. Name the project.
![WhatsApp Image 2025-11-10 at 20 11 50_c4ca29c9](https://github.com/user-attachments/assets/a4f09cfa-16b7-49c9-9dd0-081f0f15bd9f)

5. The corresponding `.ioc` file will be generated automatically.
![WhatsApp Image 2025-11-10 at 20 11 50_48336e74](https://github.com/user-attachments/assets/a16ab8fb-6fb0-4262-9a57-c8d734678666)

6. Configure the pins as **GPIO (Input/Output)**, **USART**, etc. as needed.
![WhatsApp Image 2025-11-10 at 20 11 50_984e8dfe](https://github.com/user-attachments/assets/3165f71f-338d-44c7-9099-2247f25f483b)

7. Save the configuration (`Ctrl + S`) – the base C program will be generated automatically.
   <img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/dbf4b205-5db9-4e9b-8150-94f441c8b116" />
 
8. Edit the generated main program as required.
![WhatsApp Image 2025-11-10 at 20 12 02_2f176e18](https://github.com/user-attachments/assets/eed9767d-c680-44db-9deb-e4d8dbfbc6e2)

9. Click **Project → Build All**.
![WhatsApp Image 2025-11-10 at 20 12 02_2f176e18](https://github.com/user-attachments/assets/eed9767d-c680-44db-9deb-e4d8dbfbc6e2)

10. Link the **HEX file** using the post-build process.
![WhatsApp Image 2025-11-10 at 20 11 59_e0b377df](https://github.com/user-attachments/assets/0e48c780-74a8-4c6d-895e-ff5ff156c54b)

11. Click **Debug** and connect the **STM Nucleo Board**.
![WhatsApp Image 2025-11-10 at 20 11 57_16574c4a](https://github.com/user-attachments/assets/ec9662a4-3ed8-49fe-9673-75647dbea886)

13. Click **Run** to execute the program.
    
---

### 💻 **Program**


```c
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
    HAL_Init();
    SystemClock_Config();
    MX_GPIO_Init();

    while (1)
    {
        GPIO_PinState ir = HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_10); // IR OUT at PA10 (D2)

	      if (ir == GPIO_PIN_RESET)  // IR sensor HIGH = object detected
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_SET); // Turn ON LED
	      }
	      else
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_RESET); // Turn OFF LED
	      }

	      HAL_Delay(100);
    }
}
```
---
### OUTPUT
CASE 1: LED ON 
![WhatsApp Image 2025-11-10 at 20 15 31_42dcf03c](https://github.com/user-attachments/assets/a0ad5ed4-d236-4d2e-a5e2-23d10b199389)

CASE 2: LED OFF
![WhatsApp Image 2025-11-10 at 20 15 32_fe1ff9aa](https://github.com/user-attachments/assets/8d87dead-c630-438b-862e-f3b3b0934bbb)

---
### RESULT

The experiment on IR Sensor-Based Automatic LED Control using STM32 was successfully carried out. The STM32 microcontroller accurately read the IR sensor output and controlled the LED based on object detection. When an object was detected, the LED glowed (ON) and when no object was present, the LED remained OFF. Thus, the objective of the experiment was achieved.




