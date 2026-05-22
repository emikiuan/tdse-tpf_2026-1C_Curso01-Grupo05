<img src="https://www.fi.uba.ar/images/logo-fiuba.png" alt="image2" width="50%">

# **Smart Coffee**

**Autores: Dafne Pellegrino, Ezequiel Mancaniello, Emiliano Kiuan**
**Materia: Taller de Sistemas Embebidos**
**Fecha: 1er cuatrimestre 2026**

---

### **1. Requisitos Particulares de la Entrega**

Para cumplir con la implementación del Producto Mínimo Viable (prototipo), el proyecto incorpora los siguientes elementos:

**Hardware obligatorio:**
* [cite_start]Dip Switchs, Buttons [cite: 202][cite_start], Leds[cite: 203], Buzzer, módulo HM-10 (para usar App vía Bluetooth).
* [cite_start]Memoria E2PROM externa o Flash interna (para almacenamiento del SET_UP y configuraciones)[cite: 204].
* [cite_start]Sensores analógicos: Potenciómetro de 20K [cite: 205] [cite_start]y Joystick[cite: 201].
* [cite_start]Para la interconexión de componentes, **no se utilizará protoboard ni cables Dupont**; se implementará una placa base experimental con componentes y conectores soldados e interconexión mediante cables soldados[cite: 216].

**Hardware adicional:**
* [cite_start]Pantalla LCD I2C para interfaz gráfica[cite: 206].
* [cite_start]Sensor ultrasónico HC-SR04 para medición de niveles[cite: 207].

**Programación obligatorio:**
* [cite_start]Sistema Bare Metal (sin Sistema Operativo), basado en un modelo Event-Triggered System (ETS) que reduce el consumo[cite: 273].
* [cite_start]Arquitectura Estructurada/Modular (Escrutar/Procesar/Actuar) evitando el código bloqueante[cite: 258, 259].
* Ejecutor cíclico Super-Loop con un Tick de 1mS (Systick => Callback).
* [cite_start]Tareas de código no bloqueante y diseño estructurado mediante Máquina de Estados Finitos (FSM)[cite: 271].
* Menú Interactivo navegado mediante Joystick.
* [cite_start]Gestión de Bajo Consumo (estado SAVE ENERGY)[cite: 196].
* [cite_start]Múltiples modos de operación: NORMAL (Menú Principal), SET_UP (Estado Fabricante) y FALLA (Estado Error)[cite: 173, 180, 197].
* [cite_start]Periféricos I2C [cite: 206] [cite_start]y uso de DMA en ADC para lectura de sensores[cite: 253].

---

### **2. Selección del proyecto a implementar**

#### **2.1 Objetivo del proyecto y resultados esperados**
[cite_start]El objetivo de este proyecto es diseñar e implementar un sistema embebido para una máquina de café inteligente (Smart Coffee)[cite: 153, 154]. [cite_start]El desarrollo se enfoca en crear un Producto Mínimo Viable [cite: 159] [cite_start]que cumpla con altos estándares de portabilidad, rapidez, eficiencia y bajo costo[cite: 265, 266, 267, 268]. [cite_start]Se busca que la máquina permita seleccionar diversas bebidas (Latte, Mocha, Personalizado) [cite: 163, 164, 171] [cite_start]y cuente con conectividad Bluetooth para configuraciones remotas, asegurando un sistema robusto, de bajo consumo [cite: 273] [cite_start]y sin retardos bloqueantes[cite: 258, 259].

#### **2.2 Proyectos similares**
Se consideran tres alternativas de diseño que cumplen con el objetivo de preparar café, variando en su arquitectura:

1. **Máquina de café tradicional:** Control analógico o digital simple, sin conectividad ni menús interactivos.
2. **Máquina de café con Sistema Operativo (SO):** Equipo de alta gama con pantalla táctil, procesador robusto y SO completo.
3. [cite_start]**Smart Coffee (Nuestro Proyecto):** Sistema Bare Metal Event-Triggered [cite: 273][cite_start], con menú interactivo (LCD I2C [cite: 206] [cite_start]y Joystick [cite: 201]) y configuración Bluetooth (HM-10).

Para comparar estas alternativas, se ponderan los aspectos del 1 al 10: Disponibilidad de hardware (10), Eficiencia de recursos y energía (9), Complejidad de software (8), Costo (7), Interfaz de usuario (8) e Interés personal (8).

