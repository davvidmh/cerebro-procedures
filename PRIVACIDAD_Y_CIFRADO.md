# Cifrado y recepción privada

La privacidad de las devoluciones es una decisión central del diseño: el coordinador puede organizar el trabajo y comprobar su llegada sin leer el resultado.

## Procedimiento

1. El destinatario genera su identidad age y conserva la clave privada protegida con contraseña. Oracle recibe únicamente la clave pública.
2. El worker comprime el resultado y sus dictámenes en memoria y los cifra con age antes de escribirlos en disco.
3. El archivo cifrado viaja por SSH. Un recibo externo identifica tarea, destino, tamaño y SHA-256 del cifrado.
4. El receptor persistente comprueba integridad y guarda el paquete en el proyecto correspondiente. Se reconecta tras fallos y evita instancias duplicadas. El destinatario lo descifra y decide su aceptación personalmente.

La VPN se utiliza para peticiones a los modelos de IA. El transporte de archivos usa SSH; age protege su contenido en reposo. El cifrado no oculta a un proveedor el contexto que se le envía para procesarlo.

## Evidencia registrada

- Prueba aleatoria cifrada en el servidor: el destinatario confirmó personalmente la huella tras descifrarla.
- Flujos sintéticos con IA real: devoluciones comprimidas y cifradas recibidas con huellas coincidentes, sin apertura por el coordinador.
- Verificación puntual de contenido: el propietario autorizó excepcionalmente revisar una devolución ya descifrada. El ZIP coincidió con el archivo extraído y el entregable cumplió todos los criterios de su solicitud sintética. Las demás devoluciones conservaron la regla de no apertura.
- Respaldo consistente cifrado: el 19 de octubre de 2026 se comprobaron 19 archivos recuperados contra el TAR y la integridad de SQLite, mediante una excepción puntual autorizada por el propietario. Las cinco devoluciones incluidas permanecieron cifradas.

Esta última comprobación acredita recuperación de archivos y base de datos; el arranque de un servidor restaurado es una prueba distinta. La excepción no habilita futuras lecturas. Claves, rutas reales, configuración y contenido privado permanecen fuera de este repositorio.

[Proyecto](README.md) · [Formato age](https://github.com/FiloSottile/age)

El router FreeLLMAPI mantiene su base de solicitudes y registros en RAM, con caché de respuestas deshabilitada. Solo se habilitan rutas de inferencia cuyo acceso gratuito se haya verificado. Una prueba completa remota ya produjo una entrega cifrada con revisión interna aprobada.
