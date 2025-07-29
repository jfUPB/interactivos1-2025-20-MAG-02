# Unidad 2
## Introducción 📜
En esta unidad vamos a profundizar un poco más en la programación del computador embebido o micro:bit. Vamos a estudiar una técnicas de programación basada en máquinas de estados que nos permitirá crear programas más complejos y con mayor control sobre el flujo de ejecución. Esta técnica de programación no es exclusiva del micro:bit, sino que se utiliza en muchos otros lenguajes de programación y plataformas, por lo que es una habilidad valiosa para cualquier ingeniero en diseño de entretenimiento digital. En la próxima unidad verás cómo podrás transferir esta técnica a otros lenguajes de programación y plataforma.

## 🔎 Fase: Set + Seek

### Set: ¿Qué aprenderás en esta unidad? 💡
Vas a resolver problemas de programación en el micro:bit utilizando máquinas de estados.

### Actividad 1
1. **Describe detalladamente cómo funciona este ejemplo.**  
Este ejemplo crea 2 objetos `Pixel`, los inicializa con coordenadas e intervalos diferentes, y luego los actualiza constantemente por medio de un while. Algo notorio en el código es que no utiliza `sleep()`, sino intervalos de tiempo que no se interrumpen entre sí.
2. **¿Cuáles son los estados en el programa?**  
Está el estado `WaitTimeout` y el pseudo-estado `Init`.
3. **¿Cuáles son los eventos/inputs en el programa?**  
Sólo hay un evento, que es cuando pasa el tiempo especificado en el intervalo (`if utime.ticks_diff()`).
4. **¿Cuáles son las acciones en el programa?**  
El conteo del tiempo/"mirar la hora" (`self.startTime`), cambiar el estado de los Pixeles (`self.pixelState`), cambiar el estado del objeto (`self.state`)