<table>
        <thead>
            <tr>
                <th rowspan="2">Proyecto</th>
                <th colspan="2">Tradicional</th>
                <th colspan="2">Smart Coffee (MVP)</th>
                <th colspan="2">Máquina con SO</th>
            </tr>
            <tr>
                <th>Puntaje</th>
                <th>Ponderado</th>
                <th>Puntaje</th>
                <th>Ponderado</th>
                <th>Puntaje</th>
                <th>Ponderado</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td align ="center">Disp. de Hardware (10)</td>
                <td>10</td>
                <td>100</td>
                <td>10</td>
                <td>100</td>
                <td>4</td>
                <td>40</td>
            </tr>
            <tr>
                <td align ="center">Eficiencia y Energía (9)</td>
                <td>8</td>
                <td>72</td>
                <td>10</td>
                <td>90</td>
                <td>4</td>
                <td>36</td>
            </tr>
            <tr>
                <td align ="center">Complejidad Software (8)</td>
                <td>10</td>
                <td>80</td>
                <td>8</td>
                <td>64</td>
                <td>2</td>
                <td>16</td>
            </tr>
            <tr>
                <td align ="center">Costo (7)</td>
                <td>9</td>
                <td>63</td>
                <td>8</td>
                <td>56</td>
                <td>3</td>
                <td>21</td>
            </tr>
            <tr>
                <td align ="center">Interfaz Usuario (8)</td>
                <td>3</td>
                <td>24</td>
                <td>9</td>
                <td>72</td>
                <td>10</td>
                <td>80</td>
            </tr>
            <tr>
                <td align ="center">Interés personal (8)</td>
                <td>2</td>
                <td>16</td>
                <td>10</td>
                <td>80</td>
                <td>8</td>
                <td>64</td>
            </tr>
            <tr>
                <td><strong>Puntaje Total</strong></td>
                <td>-</td>
                <td>355</td>
                <td>-</td>
                <td><strong>462</strong></td>
                <td>-</td>
                <td>257</td>
            </tr>
        </tbody>
</table>
<p align="center"><em>Tabla 2.2.1: Comparación de proyectos</em></p>

#### **2.3 Selección de proyecto**
Considerando la tabla, se elige implementar el sistema **Smart Coffee (MVP)**. Las máquinas tradicionales carecen de la interactividad y la modernidad requerida para el mercado actual, obteniendo baja puntuación en interfaz. Por otro lado, las máquinas con SO son muy costosas, consumen mucha energía y su hardware es complejo de escalar para un entorno educativo/MVP. 

[cite_start]El diseño propuesto con FSM estructurada [cite: 271][cite_start], periféricos I2C [cite: 206] [cite_start]y un modelo Event-Triggered (ETS) [cite: 273] ofrece el equilibrio perfecto. [cite_start]Permite mediciones precisas utilizando DMA en el ADC [cite: 253] [cite_start]y conversiones matemáticas [cite: 256, 257][cite_start], al tiempo que se mantiene en un entorno Bare Metal predecible y de bajo consumo[cite: 273]. [cite_start]El armado en placa base soldada garantiza robustez profesional frente a cables sueltos[cite: 216].

###### **2.3.1 Diagrama en bloques (FSM)**
[cite_start]El sistema se rige por un diagrama de estados que incluye el ESTADO MENU PRINCIPAL [cite: 173][cite_start], ESTADO SELECCION DE CAFE [cite: 167][cite_start], ESTADO BREWING [cite: 165][cite_start], ESTADO FABRICANTE (Set_Up) [cite: 180] [cite_start]y modos de energía como SAVE ENERGY y OFF[cite: 177, 196].

---

### **3. Elicitación de requisitos y casos de uso**

El mercado de máquinas de café varía desde cafeteras de goteo muy económicas hasta equipos de barista hiper-automatizados. Sin embargo, para entornos de oficina o pequeños comercios, se necesita un punto intermedio: una máquina que ofrezca selección interactiva de productos, diagnóstico de stock, y facilidad de configuración remota, manteniendo un consumo eléctrico mínimo y sin necesidad de grandes sistemas operativos. 

| Grupo | ID | Descripción |
| :---- | :---- | :---- |
| **Interfaz** | 1.1 | [cite_start]El sistema contará con un Menú Interactivo visualizado en una pantalla LCD I2C[cite: 206]. |
| | 1.2 | [cite_start]La navegación se realizará exclusivamente mediante un Joystick [cite: 201] [cite_start]y botones físicos con filtro antirrebote por software[cite: 202, 255]. |
| | 1.3 | [cite_start]Se utilizarán LEDs para señalizar el proceso de Brewing y un Buzzer para notificaciones sonoras[cite: 165, 203]. |
| **Operación** | 2.1 | [cite_start]El usuario podrá seleccionar entre opciones como Latte [cite: 163][cite_start], Mocha [cite: 164] [cite_start]o Personalizado[cite: 171]. |
| | 2.2 | [cite_start]La medición de nivel/stock se realizará mediante un sensor ultrasónico HC-SR04[cite: 207]. |
| | 2.3 | [cite_start]La temperatura y otras variables analógicas se leerán con ADC gestionado por DMA sin retardos bloqueantes[cite: 253, 258]. |
| **Modos (FSM)** | 3.1 | [cite_start]El sistema operará en múltiples estados: NORMAL (Menú), FABRICANTE (Set_up) y ERROR (Falla)[cite: 173, 180, 197]. |
| | 3.2 | [cite_start]Existirá un estado SAVE ENERGY que se activará por Timeout para reducir el consumo[cite: 174, 196]. |
| **Hardware** | 4.1 | [cite_start]El circuito estará íntegramente montado en una placa experimental soldada, sin uso de protoboard ni cables Dupont[cite: 216]. |
| | 4.2 | [cite_start]Las configuraciones de fabricante (Set_up) se guardarán en una memoria EEPROM[cite: 204]. |
| **Bluetooth** | 5.1 | El sistema incluirá un módulo HM-10 para conexión Bluetooth. |
| | 5.2 | [cite_start]Mediante una App, el administrador podrá acceder al "Estado Fabricante" para ajustar temperatura y stock remotamente[cite: 180, 183, 189]. |

