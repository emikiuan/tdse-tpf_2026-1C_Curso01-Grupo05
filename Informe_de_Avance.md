# Informe de Avances - Proyecto Cafetera

**Autores:** Dafne Pellegrino, Ezequiel Mancaniello, Emiliano Kiuan\
**Fecha:** 08/06/2026 \  
**1er cuatrimestre 2026** A continuación se detalla el informe de avances del TPF a partir de los requerimientos:

### Referencia de Estados
| Estado | Descripción |
| :---: | :--- |
| 🟢 | Ya implementado |
| 🟡 | En proceso de implementarse |
| 🔴 | No se implementará |

---

## Interfaz

| Req ID | Descripción | Estado |
| :---: | :--- | :---: |
| 1.1 | El sistema contará con un Menú Interactivo visualizado en una pantalla LCD I2C. | 🟡 |
| 1.2 | La navegación se realizará exclusivamente mediante un Joystick y botones físicos con filtro antirrebote por software. | 🟡 |
| 1.3 | Se utilizarán LEDs para señalizar el proceso de Brewing y un Buzzer para notificaciones sonoras. | 🟡 |

## Operación

| Req ID | Descripción | Estado |
| :---: | :--- | :---: |
| 2.1 | El usuario podrá seleccionar entre opciones como Latte, Mocha o Personalizado. | 🟡 |
| 2.2 | La medición de nivel/stock se realizará mediante un sensor ultrasónico HC-SR04. | 🟡 |
| 2.3 | La temperatura y otras variables analógicas se leerán con ADC gestionado por DMA sin retardos bloqueantes. | 🟡 |

## Modos (FSM)

| Req ID | Descripción | Estado |
| :---: | :--- | :---: |
| 3.1 | El sistema operará en múltiples estados: NORMAL (Menú), FABRICANTE (Set_up) y ERROR (Falla). | 🟡 |
| 3.2 | Existirá un estado SAVE ENERGY que se activará por Timeout para reducir el consumo. | 🟡 |

## Hardware

| Req ID | Descripción | Estado |
| :---: | :--- | :---: |
| 4.1 | El circuito estará íntegramente montado en una placa experimental soldada, sin uso de protoboard ni cables Dupont. | 🟡 |
| 4.2 | Las configuraciones de fabricante (Set_up) se guardarán en una memoria EEPROM. | 🟡 |

## Bluetooth

| Req ID | Descripción | Estado |
| :---: | :--- | :---: |
| 5.1 | El sistema incluirá un módulo HM-10 para conexión Bluetooth. | 🟡 |
| 5.2 | Mediante una App, el administrador podrá acceder al "Estado Fabricante" para ajustar temperatura y stock remotamente. | 🟡 |
