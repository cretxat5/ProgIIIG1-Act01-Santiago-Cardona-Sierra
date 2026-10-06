# Guión Completo de Exposición: Algoritmo de Planificación FCFS (First-Come, First-Served)

**Asignatura:** Sistemas Operativos  
**Tema:** Algoritmos de Planificación de CPU — FCFS  
**Duración Estimada:** 12 a 15 minutos  
**Equipo de Expositores:** Jorge Stiven Calderón, Carlos Eduardo Grisales, Miguel Ángel Amaya, Santiago Cardona  

---

## Estructura General y Distribución de Roles

| Bloque / Sección | Contenido Principal | Orador Asignado | Tiempo Estimado |
| :--- | :--- | :--- | :--- |
| **0. Apertura** | Saludo inicial, presentación del grupo e introducción al tema | **Miguel** & **Santiago** | 1:30 min |
| **1. Fundamentos** | Lógica, funcionamiento, criterio de selección y tipo de algoritmo | **Jorge** | 2:30 min |
| **2. Métricas Clave** | Definición y fórmulas de Tiempo de Retorno, Espera y Respuesta | **Jorge** | 2:00 min |
| **3. Ejemplo Práctico** | Simulación de 4 procesos, Diagrama de Gantt y cálculo numérico | **Carlos** | 4:30 min |
| **4. Análisis Crítico** | Ventajas, desventajas, efecto convoy y escenarios de uso | **Miguel** | 2:30 min |
| **5. Conexión de Clase** | Vinculación con Clases 04B (Evolución), 05B (Gestión) y 06B (Interrupciones) | **Santiago** | 2:00 min |
| **6. Cierre** | Síntesis general, despedida formal y apertura a preguntas | **Miguel** & **Santiago** | 1:00 min |

---

## Guión Literario y Técnico con Acotaciones

### Bloque 0: Saludo Inicial e Introducción General
*(Tiempo estimado: 1:30 min — Oradores: Miguel y Santiago)*

`[Diapositiva 1: Portada — "Algoritmo de Planificación FCFS en Sistemas Operativos" | Integrantes: Jorge Calderón, Carlos Grisales, Miguel Amaya, Santiago Cardona]`

`[Acotación: Miguel y Santiago se ubican al frente del aula. Miguel toma la iniciativa con tono seguro y acogedor, mientras Santiago complementa de forma entusiasta.]`

* **Miguel:**  
  "Muy buenos días a todos, profesor y compañeros. Sean bienvenidos a nuestra presentación. El día de hoy, nuestro grupo, conformado por Jorge Calderón, Carlos Grisales, Santiago Cardona y mi persona, Miguel Amaya, les estará exponiendo a fondo uno de los conceptos pilares en la gestión de recursos del sistema operativo: el **Algoritmo de Planificación de CPU First-Come, First-Served**, universalmente conocido por sus siglas **FCFS**."

* **Santiago:**  
  "Así es, Miguel. Cuando en un sistema operativo tenemos múltiples procesos compitiendo por un único núcleo de procesamiento, el planificador de la CPU debe aplicar un criterio estricto para decidir a quién asignarle el procesador y en qué orden. FCFS es el punto de partida histórico y conceptual de todos los algoritmos de planificación. Comprender su comportamiento es fundamental, ya que representa la política más intuitiva a partir de la cual evolucionaron las soluciones modernas. Sin más preámbulos, le cedo la palabra a mi compañero Jorge, quien nos explicará la lógica interna de este algoritmo."

---

### Bloque 1: Explicación del Algoritmo FCFS
*(Tiempo estimado: 2:30 min — Orador: Jorge)*

`[Diapositiva 2: Lógica y Funcionamiento de FCFS — "First-Come, First-Served / Cola FIFO"]`

`[Acotación: Jorge avanza hacia el centro del escenario y señala los puntos clave en la pantalla.]`

* **Jorge:**  
  "Muchas gracias, Santiago. Para entender FCFS, la clave reside en su propio nombre: *First-Come, First-Served*, o 'el primero en llegar es el primero en ser atendido'. Este algoritmo opera bajo una estricta política **FIFO** (*First-In, First-Out*).

  Conceptualmente, imaginen una fila en el banco o en el supermercado: el primer proceso que entra a la cola de listos (*ready queue*) es exactamente el primer proceso al que el planificador le otorga el control de la CPU. El criterio de selección es unívoco: se selecciona el proceso que lleva más tiempo esperando en la cola."

`[Diapositiva 3: Clasificación del Algoritmo: No Apropiativo y Ausencia de Quantum]`

