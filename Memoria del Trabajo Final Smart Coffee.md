# Memoria del Trabajo Final: Smart Coffee

**Universidad de Buenos Aires**  
**Facultad de Ingeniería**  
**Taller de Sistemas Embebidos (TA134)**  

**Autores:** Dafne Pellegrino, Ezequiel Mancaniello, Emiliano Kiuan  
**Legajos:** *[Completar]*  
**Lugar y Fecha:** Ciudad Autónoma de Buenos Aires, entre marzo y julio de 2026.  

---

## RESUMEN

En el presente trabajo se desarrolló un sistema embebido para una máquina de café inteligente (Smart Coffee) en su etapa de Producto Mínimo Viable (MVP). El sistema fue diseñado bajo una arquitectura de bajo costo, alta eficiencia energética y procesamiento en tiempo real sin retardos bloqueantes, montado sobre una placa base soldada para garantizar robustez a nivel profesional.

El firmware se implementó bajo un entorno Bare Metal utilizando un modelo conducido por eventos (Event-Triggered System - ETS). El control principal del sistema se gestiona mediante una máquina de estados finitos (FSM) estructurada, la cual se encarga de la lógica para la selección de diversas bebidas (Latte, Mocha y Personalizado). Para lograr mediciones precisas de los sensores sin afectar el rendimiento global, se configuró el módulo ADC trabajando en conjunto con el controlador DMA para la adquisición de datos y posterior conversión matemática. La comunicación con los periféricos del sistema se realiza a través del bus I2C.

El sistema cuenta con conectividad inalámbrica mediante un módulo Bluetooth, permitiendo la interacción remota para configuraciones del equipo desde dispositivos externos, ofreciendo una alternativa moderna, interactiva y escalable frente a las máquinas tradicionales o los costosos sistemas basados en sistemas operativos complejos.

---

## Índice General

* **Registro de versiones** | 4
* **CAPÍTULO 1: Introducción general** | 5
  * 1.1 Objetivo del trabajo | 5
  * 1.2 Motivaciones para realizar el trabajo y la selección de proyecto | 5
  * 1.3 Funcionamiento general del sistema | 6
  * 1.4 Desarrollo de las funcionalidades del microcontrolador | 7
* **CAPÍTULO 2: Introducción específica** | 8
  * 2.1 Requisitos | 8
  * 2.2 Casos de uso | 10
  * 2.3 Descripción de componentes y módulos principales | 12
* **CAPÍTULO 3: Diseño e implementación** | 14
  * 3.1 Hardware del Sistema de Control de Cafetera | 14
  * 3.2 Firmware del Sistema de Control de Cafetera | 15
* **CAPÍTULO 4: Ensayos y resultados** | 20
  * 4.1 Pruebas funcionales del hardware | 20
  * 4.2 Pruebas funcionales del firmware | 20
  * 4.3 Pruebas de integración | 20
  * 4.4 Cumplimiento de requisitos | 21
  * 4.5 Comparación con otros sistemas similares | 21
  * 4.6 Documentación del desarrollo realizado | 21
* **CAPÍTULO 5: Conclusiones** | 22
  * 5.1 Resultados obtenidos | 22
  * 5.2 Próximos pasos | 22
* **Bibliografía** | 23
* **Anexos** | 24
  * A. Primer Anexo | 24

---

## Registro de versiones

| Revisión | Cambios realizados | Fecha |
| :--- | :--- | :--- |
| **1.0** | Creación del documento | 01/07/2026 |
| **1.1** | *[Completar]* | *[Completar]* |
| **1.2** | *[Completar]* | *[Completar]* |

---

## CAPÍTULO 1: Introducción general

### 1.1 Objetivo del trabajo
El objetivo de este trabajo fue diseñar e implementar un sistema embebido para una máquina de café inteligente (Smart Coffee) en su etapa de Producto Mínimo Viable (MVP). El desarrollo se enfocó en crear una plataforma que cumpla con altos estándares de portabilidad, rapidez, eficiencia y bajo costo. 

