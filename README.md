# OCI Workarounds

Colmena de IA en Oracle: operación por consola, tareas revisadas y entregas cifradas para proyectos locales. Diseño y dirección: [David](https://github.com/davvidmh), con implementación asistida por IA.

**Flujo:** petición concreta → revisión → planificación → elaboración → auditoría interna y correcciones → devolución cifrada por SSH → aceptación privada del destinatario.

- Servicios persistentes, cola única y roles adaptados de ECC.
- Inferencia mediante g4f y FreeLLMAPI en el servidor; herramientas específicas solo cuando una tarea las justifica.
- Solicitudes ligadas a su huella; repetir un envío no duplica trabajo.
- Resultados comprimidos y cifrados con age. El coordinador comprueba metadatos y no abre las devoluciones.
- La auditoría exige evidencia por criterio. Un avance incompleto conserva ese estado.

**Autonomía:** el diseño persigue una colmena completamente autónoma: una vez autorizada una tarea concreta, debe planificar, elaborar, revisar, corregir y devolver el trabajo sin operación manual del servidor.

**Comprobado:** prueba completa con FreeLLMAPI, revisión interna y recepción cifrada sin apertura; piloto Java, flujos sintéticos con IA real, transferencia cifrada por SSH y corrección iterativa. También se comprobaron peticiones a los modelos mediante una salida VPN por aplicación.

**Conexiones:** la VPN se destina al acceso a los proveedores de IA y la continuidad de las peticiones. Los archivos se transfieren por SSH; la VPN no forma parte de ese transporte.

[Cifrado privado y evidencia](PRIVACIDAD_Y_CIFRADO.md) · [Decisiones técnicas](OCI_WORKAROUNDS.md) · [Recuperación SSH](https://github.com/davvidmh/oracle-ssh-recovery-guide) · [Piloto Java](https://github.com/davvidmh/java-one-way-hash-demo)
