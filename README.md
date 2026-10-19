# OCI Workarounds · Orquestación por consola

Documentación pública general de un sistema que coordina trabajos de inteligencia artificial desde un servidor, mediante consola y SSH. No contiene configuración privada, conversaciones, credenciales o datos internos de los proyectos.

[OCI Workarounds](OCI_WORKAROUNDS.md): notas de infraestructura, decisiones de arquitectura y pruebas del recorrido remoto.

## Jerarquía

El usuario define objetivos y permisos. El coordinador principal interpreta el encargo durante sus sesiones. Las herramientas de orquestación administran cola y estado. Los workers tienen roles y entregas concretas. Las herramientas específicas se incorporan cuando una tarea real las justifica.

Una biblioteca de habilidades no sustituye a los modelos ni al ejecutor: roles e instrucciones pueden adaptarse, mientras los permisos y las comprobaciones deben existir como mecanismos efectivos.

## Procedimiento de trabajo

1. Formular una petición concreta con alcance, entregables, pruebas y límites.
2. Revisarla antes de autorizar el envío; modificarla invalida la revisión anterior.
3. Ejecutar en el servidor con herramientas de consola y proveedores autorizados para ese contenido.
4. Ejecutar pruebas en el entorno autorizado y conservar evidencia real. Los errores se conservan como errores. La revisión de contenido de nuevas devoluciones corresponde al destinatario o a su ejecutor privado, no al coordinador conversacional.
5. Devolver un paquete compacto cifrado por SSH al proyecto correcto; el coordinador comprueba únicamente sus metadatos externos e integridad. La recepción ciega de una respuesta real ya fue comprobada; el destinatario también confirmó personalmente el descifrado de una prueba aleatoria.

## Primer experimento público

[Java: resumen de una cadena y entrega comprobada desde Oracle](https://github.com/davvidmh/java-one-way-hash-demo).

La prueba usa una tarea pública con la palabra `hola`. GPT4Free, ejecutado en Oracle, obtuvo código mediante LLM7; el programa se compiló y pasó seis casos en el servidor, y regresó por SSH con integridad verificada. El repositorio enlazado conserva código, recibos y limitaciones. No se afirma una identidad de modelo subyacente que el proveedor no acreditó.

La base actual añade servicios persistentes, una cuenta de ejecución separada sin administración, roles adaptados de ECC, revisión ligada a la huella de cada solicitud y envíos idempotentes. El recorrido completo de planificación, elaboración y revisión pasó con IA real, directamente y mediante una salida VPN por aplicación; ambos paquetes regresaron cifrados sin abrirse. Los proveedores gratuitos pueden agotar cuota: sus fallos se conservan y los reintentos tienen límites. Esto demuestra el recorrido, no la calidad semántica de contenidos que permanecen ocultos al coordinador.

La política posterior para nuevas devoluciones exige paquetes cifrados para el destinatario y recepción sin lectura de contenido por el coordinador conversacional. El destinatario custodia la clave privada. Este experimento público anterior se revisó antes de esa política; no autoriza publicar ni inspeccionar futuras devoluciones.

## Principios de privacidad

Las nuevas entregas incorporan una auditoría interna de cada entregable y criterio de aceptación. Si faltan elementos, el constructor recibe correcciones y vuelve a consolidar el trabajo, con rondas limitadas por el presupuesto autorizado. La instrucción exige explorar alternativas ante dificultades, conservar el objetivo y no inventar evidencia. Agotar límites o carecer de una capacidad requerida produce una entrega marcada como incompleta. Una revisión favorable del modelo no equivale a pruebas ejecutadas ni garantiza corrección total; la recepción del cifrado y la aceptación del trabajo son estados distintos. Las devoluciones anteriores no reciben aprobación retroactiva.

Un servicio local de acceso a modelos no vuelve local el procesamiento de sus proveedores remotos. Los contenidos privados requieren destinos expresamente permitidos, y los que deban permanecer desconocidos para un proveedor no se envían a él. La conexión SSH protege el transporte; la protección en reposo y durante el procesamiento necesita controles adicionales.

La documentación pública se redacta por separado de los repositorios privados; no se publican sus historiales. Cada herramienta candidata se evalúa antes de incorporarse, sin instalar recursos únicamente por estar disponibles.

Al apagar el equipo local, el servidor conserva las tareas y los paquetes cifrados. Un receptor sin interfaz puede sincronizarlos al iniciar sesión, sin aprobar trabajo, ejecutar modelos localmente ni descifrar devoluciones. Los adjuntos privados no se envían a estos proveedores; el ejecutor actual trabaja con contexto público o sintético.
