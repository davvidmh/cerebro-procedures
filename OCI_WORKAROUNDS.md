# OCI Workarounds

Notas de infraestructura y decisiones de diseño para coordinar tareas desde Oracle Cloud Infrastructure y devolver entregables a proyectos locales. Diseño y dirección: [David (@davvidmh)](https://github.com/davvidmh). Implementación asistida por inteligencia artificial.

## Del acceso al servidor a un flujo de trabajo

El punto de partida fue aprovechar recursos de coste contenido y conservar acceso a la máquina. El diseño evolucionó hacia una cola de tareas, ejecutores especializados y entregas compactas. Los servicios se administran por consola; los archivos viajan por SSH. Los datos y la configuración reales quedan fuera de esta documentación pública.

| Problema | Decisión de diseño | Resultado o estado |
|---|---|---|
| Continuidad del acceso tras perder una clave local | Recuperar el acceso conservando la verificación de identidad y retirar permisos temporales | [Procedimiento público de recuperación SSH](https://github.com/davvidmh/oracle-ssh-recovery-guide). |
| Muchos recursos disponibles y una máquina limitada | Evaluar todos los candidatos y desplegar solo los que resuelven una necesidad vigente | Las referencias sin demanda, por ejemplo una aplicación contable de otro proyecto, quedan fuera del servidor. |
| Repartir trabajo entre varios ejecutores | Separar dirección, herramientas de orquestación y funciones específicas | El coordinador básico funciona; la integración de roles y workers persistentes sigue pendiente. |
| Servidor sin una persona operando ventanas | Usar consola, cola persistente y transferencias por SSH | El piloto se ejecutó y validó en Oracle, con devolución por SSH. |
| Una prueba en el equipo cliente no demuestra ejecución en Oracle | Exigir evidencia del entorno correcto | Los intentos locales iniciales fallaron y no se contabilizan. La entrega publicada procede de un worker y pruebas posteriores en Oracle. |
| Tareas ambiguas y resultados difíciles de atribuir | Exigir objetivo, límites, entregable, verificaciones e identificador | Convención local preparada; admisión y transporte automáticos aún en desarrollo. |
| Resultados que el coordinador conversacional no debe inspeccionar | Cifrar para una clave bajo custodia del destinatario y verificar solo metadatos externos | Se comprobó una transferencia de prueba cifrada sin leer el contenido; la integración automática sigue pendiente. |

## Primer recorrido comprobado

Una tarea pública solicitó un programa Java mínimo para transformar `hola` en un resumen SHA-256. El recorrido fue:

1. Petición en la cola de Oracle.
2. Worker de consola ejecutado en Oracle Linux ARM64.
3. GPT4Free 8.7.7 con el adaptador LLM7, sin suministrar claves de proveedores ni cookies personales.
4. Recepción y revisión del código público.
5. Compilación y seis comprobaciones en Oracle, bajo usuario sin privilegios, sin red en la validación y con límites de memoria.
6. Empaquetado y devolución por SSH; huellas verificadas en el receptor.

El proveedor no acreditó la identidad exacta del modelo subyacente. TeachAnything devolvió un error y se registró como tal. Este resultado corresponde a una tarea puntual; no demuestra que todos los recursos candidatos estén integrados o que exista una flota autónoma permanente.

Evidencia: [repositorio del piloto](https://github.com/davvidmh/java-one-way-hash-demo), [código](https://github.com/davvidmh/java-one-way-hash-demo/blob/main/OneWayHash.java), [recibo del adaptador](https://github.com/davvidmh/java-one-way-hash-demo/blob/main/evidence/LLM7-receipt.json), [comprobaciones](https://github.com/davvidmh/java-one-way-hash-demo/blob/main/evidence/validation.json) y [transferencia](https://github.com/davvidmh/java-one-way-hash-demo/blob/main/evidence/transfer.json).

## Hashing, privacidad y límites

La pregunta sobre una transformación no inyectiva permitió precisar la diferencia entre un resumen y cifrado recuperable. Que existan colisiones no demuestra por sí solo resistencia computacional; una entrada corta puede reconocerse comparando candidatos. El verificador identifica `hola` dentro de una lista pequeña sin descifrar ni romper SHA-256.

Ese ejemplo no cifra archivos privados ni protege contraseñas. Los paquetes recuperables necesitan cifrado autenticado y custodia de claves. Una pasarela local hacia modelos externos tampoco convierte en local el procesamiento de esos proveedores.

Las nuevas devoluciones siguen una política distinta del piloto público: el coordinador conversacional no abre su contenido; su revisión corresponde al destinatario o a un ejecutor privado autorizado. Una comprobación posterior generó datos aleatorios en memoria en Oracle, los cifró con age para la clave pública del destinatario y verificó la huella del archivo cifrado tras transferirlo. No se publicó ni descifró ese contenido. El descifrado de comprobación por el destinatario y la integración general siguen pendientes.

Los requisitos físicos ausentes se mantienen como bloqueos y las ideas de investigación opcionales no desplazan el trabajo de infraestructura pendiente.

## Próximos pasos

Completar roles y permisos por worker, verificar devolución cifrada, automatizar la admisión de peticiones concretas y comprobar recuperación ante desconexión. Los criterios y pruebas completadas se publican por separado de las conversaciones y de los proyectos privados.

[Procedimiento general](README.md) · [Guía SSH](https://github.com/davvidmh/oracle-ssh-recovery-guide) · [Piloto Java](https://github.com/davvidmh/java-one-way-hash-demo)