Se buscó que la máquina permita al usuario seleccionar diversas bebidas, tales como Latte, Mocha o una configuración personalizada, y que cuente con conectividad inalámbrica para realizar configuraciones de forma remota. A través de este diseño, se persiguió la obtención de un sistema robusto, de bajo consumo energético y libre de retardos bloqueantes.

### 1.2 Motivaciones para realizar el trabajo y la selección de proyecto
Las máquinas de café tradicionales que se encuentran habitualmente en el mercado carecen de la interactividad y la modernidad requeridas por los usuarios actuales, obteniendo un desempeño deficiente en lo que respecta a la interfaz de usuario. Por otra parte, aquellas soluciones comerciales que incorporan un SO (Operating System, Sistema Operativo) complejo resultan costosas, exhiben un elevado consumo de energía y poseen una arquitectura de hardware cuya escalabilidad es compleja para un entorno educativo o de desarrollo inicial.

La decisión de implementar el sistema Smart Coffee se fundamentó en la búsqueda de un equilibrio óptimo entre interactividad, costo y eficiencia. El diseño propuesto se destaca especialmente por incorporar una FSM (Finite State Machine, Máquina de Estados Finitos) estructurada junto con un modelo Event-Triggered (ETS, Sistema Conducido por Eventos) en un entorno Bare Metal predecible y de bajo consumo. Esto diferencia al proyecto de otros sistemas similares en que permite realizar mediciones precisas utilizando Advanced Data Conversion a través del módulo ADC (Analog-to-Digital Converter, Conversor Analógico Digital) gestionado por acceso directo a memoria mediante DMA (Direct Memory Access), optimizando las conversiones matemáticas sin penalizar el rendimiento del procesador.

### 1.3 Funcionamiento general del sistema
*[Nota: Completar con la descripción del flujo general que sigue el hardware y software en conjunto desde el encendido]*

### 1.4 Desarrollo de las funcionalidades del microcontrolador
Para llevar adelante el trabajo, la lógica de control principal del firmware fue estructurada en base a la máquina de estados mencionada en la Sección 1.2. El sistema transita de forma predecible entre los procesos de espera, configuración y dispensado de las distintas recetas de café.

Por el lado de la conectividad y la gestión remota, el sistema se comunicó con un módulo comercial inalámbrico compatible con el protocolo Bluetooth. Este módulo se encargó de intercambiar datos de configuración y comandos con el microcontrolador central a través de una interfaz de comunicación serie UART (Universal Asynchronous Receiver-Transmitter). Mediante esta vía, el firmware es capaz de procesar las solicitudes de bebidas enviadas de forma remota desde una aplicación externa, actualizando los parámetros de las recetas en el almacenamiento local del sistema embebido antes de proceder al ciclo de servido.

---

## CAPÍTULO 2: Introducción específica

### 2.1 Requisitos
El mercado de máquinas de café varía desde cafeteras de goteo muy económicas hasta equipos de barista hiper-automatizados. Sin embargo, para entornos de oficina o pequeños comercios, se necesita un punto intermedio: una máquina que ofrezca selección interactiva de productos, diagnóstico de stock, y facilidad de configuración remota, manteniendo un consumo eléctrico mínimo y sin necesidad de grandes sistemas operativos.

**Tabla 3.1: Requisitos del proyecto**

