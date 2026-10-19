# OCI Workarounds

Notas de infraestructura y decisiones de diseño para coordinar tareas desde Oracle Cloud Infrastructure y devolver entregables a proyectos locales. Diseño y dirección: [David (@davvidmh)](https://github.com/davvidmh). Implementación asistida por inteligencia artificial.

## Del acceso al servidor a un flujo de trabajo

El punto de partida fue aprovechar recursos de coste contenido y conservar acceso a la máquina. El diseño evolucionó hacia una cola de tareas, ejecutores especializados y entregas compactas. Los servicios se administran por consola; los archivos viajan por SSH. Los datos y la configuración reales quedan fuera de esta documentación pública.

| Problema | Decisión de diseño | Resultado o estado |
|---|---|---|
| Continuidad del acceso tras perder una clave local | Recuperar el acceso conservando la verificación de identidad y retirar permisos temporales | [Procedimiento público de recuperación SSH](https://github.com/davvidmh/oracle-ssh-recovery-guide). |
| Muchos recursos disponibles y una máquina limitada | Evaluar todos los candidatos y desplegar solo los que resuelven una necesidad vigente | Las referencias sin demanda, por ejemplo una aplicación contable de otro proyecto, quedan fuera del servidor. |
| Repartir trabajo entre varios ejecutores | Separar dirección, herramientas de orquestación y funciones específicas | Servicios persistentes y roles adaptados de ECC; el recorrido de tres etapas con inferencia real regresó cifrado. |
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

Las nuevas devoluciones siguen una política distinta del piloto público: el coordinador conversacional no abre su contenido; su revisión corresponde al destinatario o a un ejecutor privado autorizado. Una comprobación posterior generó datos aleatorios en memoria en Oracle, los cifró con age y verificó la huella del archivo cifrado tras transferirlo. El destinatario confirmó personalmente la huella del descifrado; el coordinador no accedió a su identidad privada. También regresó una respuesta real de IA cifrada, cuya recepción se comprobó solo por metadatos.

Los requisitos físicos ausentes se mantienen como bloqueos y las ideas de investigación opcionales no desplazan el trabajo de infraestructura pendiente.

## Validación operativa

La recepción usa destinos registrados y rechaza recorridos fuera de ellos. Modificar una solicitud invalida la revisión anterior; repetir su envío no duplica trabajo. El ejecutor tiene una cuenta distinta del coordinador, sin poder leer su base ni invocar acciones administrativas. Los roles comparten esa cuenta: no se presenta como aislamiento de seguridad entre ellos.

El paquete se comprime en memoria y se cifra antes de guardarse. Primero se comprobó el empaquetado sin modelos; después pasó el recorrido real de tres etapas por un adaptador web alternativo de g4f, tras registrar el límite de otro proveedor. Una segunda prueba completa pasó por una salida WARP por aplicación. Ambas llegaron cifradas con la huella correcta, sin revisión de contenido por el coordinador. Se conservaron respaldos cifrados consistentes y recepción al reiniciar el equipo local; no se presenta como probada una restauración que requiera la clave privada del destinatario.

La VPN se limita al proxy local y conserva la conexión de administración. El ejecutor distingue fallos de conectividad y cuotas: utiliza solo intermediarios/proveedores aprobados y aplica espera ante límites de uso. Los proveedores tienen bloqueos independientes para permitir concurrencia sin mezclar sesiones. No se promete capacidad ilimitada ni se atribuye un modelo concreto sin evidencia del origen.

La implementación actual entrega workflows y texto con contexto expresamente permitido. No ejecuta comandos generados, no recoge archivos privados automáticamente ni aplica resultados. Las herramientas específicas siguen necesitando una petición real. La memoria de disponibilidad de proveedores no equivale a reentrenar modelos ni a aprender contenido que permanece cifrado.

Referencias técnicas: [ECC](https://github.com/affaan-m/ECC), [GPT4Free](https://github.com/xtekky/gpt4free), [age](https://github.com/FiloSottile/age). Los criterios y pruebas completadas se publican por separado de las conversaciones y de los proyectos privados.

[Procedimiento general](README.md) · [Guía SSH](https://github.com/davvidmh/oracle-ssh-recovery-guide) · [Piloto Java](https://github.com/davvidmh/java-one-way-hash-demo)