* **Jorge:**  
  "Ahora bien, es vital clasificar correctamente a FCFS según la naturaleza de su control. FCFS es un algoritmo strictly **no apropiativo** (*non-preemptive*). ¿Qué significa esto en la práctica? Significa que una vez que a un proceso se le concede el uso de la CPU, este conserva el procesador de forma ininterrumpida hasta que ocurre uno de dos eventos:
  1. El proceso **finaliza por completo** su ráfaga de ejecución.
  2. El proceso realiza voluntariamente una **solicitud de Entrada/Salida (E/S)** u otra llamada al sistema que lo bloquee.

  Bajo FCFS, el sistema operativo **no puede quitarle la CPU de manera forzada** a un proceso en ejecución. Asimismo, es importante remarcar que este algoritmo **no requiere ni utiliza quantum de tiempo** (*time-slice*); no existen límites temporales prefijados por proceso. Si un proceso ingresa a la CPU, se adueña de ella hasta concluir su ciclo."

---

### Bloque 2: Fórmulas y Cálculo de Métricas Clave
*(Tiempo estimado: 2:00 min — Orador: Jorge)*

`[Diapositiva 4: Métricas Clave de Evaluación del Planificador]`

`[Acotación: Jorge utiliza el apuntador para resaltar las fórmulas matemáticas expuestas en la diapositiva.]`

* **Jorge:**  
  "Para evaluar qué tan eficiente resulta un algoritmo de planificación, nos apoyamos en cuatro métricas cuantitativas clave. Es fundamental comprender la definición de cada una:

  1. **Tiempo de Finalización ($TF$):** Es el instante de tiempo absoluto en el cual el proceso termina su ejecución completa en la CPU.
  2. **Tiempo de Retorno ($TR$):** Mide la estancia total del proceso en el sistema, desde que llega hasta que finaliza. Se calcula como:
     $$TR = TF - \text{Tiempo de llegada}$$
  3. **Tiempo de Espera ($TE$):** Es el tiempo total acumulado que el proceso permanece inactivo dentro de la cola de listos esperando a ser atendido. Su fórmula es:
     $$TE = TR - \text{Ráfaga de CPU}$$
  4. **Tiempo de Respuesta ($TResp$):** Corresponde al intervalo transcurrido desde que el proceso llega a la cola de listos hasta que obtiene la CPU por primera vez:
     $$TResp = \text{Instante de primera asignación de CPU} - \text{Tiempo de llegada}$$"

`[Acotación: Jorge enfatiza con la voz la siguiente deducción teórica.]`

* **Jorge:**  
  "Aquí quiero que presten especial atención a una propiedad matemática exclusiva de FCFS: debido a que FCFS es **no apropiativo**, cada proceso se ejecuta de corrido en un único bloque continuo. Como no hay interrupciones ni fragmentación de la ráfaga, **el Tiempo de Espera ($TE$) y el Tiempo de Respuesta ($TResp$) coinciden numéricamente para todos los procesos** ($TE = TResp$).

  A continuación, le doy el paso a mi compañero Carlos, quien nos ilustrará estos conceptos mediante un ejemplo práctico numérico."

---

### Bloque 3: Ejemplo Práctico, Diagrama de Gantt y Cálculos
*(Tiempo estimado: 4:30 min — Orador: Carlos)*

`[Diapositiva 5: Ejemplo Práctico con 4 Procesos — Tabla de Entrada]`

`[Acotación: Carlos pasa al frente con confianza, señalando la tabla de procesos.]`

* **Carlos:**  
  "Gracias, Jorge. Vamos a aterrizar toda esta teoría analizando un caso de simulación con $4$ procesos: $P1$, $P2$, $P3$ y $P4$. Revisemos sus datos de entrada:

  * **$P1$:** Llega en el instante $t = 0$ y requiere una ráfaga de CPU de $8$ unidades.
  * **$P2$:** Llega en el instante $t = 1$ con una ráfaga de $4$ unidades.
  * **$P3$:** Llega en el instante $t = 2$ con una ráfaga de $9$ unidades.
  * **$P4$:** Llega en el instante $t = 3$ con una ráfaga de $5$ unidades.

  Veamos el paso a paso del comportamiento de la cola de listos y la CPU a lo largo del tiempo:"

`[Diapositiva 6: Simulación Paso a Paso y Construcción del Diagrama de Gantt]`

`[Acotación: Carlos simula en el tablero o pantalla el avance del reloj de simulación.]`