| Grupo | ID | Descripción |
| :--- | :--- | :--- |
| **Interfaz** | 1.1 | El sistema contará con un Menú Interactivo visualizado en una pantalla LCD I2C. |
| | 1.2 | La navegación se realizará exclusivamente mediante un Joystick y botones físicos con filtro antirrebote por software. |
| | 1.3 | Se utilizarán LEDs para señalizar el proceso de Brewing y un Buzzer para notificaciones sonoras. |
| **Operación** | 2.1 | El usuario podrá seleccionar entre opciones como Latte, Mocha o Personalizado. |
| | 2.2 | La medición de nivel/stock se realizará mediante un sensor ultrasónico HC-SR04. |
| | 2.3 | La temperatura y otras variables analógicas se leerán con ADC gestionado por DMA sin retardos bloqueantes. |
| **Modos (FSM)**| 3.1 | El sistema operará en múltiples estados: NORMAL (Menú), FABRICANTE (Set_up) y ERROR (Falla). |
| | 3.2 | Existirá un estado SAVE ENERGY que se activará por Timeout para reducir el consumo. |
| **Hardware** | 4.1 | El circuito estará íntegramente montado en una placa experimental soldada, sin uso de protoboard ni cables Dupont. |
| | 4.2 | Las configuraciones de fabricante (Set_up) se guardarán en una memoria EEPROM. |
| **Bluetooth** | 5.1 | El sistema incluirá un módulo HM-10 para conexión Bluetooth. |
| | 5.2 | Mediante una App, el administrador podrá acceder al "Estado Fabricante" para ajustar temperatura y stock remotamente. |

### 2.2 Casos de uso

**Tabla 3.2: Caso de uso 1 - El usuario prepara un café**

| Elemento | Definición |
| :--- | :--- |
| **Disparador** | El usuario desea preparar una bebida desde el menú principal. |
| **Precondiciones** | El sistema está encendido en ESTADO MENU PRINCIPAL. No hay errores de hardware. |
| **Flujo principal** | 1. El usuario interactúa con el Joystick para entrar al ESTADO SELECCION DE CAFE.<br>2. Se selecciona "Latte" y se presiona el botón, generando un evento.<br>3. El sistema transiciona al ESTADO BREWING, activando los LEDs correspondientes.<br>4. Al finalizar, suena el Buzzer y se retorna al menú principal. |
| **Flujos alternativos**| a. Si hay inactividad prolongada antes de elegir, se dispara un EVENT_TIMEOUT y la máquina pasa a SAVE ENERGY.<br>b. Si falta agua (detectado por HC-SR04), el sistema entra en ESTADO ERROR. |

**Tabla 3.3: Caso de uso 2 - Configuración remota Set_Up vía Bluetooth**

| Elemento | Definición |
| :--- | :--- |
| **Disparador** | El administrador necesita calibrar la temperatura y revisar el stock mediante la App. |
| **Precondiciones** | La máquina está en modo espera. El usuario tiene un smartphone vinculado al módulo HM-10. |
| **Flujo principal** | 1. El administrador envía un comando por Bluetooth.<br>2. El sistema entra al ESTADO FABRICANTE (Set_up).<br>3. Navega al subestado de AJUSTE TEMPERATURA y modifica el valor.<br>4. Revisa el estado de AJUSTE STOCK.<br>5. Los nuevos parámetros se guardan en la memoria EEPROM. |
| **Flujos alternativos**| a. Si se corta la conexión Bluetooth durante el Set_up, el sistema descarta los cambios no guardados y vuelve al Menú Principal.<br>b. Si se envían valores fuera de rango, el sistema emite una alerta con el Buzzer y rechaza el dato. |

**Tabla 3.4: Caso de uso 3 - Ingreso al modo de bajo consumo**

| Elemento | Definición |
| :--- | :--- |
| **Disparador** | El sistema no detecta interacción por un tiempo definido. |
| **Precondiciones** | El sistema está inactivo en el ESTADO MENU PRINCIPAL. |
| **Flujo principal** | 1. El timer del Super-Loop (basado en el Systick de 1ms) alcanza el límite de inactividad.<br>2. Se genera un EVENT_TIMEOUT.<br>3. La FSM transiciona al estado SAVE ENERGY.<br>4. Se apaga la pantalla LCD y se reduce el consumo de CPU utilizando el modelo de ejecución ETS. |
| **Flujos alternativos**| a. El usuario presiona cualquier botón o mueve el joystick. Se genera un evento (ej. EVENT_BOTON_EDGE), el sistema "despierta" y regresa instantáneamente al Menú Principal. |

