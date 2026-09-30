# Skills

Colección de skills para opencode

## security-audit

### Contenido

- **`security-audit`** — puerta de auditoría de seguridad final. Se invoca al final de una funcionalidad o de un cambio importante, antes de cerrarlo.

  - Revisión **estática** y agnóstica del stack (base: OWASP ASVS/Top 10 + CCN-STIC-140 Anexo F.1).
  - Recorre el código en ámbito por las áreas A-M (autenticación, autorización, inyección, XSS, CSRF, TLS, criptografía, datos sensibles, registro, configuración, dependencias, integridad, manejo de errores).
  - Produce un informe en markdown con los hallazgos agrupados por severidad (Crítica, Alta, Media, Baja) y un veredicto: `APPROVED`, `WITH OBSERVATIONS` o `REJECTED`.
  - **No modifica el código**: solo reporta hallazgos y propone remediaciones.

### Cómo usarla

La skill acepta un argumento opcional:

- Ruta de directorio: audita solo ese árbol.
- Ruta de archivo: audita solo ese archivo.
- Sin argumento: audita todo el repositorio (o todo el proyecto si no hay git).

Ejemplos de invocación (desde la sesión de opencode):

- `security-audit` — audita todo el repositorio.
- `security-audit <ruta/subárbol>` — solo ese subárbol, p. ej. una carpeta `src/`.
- `security-audit <ruta/archivo>` — solo ese archivo, p. ej. un manifiesto `package.json`.

Siempre dentro del workspace: las rutas que escapen (`..`, rutas absolutas externas, symlinks) se rechazan.

Ejemplo de salida (veredicto):

```
## Verdict
- REJECTED: there is at least one Critical or High finding.
- WITH OBSERVATIONS: no Critical or High, but there is at least one Medium or Low.
- APPROVED: there are no findings at any severity.
```