* **Carlos:**  
  * **En $t = 0$:** Llega $P1$. Como la CPU está totalmente libre, $P1$ toma la CPU de inmediato. La cola de listos queda vacía.
  * **En $t = 1$, $t = 2$ y $t = 3$:** Van arribando sucesivamente $P2$, $P3$ y $P4$. Se forman en orden FIFO en la cola de listos: primero $P2$, luego $P3$, y al final $P4$.
  * **En $t = 8$:** $P1$ completa sus $8$ unidades de ráfaga ($0 \to 8$) y abandona el sistema. El planificador toma el frente de la cola, que es $P2$, y le asigna la CPU de $t = 8$ a $t = 12$.
  * **En $t = 12$:** $P2$ concluye su ráfaga de $4$ unidades ($8 \to 12$). Ingresa $P3$ a la CPU, ejecutándose durante $9$ unidades, desde $t = 12$ hasta $t = 21$.
  * **En $t = 21$:** $P3$ finaliza ($12 \to 21$). Finalmente, $P4$ pasa a la CPU para ejecutar sus $5$ unidades restantes, de $t = 21$ a $t = 26$.

  El **Diagrama de Gantt** resultante muestra los bloques contiguos: $P1$ de $0$ a $8$, $P2$ de $8$ a $12$, $P3$ de $12$ a $21$, y $P4$ de $21$ a $26$, acumulando un tiempo total de ejecución de $26$ unidades."

`[Diapositiva 7: Tabla Resumen de Métricas Calculadas y Promedios]`

`[Acotación: Carlos desglosa los cálculos cuantitativos apoyándose en los valores tabulados.]`

* **Carlos:**  
  "Ahora, calculemos las métricas individuales y promedios para cada proceso:

  | Proceso | Llegada | Ráfaga | Inicio | Fin ($TF$) | Retorno ($TR = TF - \text{Llegada}$) | Espera ($TE = TR - \text{Ráfaga}$) | Respuesta ($TResp = \text{Inicio} - \text{Llegada}$) |
  | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
  | **P1** | $0$ | $8$ | $0$ | $8$ | $8 - 0 = \mathbf{8}$ | $8 - 8 = \mathbf{0}$ | $0 - 0 = \mathbf{0}$ |
  | **P2** | $1$ | $4$ | $8$ | $12$ | $12 - 1 = \mathbf{11}$ | $11 - 4 = \mathbf{7}$ | $8 - 1 = \mathbf{7}$ |
  | **P3** | $2$ | $9$ | $12$ | $21$ | $21 - 2 = \mathbf{19}$ | $19 - 9 = \mathbf{10}$ | $12 - 2 = \mathbf{10}$ |
  | **P4** | $3$ | $5$ | $21$ | $26$ | $26 - 3 = \mathbf{23}$ | $23 - 5 = \mathbf{18}$ | $21 - 3 = \mathbf{18}$ |

  Procedemos a calcular los valores promedios globales:

  * **Tiempo de Espera Promedio:**  
    $$\bar{TE} = \frac{0 + 7 + 10 + 18}{4} = \frac{35}{4} = \mathbf{8.75} \text{ unidades de tiempo}$$
  * **Tiempo de Retorno Promedio:**  
    $$\bar{TR} = \frac{8 + 11 + 19 + 23}{4} = \frac{61}{4} = \mathbf{15.25} \text{ unidades de tiempo}$$
  * **Tiempo de Respuesta Promedio:**  
    $$\bar{TResp} = \frac{0 + 7 + 10 + 18}{4} = \frac{35}{4} = \mathbf{8.75} \text{ unidades de tiempo}$$

  Adicionalmente, destacamos que la CPU estuvo ocupada durante los $26$ instantes continuos, logrando una **utilización de la CPU del $100\%$**, con un rendimiento (*throughput*) de $\frac{4}{26} \approx \mathbf{0.1538}$ procesos por unidad de tiempo.

  Ahora, le cedo la palabra a Miguel para analizar las fortalezas, limitaciones y fenómenos críticos de este algoritmo."

---

### Bloque 4: Ventajas, Desventajas y Efecto Convoy
*(Tiempo estimado: 2:30 min — Orador: Miguel)*

`[Diapositiva 8: Ventajas del Algoritmo FCFS]`

`[Acotación: Miguel vuelve al centro de la escena con postura analítica.]`

* **Miguel:**  
  "Muchas gracias, Carlos. Hablemos del balance de fortalezas y debilidades de FCFS. Comenzando por sus **ventajas**:

  1. **Simplicidad de diseño e implementación:** Al basarse en una estructura de cola FIFO, las operaciones de encolar y desencolar tienen una complejidad algorítmica constante de $\mathcal{O}(1)$.
  2. **Equidad según orden de llegada:** Garantiza que no exista inanición (*starvation*). Todo proceso que ingresa a la cola terminará siendo atendido.
  3. **Mínimo sobrecosto (*overhead*):** Dado que los procesos no son desapropiados, los cambios de contexto son muy reducidos, ocurriendo únicamente por terminación o bloqueo por E/S."

`[Diapositiva 9: Desventajas y el Efecto Convoy (*Convoy Effect*)]`