### 2.3 Descripción de componentes y módulos principales
En las siguientes subsecciones se detallan los módulos de hardware, componentes de terceros y protocolos utilizados en el sistema que resultan necesarios para comprender las decisiones de diseño adoptadas, pero que no fueron diseñados desde cero en el marco de este trabajo.

#### 2.3.1 Microcontrolador STM32F103RBT6 (Placa Nucleo-64)
Para el núcleo de procesamiento central del sistema, se utilizó la placa de desarrollo Nucleo-64 equipada con el microcontrolador STM32F103RBT6. Este dispositivo actúa como el cerebro central del sistema. Su elección se basó en su capacidad para ejecutar el firmware bajo un entorno Bare Metal conducido por eventos (ETS). Además, cuenta con periféricos clave como conversores ADC con soporte para DMA (Direct Memory Access), temporizadores avanzados para PWM y captura (Input Capture), lo que permite operaciones en tiempo real sin retardos bloqueantes.

#### 2.3.2 Módulo Bluetooth HM-10
Para dotar al sistema de conectividad inalámbrica y permitir su configuración de forma remota, se empleó el módulo comercial HM-10. Este módulo intercambia datos de configuración y comandos con el microcontrolador a través de una interfaz de comunicación serie UART. La decisión de incorporarlo se fundamentó en la necesidad de que un administrador pueda acceder al "Estado Fabricante" (Set_up) mediante una aplicación móvil (App) para calibrar la temperatura y revisar el stock remotamente.

#### 2.3.3 Sensor ultrasónico HC-SR04
Para la medición del nivel y stock de agua en la máquina, se seleccionó el sensor ultrasónico HC-SR04. Este sensor opera con una tensión nativa de 5V, por lo que fue interconectado a pines tolerantes a 5V (FT) del microcontrolador utilizando divisores de tensión. Su lectura se realiza mediante los pines Echo y Trigger enlazados a un temporizador de captura nativo, permitiendo medir los pulsos por hardware sin interrumpir el lazo principal.

#### 2.3.4 Display LCD 16x2 y expansor I2C PCF8574
El sistema cuenta con un menú interactivo visualizado en una pantalla LCD de 16x2 caracteres. Dado que los microcontroladores cuentan con pines limitados y existía una gran concurrencia de tareas, se optó por no utilizar una conexión paralela y comandar el display a través de un expansor de bus I2C (PCF8574). Esta elección de diseño permitió acoplar el display al bus compartido I2C1, reduciendo drásticamente la complejidad del cableado y ahorrando pines GPIO.

#### 2.3.5 Memoria EEPROM 24C02
Para lograr un almacenamiento no volátil de los parámetros del equipo, se incorporó una memoria EEPROM 24C02. En este componente se guardan las configuraciones establecidas por el administrador (como el ajuste de temperatura, niveles de stock y tiempo del actuador del molino). Al igual que el expansor del display, este integrado se comunica con el microcontrolador de forma bidireccional mediante el bus de datos compartido I2C1.

#### 2.3.6 Protocolo I2C (Inter-Integrated Circuit)
Para asegurar la robustez profesional del prototipo y facilitar la interconexión con múltiples periféricos locales, se adoptó el bus industrial I2C. Este protocolo permitió la comunicación concurrente con el expansor de la pantalla LCD y la memoria EEPROM utilizando únicamente dos pines compartidos (SCL y SDA).

---

## CAPÍTULO 3: Diseño e implementación

### 3.1 Hardware del Sistema de Control de Cafetera
El diseño de hardware del sistema se estructuró buscando un equilibrio entre la reutilización de recursos internos del microcontrolador STM32F103RBT6 (placa Nucleo-64) y la inmunidad al ruido eléctrico generado por los actuadores de potencia de la cafetera (como bombas y resistencias de calentamiento).

