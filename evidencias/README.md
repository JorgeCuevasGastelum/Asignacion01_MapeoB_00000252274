# Evidencia del modelo relacional

Estado: pendiente de conexión a MySQL y captura real de Workbench.

1. Configurar el archivo local .env y ejecutar npm run migrate:deploy.
2. Abrir MySQL Workbench y conectarse al servidor local.
3. Seleccionar Database > Reverse Engineer.
4. Seleccionar la base asignacion01_restaurante_00000252274 y continuar con las tablas del dominio.
5. Completar el asistente y ordenar las cuatro tablas para que se vean columnas y relaciones.
6. Guardar una captura legible del diagrama EER en esta carpeta como modelo-relacional.png.
7. Guardar opcionalmente el modelo como modelo-relacional.mwb.
8. Agregar la evidencia a Git y subirla al repositorio público.

La tabla _prisma_migrations es de control de Prisma y puede omitirse del diagrama del dominio. Una imagen dibujada manualmente no sustituye la captura solicitada.