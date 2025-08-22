# Unidad 3


## 🤔 Fase: Reflect

### Parte 1: recuperación de conocimiento (Retrieval Practice)

1. **Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?**  
Una máquina de estados es un código/programa que funciona moviéndose de un estado a otro según ciertos eventos y ejecutando ciertas acciones específicas en cada estado. Está compuesta de *estados*, *eventos*, y *acciones*. No recuerdo cuál sería el 4to componenete :c
2. **Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender varios eventos y tareas “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el *micro:bit* o en *p5.js*. ¿Qué problema soluciona en comparación con usar funciones como `sleep()`?**  
El problema específico de `sleep()` es que detiene todo el código, por lo que no se podrían registrar otros eventos durante un tiempo. La máquina de estados pretende que el código está "atento" a los eventos en todo momento, y tiene una respuesta acorde que no interrumpirá la ejecución del código ni lo "distraerá" de otros eventos.
3. **Imagina que tienes que añadir una nueva funcionalidad a la bomba: si se recibe un evento especial (por ejemplo, una combinación de botones o un comando serial) *mientras* la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?**  
Ya que el evento es durante la cuenta regresiva, se sabe que el cambio se añadirá entre los eventos que se esperan en el estado "ARMED". Teniendo eso en cuenta, creo que se podría introducir como un condicional más dentro del que ya tenemos para reconocer la contraseña, reutilizando el código existente pero cambiando la comparación con `password` por un array nuevo de letras.
4. **Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.**  
Un vector de prueba simplemente es una línea de tiempo de lo que sucede en el código siguiendo una combinación de eventos y acciones, la cual que empieza desde un estado y termina en otro (o el mismo, algunas veces).

### Parte 2: reflexión sobre tu proceso (Metacognición)

1. **¿Qué parte del diseño de la bomba te resultó más desafiante: crear el diagrama de estados o traducir ese diagrama a código? ¿Por qué?**  
Ans
2. **Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?**  
Ans
3. **El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?**  
Ans
4. **Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?**  
Ans