#### 3.1.1 Arquitectura General del Hardware
A continuación, se presenta la organización de los bloques funcionales que componen el sistema, detallando la interconexión de los periféricos críticos.
* **STM32F103 (Nucleo):** Actúa como el cerebro central del sistema.
* **ADC1 (Entrada Analógica):** Conectado al sensor de temperatura y/o nivel para el monitoreo del agua.
* **I2C1 (Bus de Datos Compartido):** Comunica de forma bidireccional el microcontrolador con el Display LCD 16x2 (vía expansor PCF8574) y la memoria EEPROM (24C02).
* **TIM1 (Temporizador de Captura):** Interfaz directa con los pines Echo y Trigger del sensor ultrasónico.
* **TIM2 (Temporizador PWM):** Salida de modulación por ancho de pulso para accionar los actuadores de potencia (bomba y calentador).
* **GPIO (Entradas Digitales):** Conexión con la matriz de botones de la interfaz de usuario.
* **UART (Salida Serial):** Envío de registros (logger) hacia la computadora para diagnóstico.

#### 3.1.2 Asignación de Pines y Multiplexación (Tabla de Coexistencia)
Para evitar conflictos con las interfaces de depuración y comunicación nativas de la placa Nucleo, se diseñó la siguiente distribución de pines, justificando la exclusión de ciertas líneas críticas:

| Periférico | Pin STM32 | Función HAL | Criterio de Selección / Justificación |
| :--- | :--- | :--- | :--- |
| **Debug/SWD** | PA13 / PA14 | SYS_SWDIO / SYS_SWCLK | Reservados. Se mantuvieron libres para garantizar la programación y depuración en tiempo real a través del ST-Link. |
| **Logger** | PA2 / PA3 | USART2_TX / USART2_RX | Reservados. Conectados internamente al puerto COM virtual del ST-Link para el volcado de logs hacia la PC. |
| **Sensor Distancia** | PA8 | TIM1_CH1 (Input Capture) | Uso de canales de temporizador nativos para medir el ancho de pulso del eco de forma precisa por hardware sin bloquear la CPU. |
| **Bus I2C1** | PB6 / PB7 | I2C1_SCL / I2C1_SDA | Se seleccionó este bus compartido para comandar tanto el Display LCD (vía expansor PCF8574) como la memoria EEPROM, ahorrando un total de 4 pines GPIO. |
| **Actuadores** | PA0 | TIM2_CH1 (PWM) | Generación de señal PWM por hardware para el control gradual de potencia de la bomba de agua. |
| **Botones** | PC0 / PC3 | GPIO_Input (Pull-up) | Pines limpios en el Puerto C, alejados de las líneas JTAG nativas (PB3/PB4) que suelen causar falsos disparos. |

#### 3.1.3 Problemas Encontrados y Criterios de Diseño (Hardware)
* **Conflicto de Voltajes (5V vs 3.3V):** El sensor ultrasónico y algunos displays LCD operan de forma nativa a 5V, mientras que el STM32 trabaja a 3.3V. Se aplicó el criterio de usar pines clasificados como FT (Five-Volt Tolerant) en el microcontrolador y se implementaron divisores de tensión en las líneas de retorno para proteger las entradas del ADC y del Timer.
* **Ahorro de Pines mediante I2C:** Inicialmente se evaluó una conexión paralela de 4 bits para el display. Sin embargo, debido a la cantidad de tareas concurrentes (ADC, Sensores, Botones), se optó por un esquema de bus compartido I2C para el LCD y la EEPROM, reduciendo drásticamente la complejidad del cableado.

---

### 3.2 Firmware del Sistema de Control de Cafetera
El firmware se diseñó bajo un paradigma de arquitectura cooperativa multitarea basada en tiempo, gobernada por interrupciones periódicas del temporizador del sistema (SysTick) y procesada mediante máquinas de estado finitas (FSM) no bloqueantes.

#### 3.2.1 Arquitectura del Software y Planificación de Tareas
Para evitar el uso de un RTOS completo y mantener bajo el consumo de memoria, se implementó un planificador (scheduler) básico en el módulo de sistema. Las tareas se ejecutan en el lazo principal evaluando banderas de tiempo de manera periódica:

| Tarea | Archivo Fuente | Período (ms) | Prioridad | Descripción / Función |
| :--- | :--- | :--- | :--- | :--- |
| **task_botones** | `task_botones.c` | 20 | Alta | Lectura de entradas analógicas/digitales y filtrado de rebotes (debounce). |
| **task_sensor** | `task_sensor.c` | 50 | Alta | Disparo del Trigger y lectura del Input Capture del sensor ultrasónico de nivel. |
| **task_adc** | `task_adc.c` | 100 | Media | Adquisición de temperatura por DMA para no interrumpir el lazo principal. |
| **task_cafe_fsm**| `task_cafe_fsm.c`| 10 | Crítica | Núcleo del negocio. Transiciones de estado de la cafetera. |
| **task_display** | `task_display.c` | 200 | Baja | Actualización de la interfaz visual en el LCD. |
| **logger** | `logger.c` | 500 | Baja | Transmisión asincrónica de estados hacia la UART. |

#### 3.2.2 Máquina de Estados de la Cafetera (FSM)
La lógica de control de la preparación del café se modeló mediante una máquina de estados finitos central. Cada estado es estrictamente no bloqueante, apoyándose en contadores de ticks de software para las esperas. Los estados principales son:
* **ST_REPOSO:** El sistema espera a que el usuario interactúe. Muestra un mensaje de bienvenida en la interfaz.
* **ST_SELECCION:** Monitorea los botones para determinar el tamaño y tipo de café elegidos.
* **ST_MOLIDO:** Activa el actuador del molino durante un tiempo parametrizado que es rescatado de la memoria EEPROM.
* **ST_SERVIDO:** Controla la temperatura del agua mediante el ADC y acciona la bomba de agua hasta que el sensor ultrasónico detecte que la taza está llena.

#### 3.2.3 Fragmentos de Código Relevantes
A modo de ejemplo de la implementación no bloqueante, se presenta el núcleo del manejo de temporización en la interrupción de SysTick (Código 3.1):

```c
// Código 3.1: Manejo de Base de Tiempo
void app_it_init(void) {
    g_app_tick_cnt = 0;
}

void HAL_SYSTICK_Callback(void) {
    g_app_tick_cnt++;
    if ((g_app_tick_cnt % 20) == 0) {
        flag_task_botones = 1;
    }
    if ((g_app_tick_cnt % 100) == 0) {
        flag_task_adc = 1;
    }
}
```

##### Análisis del Código 3.1:
* En las **líneas 1 a 3**, se observa la función de inicialización donde la variable global `g_app_tick_cnt` se fuerza a un estado inicial seguro e igual a cero, evitando desbordamientos indeterminados en el arranque.
* En la **línea 5**, se implementa el Callback nativo de la HAL para el SysTick, el cual se ejecuta de forma asincrónica cada 1 milisegundo.
* En las **líneas 7 a 9**, se realiza una operación de módulo para emular un temporizador de software; cada vez que transcurren 20 ms, se levanta la bandera `flag_task_botones` para que el lazo principal ejecute la lectura de periféricos sin detener el resto del sistema, manteniendo la filosofía no bloqueante.

#### 3.2.4 Problemas Encontrados y Criterios de Diseño (Firmware)
* **Referencias indefinidas en la etapa de Enlazado (Linker):** Durante la integración de los módulos independientes de hardware (LCD y Sensores), el enlazador arrojó errores de funciones faltantes correspondientes a la transmisión I2C y el inicio del Timer. El criterio de solución fue corregir el archivo de configuración global del HAL para habilitar explícitamente los módulos de hardware omitidos y forzar al generador de código a enlazar las librerías estáticas correspondientes.
* **Uso de DMA para el ADC:** Inicialmente, la lectura continua del sensor analógico mediante técnica de polling (`HAL_ADC_PollForConversion`) bloqueaba el procesador por varios microsegundos, afectando la precisión de lectura del sensor ultrasónico. Se resolvió aplicando el criterio de configurar el ADC en modo circular asistido por Acceso Directo a Memoria (DMA), volcando las muestras directamente en memoria RAM en segundo plano de manera transparente para la CPU.

