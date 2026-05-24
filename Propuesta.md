<img src="https://www.fi.uba.ar/images/logo-fiuba.png" alt="image2" width="50%">

# **Smart Coffee**

**Autores: Dafne Pellegrino, Ezequiel Mancaniello, Emiliano Kiuan**
**Materia: Taller de Sistemas Embebidos**
**Fecha: 1er cuatrimestre 2026**


---

### **1. Selección del proyecto a implementar**

#### **1.1 Objetivo del proyecto y resultados esperados**
El objetivo de este proyecto es diseñar e implementar un sistema embebido para una máquina de café inteligente (Smart Coffee). El desarrollo se enfoca en crear un Producto Mínimo Viable que cumpla con altos estándares de portabilidad, rapidez, eficiencia y bajo costo. Se busca que la máquina permita seleccionar diversas bebidas (Latte, Mocha, Personalizado) y cuente con conectividad Bluetooth para configuraciones remotas, asegurando un sistema robusto, de bajo consumo y sin retardos bloqueantes.

#### **1.2 Proyectos similares**
Se consideran tres alternativas de diseño que cumplen con el objetivo de preparar café, variando en su arquitectura:

1. **Máquina de café tradicional:** Control analógico o digital simple, sin conectividad ni menús interactivos.
2. **Máquina de café con Sistema Operativo (SO):** Equipo de alta gama con pantalla táctil, procesador robusto y SO completo.
3. **Smart Coffee (Nuestro Proyecto):** Sistema Bare Metal Event-Triggered, con menú interactivo (LCD I2C y Joystick) y configuración Bluetooth (HM-10).

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

#### **1.3 Selección de proyecto**
Considerando la tabla, se elige implementar el sistema **Smart Coffee (MVP)**. Las máquinas tradicionales carecen de la interactividad y la modernidad requerida para el mercado actual, obteniendo baja puntuación en interfaz. Por otro lado, las máquinas con SO son muy costosas, consumen mucha energía y su hardware es complejo de escalar para un entorno educativo/MVP. 

El diseño propuesto con FSM estructurada, periféricos I2C y un modelo Event-Triggered (ETS) ofrece el equilibrio perfecto. Permite mediciones precisas utilizando DMA en el ADC y conversiones matemáticas, al tiempo que se mantiene en un entorno Bare Metal predecible y de bajo consumo. El armado en placa base soldada garantiza robustez profesional frente a cables sueltos.

---

### **2. Elicitación de requisitos y casos de uso**

El mercado de máquinas de café varía desde cafeteras de goteo muy económicas hasta equipos de barista hiper-automatizados. Sin embargo, para entornos de oficina o pequeños comercios, se necesita un punto intermedio: una máquina que ofrezca selección interactiva de productos, diagnóstico de stock, y facilidad de configuración remota, manteniendo un consumo eléctrico mínimo y sin necesidad de grandes sistemas operativos. 

| Grupo | ID | Descripción |
| :---- | :---- | :---- |
| **Interfaz** | 1.1 | El sistema contará con un Menú Interactivo visualizado en una pantalla LCD I2C. |
| | 1.2 | La navegación se realizará exclusivamente mediante un Joystick y botones físicos con filtro antirrebote por software. |
| | 1.3 | Se utilizarán LEDs para señalizar el proceso de Brewing y un Buzzer para notificaciones sonoras. |
| **Operación** | 2.1 | El usuario podrá seleccionar entre opciones como Latte, Mocha o Personalizado. |
| | 2.2 | La medición de nivel/stock se realizará mediante un sensor ultrasónico HC-SR04. |
| | 2.3 | La temperatura y otras variables analógicas se leerán con ADC gestionado por DMA sin retardos bloqueantes. |
| **Modos (FSM)** | 3.1 | El sistema operará en múltiples estados: NORMAL (Menú), FABRICANTE (Set_up) y ERROR (Falla). |
| | 3.2 | Existirá un estado SAVE ENERGY que se activará por Timeout para reducir el consumo. |
| **Hardware** | 4.1 | El circuito estará íntegramente montado en una placa experimental soldada, sin uso de protoboard ni cables Dupont. |
| | 4.2 | Las configuraciones de fabricante (Set_up) se guardarán en una memoria EEPROM. |
| **Bluetooth** | 5.1 | El sistema incluirá un módulo HM-10 para conexión Bluetooth. |
| | 5.2 | Mediante una App, el administrador podrá acceder al "Estado Fabricante" para ajustar temperatura y stock remotamente. |

<p align="center"><em>Tabla 3.1: Requisitos del proyecto</em></p>


| Elemento | Definición |
| :---- | :---- |
| **Disparador** | El usuario desea preparar una bebida desde el menú principal. |
| **Precondiciones** | El sistema está encendido en ESTADO MENU PRINCIPAL. No hay errores de hardware. |
| **Flujo principal** | 1. El usuario interactúa con el Joystick para entrar al ESTADO SELECCION DE CAFE.<br>2. Se selecciona "Latte" y se presiona el botón, generando un evento.<br>3. El sistema transiciona al ESTADO BREWING, activando los LEDs correspondientes.<br>4. Al finalizar, suena el Buzzer y se retorna al menú principal. |
| **Flujos alternativos** | **a.** Si hay inactividad prolongada antes de elegir, se dispara un EVENT_TIMEOUT y la máquina pasa a SAVE ENERGY.<br>**b.** Si falta agua (detectado por HC-SR04), el sistema entra en ESTADO ERROR. |

<p align="center"><em>Tabla 3.2: Caso de uso 1 - El usuario prepara un café</em></p>


| Elemento | Definición |
| :---- | :---- |
| **Disparador** | El administrador necesita calibrar la temperatura y revisar el stock mediante la App. |
| **Precondiciones** | La máquina está en modo espera. El usuario tiene un smartphone vinculado al módulo HM-10. |
| **Flujo principal** | 1. El administrador envía un comando por Bluetooth.<br>2. El sistema entra al ESTADO FABRICANTE (Set_up).<br>3. Navega al subestado de AJUSTE TEMPERATURA y modifica el valor.<br>4. Revisa el estado de AJUSTE STOCK.<br>5. Los nuevos parámetros se guardan en la memoria EEPROM. |
| **Flujos alternativos** | **a.** Si se corta la conexión Bluetooth durante el Set_up, el sistema descarta los cambios no guardados y vuelve al Menú Principal.<br>**b.** Si se envían valores fuera de rango, el sistema emite una alerta con el Buzzer y rechaza el dato. |

<p align="center"><em>Tabla 3.3: Caso de uso 2 - Configuración remota Set_Up vía Bluetooth</em></p>


| Elemento | Definición |
| :---- | :---- |
| **Disparador** | El sistema no detecta interacción por un tiempo definido. |
| **Precondiciones** | El sistema está inactivo en el ESTADO MENU PRINCIPAL. |
| **Flujo principal** | 1. El timer del Super-Loop (basado en el Systick de 1ms) alcanza el límite de inactividad.<br>2. Se genera un EVENT_TIMEOUT.<br>3. La FSM transiciona al estado SAVE ENERGY.<br>4. Se apaga la pantalla LCD y se reduce el consumo de CPU utilizando el modelo de ejecución ETS. |
| **Flujos alternativos** | **a.** El usuario presiona cualquier botón o mueve el joystick. Se genera un evento (ej. EVENT_BOTON_EDGE), el sistema "despierta" y regresa instantáneamente al Menú Principal. |

<p align="center"><em>Tabla 3.4: Caso de uso 3 - Ingreso al modo de bajo consumo</em></p>