* **Miguel:**  
  "Sin embargo, FCFS presenta desventajas muy severas en entornos modernos, siendo la principal de ellas el famoso **Efecto Convoy** (*Convoy Effect*).

  El efecto convoy sucede cuando un proceso con una ráfaga de CPU excesivamente larga llega primero a la cola de listos. Todos los procesos cortos que llegan justo después quedan trancados e inactivos detrás de él, como automóviles atascados detrás de un camión pesado en una carretera de un solo carril. Esto genera dos grandes problemas:
  * El **Tiempo de Espera Promedio se dispara de forma dramática**, variando drásticamente según el orden aleatorio de llegada.
  * Se genera una **subutilización de los dispositivos de Entrada/Salida**, ya que los procesos de E/S están parados en la cola de la CPU en lugar de estar realizando transferencias.

  Por esta razón, FCFS presenta un desempeño deficiente en **sistemas interactivos**, donde los usuarios requieren respuestas inmediatas."

`[Diapositiva 10: Escenarios Ideales vs. Escenarios de Falla]`

* **Miguel:**  
  "En resumen:
  * **Escenario Ideal:** Sistemas por lotes (*Batch Systems*), donde las ráfagas de los procesos tienen duraciones homogéneas y no hay usuarios interactivos esperando respuesta en pantalla.
  * **Escenario donde Falla:** Sistemas interactivos de tiempo compartido y sistemas de tiempo real (*Real-Time Systems*).

  A continuación, Santiago relacionará estos descubrimientos con los temas vistos en nuestras clases."

---

### Bloque 5: Conexión con el Material de Clase
*(Tiempo estimado: 2:00 min — Orador: Santiago)*

`[Diapositiva 11: Vinculación Curricular — Clases 04B, 05B y 06B]`

`[Acotación: Santiago retoma la palabra para contextualizar el tema dentro del currículo académico.]`

* **Santiago:**  
  "Gracias, Miguel. Es sumamente enriquecedor conectar el funcionamiento de FCFS con los temas abordados a lo largo del curso:

  1. **Conexión con la Clase 04B (Evolución y Tipos de SO):**  
     FCFS refleja exactamente el paradigma operativo de la primera generación de **Sistemas Por Lotes (Batch Processing)**. La incapacidad de FCFS para ofrecer tiempos de respuesta ágiles fue justamente la gran fuerza motriz que impulsó la invención de los **Sistemas de Tiempo Compartido (Time-Sharing Systems)** y la aparición de algoritmos con desapropiación como Round Robin.

  2. **Conexión con la Clase 05B (Gestión del Sistema Operativo):**  
     FCFS es la política de planificación de corto plazo (*Short-Term Scheduler*) más elemental aplicada sobre la cola de procesos listos en el Bloque de Control de Procesos (PCB). Destaca por su mínimo *overhead*, ya que reduce a la menor expresión posible los cambios de contexto por unidad de tiempo.

  3. **Conexión con la Clase 06B (Interrupciones):**  
     FCFS **no hace uso de la interrupción del temporizador (*Timer Interrupt*)**, puesto que carece de quantum. La única interrupción que interactúa con FCFS es la **interrupción por finalización de E/S**, la cual notifica al SO que un proceso bloqueado ha terminado su transferencia y debe reingresar al final de la cola de listos. Además, conceptualmente se compara con el *Polling* por su extrema simplicidad de diseño, pero igualmente comparte su ineficiencia para entornos interactivos."

---

### Bloque 6: Conclusión y Despedida Final
*(Tiempo estimado: 1:00 min — Oradores: Miguel y Santiago)*

`[Diapositiva 12: Cierre y Preguntas — "¡Muchas gracias por su atención!"]`

`[Acotación: Miguel y Santiago vuelven a quedar juntos al frente del grupo. Miguel ofrece la síntesis de cierre y Santiago brinda la despedida final.]`

* **Miguel:**  
  "En conclusión, el algoritmo FCFS destaca por ser una solución justa en cuanto al orden de llegada, conceptualmente limpia y sumamente económica en términos de procesamiento del sistema operativo. No obstante, su rigidez no apropiativa y su alta sensibilidad al orden de llegada —reflejada en el efecto convoy— hacen que resulte inviable para los sistemas operativos interactivos actuales, funcionando hoy como la base teórica sobre la que se construyen esquemas más sofisticados."

* **Santiago:**  
  "Con esto concluimos nuestra exposición sobre el algoritmo FCFS. Agradecemos enormemente al profesor y a todos ustedes por su atención. Quedamos a su entera disposición para responder cualquier duda o inquietud que tengan. ¡Muchas gracias!"

`[Acotación: Los cuatro integrantes hacen una breve reverencia y se abre el espacio para preguntas de la audiencia y del docente.]`