#### 3.2.5 Repositorio del Proyecto
El código fuente completo, el historial de cambios y los esquemáticos de conexión se encuentran disponibles en el siguiente repositorio público:

**Enlace al repositorio:** [https://github.com/emikiuan/tdse-tpf_2026-1C_Curso01-Grupo05](https://github.com/emikiuan/tdse-tpf_2026-1C_Curso01-Grupo05)

En la raíz de este repositorio se incluye un archivo `README.md` en el que se detallan los requisitos de compilación y las instrucciones para que cualquier usuario pueda clonar el proyecto, compilarlo a través de STM32CubeIDE y replicar la funcionalidad documentada en el presente informe.

---

## CAPÍTULO 4: Ensayos y resultados

### 4.1 Pruebas funcionales del hardware
La idea de esta sección es explicar cómo se hicieron los ensayos, qué resultados se obtuvieron y analizarlos.  
Es muy importante que haya fotografías que sirvan de evidencia de que los ensayos realmente se hicieron.  
También es esperable que haya tablas o gráficos que presenten los resultados obtenidos.

### 4.2 Pruebas funcionales del firmware
La idea de esta sección es explicar cómo se hicieron los ensayos, qué resultados se obtuvieron y analizarlos.  
Es muy importante que haya fotografías que sirvan de evidencia de que los ensayos realmente se hicieron.  
También es esperable que haya tablas o gráficos que presenten los resultados obtenidos.

### 4.3 Pruebas de integración
Las pruebas de integración son aquellas que se realizan en el ámbito del desarrollo de software una vez que se han aprobado las pruebas unitarias y lo que prueban es que todos los elementos unitarios que componen el software, funcionan juntos correctamente probándolos en grupo.  

Se pueden incluir fotos o links a vídeos donde se aprecien las pruebas de integración desarrolladas y los resultados obtenidos. En esta sección se espera encontrar un análisis similar al presentado en la Tabla 12.36 del libro.

### 4.4 Cumplimiento de requisitos
En esta sección se espera encontrar un análisis similar al presentado en la Tabla 12.35 del libro.

### 4.5 Comparación con otros sistemas similares
Esta sección sería la continuación del análisis de sistemas similares presentados en el Capítulo 1. La diferencia es que en este caso se incluye en la comparación al desarrollo realizado. Esta comparación se recomienda que se haga mediante una tabla.

### 4.6 Documentación del desarrollo realizado
En esta sección se espera encontrar una tabla similar a la Tabla 12.37 que se presenta en el libro.

---

## CAPÍTULO 5: Conclusiones

### 5.1 Resultados obtenidos
La idea de esta sección es resaltar cuáles son los principales aportes del trabajo realizado. Debe ser especialmente breve y concisa. Es buena idea usar un listado para enumerar los logros obtenidos.

### 5.2 Próximos pasos
Acá se indica bien breve cómo se podría continuar el trabajo más adelante. Se propone incluir un análisis al respecto similar al que se realiza en el libro en relación a la mencionada Tabla 12.37, donde se discuten las mejoras adicionales que se podrían realizar en el futuro.

---

## Bibliografía

* **[1]** IEEE (2016, Jun 26). *IEEE Citation Reference* [Online]. Available: [http://www.ieee.org/documents/ieeecitationref.pdf](http://www.ieee.org/documents/ieeecitationref.pdf)
* **[2]** Proyecto CIAA (2016, Jun 26). *EDU-CIAA-NXP* [Online]. Available: [http://www.proyecto-ciaa.com.ar/devwiki/doku.php](http://www.proyecto-ciaa.com.ar/devwiki/doku.php)

---

## Anexos

### A. Primer Anexo
En caso de ser necesario utilizar anexos, siguiendo siempre el mismo formato que para el cuerpo principal de la Memoria.
