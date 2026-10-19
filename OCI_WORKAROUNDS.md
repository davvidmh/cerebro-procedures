# Decisiones técnicas

| Necesidad | Solución |
|---|---|
| Recuperar SSH sin dejar permisos provisionales | Recuperación con identidad verificada y retirada de accesos temporales. |
| Aprovechar recursos limitados | Evaluar el inventario completo y desplegar solo herramientas con demanda real. |
| Operar sin escritorio | Cola persistente, servicios de sistema y transferencias por SSH. |
| Evitar tareas ambiguas | Objetivo, entregables, criterios medibles, presupuesto e identificador; revisión vinculada a la huella. |
| Revisar antes de entregar | Auditoría de todos los criterios y hasta tres rondas de corrección dentro de los límites autorizados. |
| Mantener privadas las devoluciones | Compresión en memoria y cifrado age para una clave custodiada por el destinatario. |
| Manejar fallos del proveedor | Esperas, reintentos limitados y alternativas autorizadas; VPN por aplicación ante problemas de conectividad. |

## Evidencia y alcance

El [piloto Java](https://github.com/davvidmh/java-one-way-hash-demo) se generó mediante g4f, se compiló y pasó seis comprobaciones en Oracle. Después se verificaron flujos de tres roles y devoluciones cifradas, tanto directas como por VPN. La nueva auditoría pasó pruebas de omisiones, correcciones y límites, y una prueba sintética con IA real.

Recepción, aprobación interna del modelo y aceptación del destinatario son estados distintos. No se atribuye un modelo remoto sin evidencia ni se considera una revisión del modelo equivalente a pruebas ejecutadas.

La base actual produce texto y workflows; no ejecuta comandos generados ni procesa adjuntos privados. El cifrado no oculta al proveedor el texto que recibe. No hay garantía de cuota ilimitada, servicio continuo o factura cero de toda la cuenta. La restauración del respaldo sigue pendiente de comprobación privada.

[Procedimiento SSH](https://github.com/davvidmh/oracle-ssh-recovery-guide) · [ECC](https://github.com/affaan-m/ECC) · [g4f](https://github.com/xtekky/gpt4free) · [age](https://github.com/FiloSottile/age)
