# Cerebro: procedimientos de orquestación

Documentación pública general de un sistema que coordina trabajos de inteligencia artificial desde un servidor, mediante consola y SSH. No contiene configuración privada, conversaciones, credenciales o datos internos de los proyectos.

**Para evaluación técnica y reclutamiento:** [caso técnico de David (@davvidmh)](CASO_TECNICO.md), con decisiones de arquitectura, contribución del responsable, implementación asistida, evidencia pública y límites de lo completado.

## Jerarquía

El usuario define objetivos y permisos. El coordinador principal interpreta el encargo durante sus sesiones. Las herramientas de orquestación administran cola y estado. Los workers tienen roles y entregas concretas. Las herramientas específicas se incorporan cuando una tarea real las justifica.

Una biblioteca de habilidades no sustituye a los modelos ni al ejecutor: roles e instrucciones pueden adaptarse, mientras los permisos y las comprobaciones deben existir como mecanismos efectivos.

## Procedimiento de trabajo

1. Formular una petición concreta con alcance, entregables, pruebas y límites.
2. Revisarla antes de autorizar el envío; modificarla invalida la revisión anterior.
3. Ejecutar en el servidor con herramientas de consola y proveedores autorizados para ese contenido.
4. Ejecutar pruebas en el entorno autorizado y conservar evidencia real. Los errores se conservan como errores. La revisión de contenido de nuevas devoluciones corresponde al destinatario o a su ejecutor privado, no al coordinador conversacional.
5. Devolver un paquete compacto cifrado por SSH al proyecto correcto; el coordinador comprueba únicamente sus metadatos externos e integridad. Ese flujo cifrado sigue pendiente de verificación.

## Primer experimento público

[Java: resumen de una cadena y entrega comprobada desde Oracle](https://github.com/davvidmh/java-one-way-hash-demo).

La prueba usa una tarea pública con la palabra `hola`. GPT4Free, ejecutado en Oracle, obtuvo código mediante LLM7; el programa se compiló y pasó seis casos en el servidor, y regresó por SSH con integridad verificada. El repositorio enlazado conserva código, recibos y limitaciones. No se afirma una identidad de modelo subyacente que el proveedor no acreditó.

Esto demuestra un recorrido técnico acotado, no una plataforma autónoma completa. Quedan pendientes autorizaciones restringidas por worker, cifrado de paquetes privados con claves separadas y validación de más workflows.

La política posterior para nuevas devoluciones exige paquetes cifrados para el destinatario y recepción sin lectura de contenido por el coordinador conversacional. El destinatario custodia la clave privada. Este experimento público anterior se revisó antes de esa política; no autoriza publicar ni inspeccionar futuras devoluciones.

## Principios de privacidad

Un servicio local de acceso a modelos no vuelve local el procesamiento de sus proveedores remotos. Los contenidos privados requieren destinos expresamente permitidos, y los que deban permanecer desconocidos para un proveedor no se envían a él. La conexión SSH protege el transporte; la protección en reposo y durante el procesamiento necesita controles adicionales.

La documentación pública se redacta por separado de los repositorios privados; no se publican sus historiales. Cada herramienta candidata se evalúa antes de incorporarse, sin instalar recursos únicamente por estar disponibles.
