# OCI Workarounds

Colmena de IA en Oracle: operación por consola, tareas revisadas y entregas cifradas para proyectos locales. Diseño y dirección: [David](https://github.com/davvidmh), con implementación asistida por IA.

**Flujo:** petición concreta → revisión → planificación → elaboración → auditoría interna y correcciones → devolución cifrada por SSH → aceptación privada del destinatario.

- Servicios persistentes, cola única y roles adaptados de ECC.
- Inferencia mediante g4f en el servidor; herramientas específicas solo cuando una tarea las justifica.
- Solicitudes ligadas a su huella; repetir un envío no duplica trabajo.
- Resultados comprimidos y cifrados con age. El coordinador comprueba metadatos y no abre las devoluciones.
- La auditoría exige evidencia por criterio. Un avance incompleto conserva ese estado.

**Comprobado:** piloto Java, flujos sintéticos con IA real, transferencia cifrada, recorrido mediante VPN y corrección iterativa probada con casos sintéticos. No demuestra ejecución autónoma de cualquier proyecto.

**Límites:** el ejecutor actual entrega texto/workflows, sin ejecutar comandos generados. Cuota gratuita no significa disponibilidad continua. El respaldo cifrado y la aceptación de resultados requieren comprobación privada del destinatario.

[Decisiones técnicas](OCI_WORKAROUNDS.md) · [Recuperación SSH](https://github.com/davvidmh/oracle-ssh-recovery-guide) · [Piloto Java](https://github.com/davvidmh/java-one-way-hash-demo)
