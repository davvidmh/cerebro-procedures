# Caso técnico: dirección de una colmena privada con ejecución remota verificable

**Responsable de objetivos y decisiones de arquitectura:** David, [@davvidmh](https://github.com/davvidmh).

**Modalidad:** proyecto personal con implementación asistida por inteligencia artificial. Este caso distingue las decisiones del responsable, el trabajo realizado con asistencia y los resultados que tienen evidencia. No atribuye al responsable ejecución manual de cada comando, autoría exclusiva del código generado ni competencias profesionales no evaluadas.

## Problema y evolución del encargo

Desde el inicio del trabajo se buscó aprovechar una máquina virtual de coste contenido para servir a proyectos locales. El alcance evolucionó desde conectividad y continuidad de acceso hasta una arquitectura que pudiera recibir peticiones concretas, coordinar ejecutores especializados y devolver entregables pequeños al equipo de origen.

Las prioridades planteadas por David fueron: privacidad de los proyectos, operación remota por consola, aprovechamiento selectivo de recursos existentes, separación de responsabilidades y evidencia de que el trabajo ocurrió en el servidor previsto.

## Decisiones del responsable y capacidades que permiten observar

| Decisión o exigencia de David | Capacidad observable | Evidencia y límite |
|---|---|---|
| Solicitar comparar recursos disponibles de la infraestructura antes de adoptarla y considerar almacenamiento, acceso y continuidad | Formulación de requisitos de infraestructura y atención al coste operativo | El caso parte de una máquina virtual y acceso por SSH; la guía pública de recuperación se enlaza abajo. No se publican datos reales de la instancia. |
| Definir una jerarquía de coordinador principal, herramientas orquestadoras y ejecutores con funciones específicas | Descomposición de responsabilidades y diseño de coordinación | El procedimiento general documenta esa separación; no se presenta una colmena completa como producto terminado. |
| Aclarar que revisar todos los recursos no significa instalarlos, y excluir una referencia contable sin demanda actual | Selección por necesidad, control del alcance y reducción de dependencias | La arquitectura admite herramientas específicas cuando existe una petición aplicable. El inventario privado no se copia a esta publicación. |
| Exigir que el servidor se opere por consola, incluyendo transferencias | Diseño de operación sin intervención gráfica | El piloto usa cola, worker de consola, comprobaciones y devolución por SSH. No depende de mover ventanas o de un panel. |
| Detectar que ejecutar el piloto en el equipo cliente no validaba el servidor y exigir la corrección | Revisión de evidencia contra el requisito original y criterio de aceptación | La entrega publicada procede de ejecución y pruebas posteriores en Oracle. Los intentos locales fallidos no se contabilizan como éxito del servidor. |
| Pedir tareas muy específicas, revisadas antes de enviarse y con retorno al proyecto correcto | Diseño de contratos de trabajo y trazabilidad | Hay un protocolo de petición/entrega en desarrollo. No se afirma que el transporte automático de todas las bandejas esté operativo. |
| Separar información pública de propiedad intelectual reservada y pedir devoluciones que el coordinador conversacional no abra | Identificación de fronteras de confianza y requisitos de custodia de claves | La política vigente exige cifrado y recepción ciega. Su verificación depende de una clave pública del destinatario y del flujo todavía pendiente. No se promete protección frente a un anfitrión comprometido. |
| Diferenciar un bloqueo físico —por ejemplo, falta de un medio externo— de una investigación difícil que puede explorarse | Evaluación de factibilidad y planteamiento de experimentos | La exploración criptográfica se formula con pruebas y límites. No existe una ruptura demostrada de SHA-256. |

Estos puntos documentan decisiones y criterios observados en este proyecto. No constituyen una certificación de nivel, experiencia laboral, auditoría de seguridad completa o resultados económicos.

## Experimento que sí tiene evidencia pública

**Encargo:** obtener un programa Java mínimo que transforme una cadena de ejemplo en un resumen y usarlo para validar el recorrido remoto.

**Ejecución:** una tarea de la cola de Oracle fue tomada por un worker en el mismo servidor. GPT4Free 8.7.7, mediante LLM7, devolvió código. Tras revisar esa entrega pública, se compiló y se ejecutaron seis casos en Oracle, bajo una cuenta de servicio sin privilegios, sin red en la validación y con límites de recursos. El paquete regresó por SSH y se comprobaron sus huellas.

**Resultado:** [repositorio del piloto Java](https://github.com/davvidmh/java-one-way-hash-demo), con [código](https://github.com/davvidmh/java-one-way-hash-demo/blob/main/OneWayHash.java), [recibo del adaptador](https://github.com/davvidmh/java-one-way-hash-demo/blob/main/evidence/LLM7-receipt.json), [pruebas](https://github.com/davvidmh/java-one-way-hash-demo/blob/main/evidence/validation.json) y [comprobación de transferencia](https://github.com/davvidmh/java-one-way-hash-demo/blob/main/evidence/transfer.json).

El proveedor no acreditó la identidad del modelo subyacente. Un adaptador que falló se documentó como fallo. El éxito corresponde a esta tarea acotada, no a todos los repositorios candidatos ni a una flota permanente de agentes.

## Qué aportó la pregunta sobre funciones no inyectivas

David propuso explorar la transformación de una cadena y su relación con una función no inyectiva. La implementación educativa permitió precisar tres conceptos: hashing, falta de inversa única y dificultad computacional de recuperar una entrada.

La no inyectividad no demuestra por sí sola seguridad criptográfica. Una entrada como `hola` puede reconocerse comparando candidatos. El verificador incluye esa demostración y la documentación evita presentar el resultado como cifrado recuperable o como ruptura de SHA-256. La investigación posterior solicitada sigue sin un resultado de ruptura demostrado.

## Estado y límites del caso

Comprobado: coordinación mínima, un worker remoto de una sola ejecución, respuesta externa a una tarea pública, compilación/pruebas en el servidor y devolución íntegra por SSH.

Pendiente: identidades restringidas por worker, cifrado de nuevas devoluciones para una clave bajo custodia del destinatario, recogida automática de peticiones y validación de más tipos de tarea. Los requisitos de devolución sin lectura son posteriores al piloto público y no autorizan publicar resultados privados futuros.

La implementación asistida se declara para que el caso pueda evaluarse por sus decisiones, evidencia y límites. No se publica la conversación privada ni se utiliza como prueba una afirmación que carezca de un entregable verificable.

## Referencias relacionadas

- [Procedimiento general del cerebro](README.md).
- [Guía pública de recuperación SSH, con ejemplos sanitizados](https://github.com/davvidmh/oracle-ssh-recovery-guide).
- [Piloto Java y explicación de sus límites](https://github.com/davvidmh/java-one-way-hash-demo).