<p align="center"><em>Tabla 3.1: Requisitos del proyecto</em></p>


| Elemento | Definición |
| :---- | :---- |
| **Disparador** | El usuario desea preparar una bebida desde el menú principal. |
| **Precondiciones** | [cite_start]El sistema está encendido en ESTADO MENU PRINCIPAL[cite: 173]. No hay errores de hardware. |
| **Flujo principal** | 1. [cite_start]El usuario interactúa con el Joystick [cite: 201] [cite_start]para entrar al ESTADO SELECCION DE CAFE[cite: 167].<br>2. Se selecciona "Latte" y se presiona el botón, generando un evento.<br>3. [cite_start]El sistema transiciona al ESTADO BREWING [cite: 165][cite_start], activando los LEDs correspondientes[cite: 163, 203].<br>4. Al finalizar, suena el Buzzer y se retorna al menú principal. |
| **Flujos alternativos** | [cite_start]**a.** Si hay inactividad prolongada antes de elegir, se dispara un EVENT_TIMEOUT [cite: 175] [cite_start]y la máquina pasa a SAVE ENERGY [cite: 196][cite_start].<br>**b.** Si falta agua (detectado por HC-SR04 [cite: 207][cite_start]), el sistema entra en ESTADO ERROR[cite: 197]. |

<p align="center"><em>Tabla 3.2: Caso de uso 1 - El usuario prepara un café</em></p>


| Elemento | Definición |
| :---- | :---- |
| **Disparador** | El administrador necesita calibrar la temperatura y revisar el stock mediante la App. |
| **Precondiciones** | La máquina está en modo espera. El usuario tiene un smartphone vinculado al módulo HM-10. |
| **Flujo principal** | 1. El administrador envía un comando por Bluetooth.<br>2. [cite_start]El sistema entra al ESTADO FABRICANTE (Set_up)[cite: 180].<br>3. [cite_start]Navega al subestado de AJUSTE TEMPERATURA [cite: 183] y modifica el valor.<br>4. [cite_start]Revisa el estado de AJUSTE STOCK[cite: 189].<br>5. [cite_start]Los nuevos parámetros se guardan en la memoria EEPROM[cite: 204]. |
| **Flujos alternativos** | **a.** Si se corta la conexión Bluetooth durante el Set_up, el sistema descarta los cambios no guardados y vuelve al Menú Principal.<br>**b.** Si se envían valores fuera de rango, el sistema emite una alerta con el Buzzer y rechaza el dato. |

<p align="center"><em>Tabla 3.3: Caso de uso 2 - Configuración remota Set_Up vía Bluetooth</em></p>


| Elemento | Definición |
| :---- | :---- |
| **Disparador** | El sistema no detecta interacción por un tiempo definido. |
| **Precondiciones** | [cite_start]El sistema está inactivo en el ESTADO MENU PRINCIPAL[cite: 173]. |
| **Flujo principal** | 1. El timer del Super-Loop (basado en el Systick de 1ms) alcanza el límite de inactividad.<br>2. [cite_start]Se genera un EVENT_TIMEOUT[cite: 174].<br>3. [cite_start]La FSM transiciona al estado SAVE ENERGY[cite: 196].<br>4. [cite_start]Se apaga la pantalla LCD [cite: 206] [cite_start]y se reduce el consumo de CPU [cite: 261] [cite_start]utilizando el modelo de ejecución ETS[cite: 273]. |
| **Flujos alternativos** | [cite_start]**a.** El usuario presiona cualquier botón [cite: 202] [cite_start]o mueve el joystick[cite: 201]. [cite_start]Se genera un evento (ej. EVENT_BOTON_EDGE [cite: 176]), el sistema "despierta" y regresa instantáneamente al Menú Principal. |

<p align="center"><em>Tabla 3.4: Caso de uso 3 - Ingreso al modo de bajo consumo</em></p>
