# Decisiones técnicas

| Necesidad | Solución |
|---|---|
| Recuperar SSH sin dejar permisos provisionales | Recuperación con identidad verificada y retirada de accesos temporales. |
| Aprovechar recursos limitados | Evaluar el inventario completo y desplegar solo herramientas con demanda real. |
| Operar sin escritorio | Cola persistente, servicios de sistema y transferencias por SSH. |
| Avanzar hacia autonomía completa | Encadenar planificación, elaboración, revisión y correcciones, conservando el objetivo original hasta consolidar la entrega. |
| Evitar tareas ambiguas | Objetivo, entregables, criterios medibles, presupuesto e identificador; revisión vinculada a la huella. |
| Revisar antes de entregar | Auditoría de todos los criterios y hasta tres rondas de corrección dentro de los límites autorizados. |
| Mantener privadas las devoluciones | Compresión en memoria y cifrado age para una clave custodiada por el destinatario. |
| Mantener el acceso a modelos de IA | VPN por aplicación para las peticiones a proveedores; esperas, reintentos y alternativas autorizadas ante interrupciones. |

## Evidencia y alcance

El [piloto Java](https://github.com/davvidmh/java-one-way-hash-demo) se generó mediante g4f, se compiló y pasó seis comprobaciones en Oracle. Después se verificaron flujos de tres roles con peticiones a los modelos tanto directas como mediante VPN. Las devoluciones se cifraron y transfirieron por SSH. La nueva auditoría pasó pruebas de omisiones, correcciones y límites, y una prueba sintética con IA real.

Recepción, aprobación interna del modelo y aceptación del destinatario son estados distintos. No se atribuye un modelo remoto sin evidencia ni se considera una revisión del modelo equivalente a pruebas ejecutadas.

La autonomía completa guía la arquitectura: el usuario define el encargo y la colmena coordina su resolución, revisión y devolución. La VPN se aplica a la comunicación con los modelos; el transporte de archivos utiliza SSH. El destinatario conserva el control de la clave y de la aceptación final de sus entregables.

[Procedimiento SSH](https://github.com/davvidmh/oracle-ssh-recovery-guide) · [ECC](https://github.com/affaan-m/ECC) · [g4f](https://github.com/xtekky/gpt4free) · [age](https://github.com/FiloSottile/age)

## Ejecución sin escritorio

Las sesiones de navegador necesarias para un proveedor se ejecutan aisladas en Oracle, sin interfaz gráfica, con sandbox y acceso de control limitado a localhost. Cada sesión se elimina al terminar. Los workers tienen límites de memoria y procesos; los reintentos respetan la espera de cada proveedor. La revisión interna exige evidencia por criterio antes de declarar un entregable consolidado.
