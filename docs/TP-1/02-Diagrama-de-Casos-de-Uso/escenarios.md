# Especificación de Escenarios de Casos de Uso (Punto 2)

---

## 📋 Escenario 1: Crear Archivo

- **Caso de Uso:** Crear Archivo
- **Actor Principal:** Usuario
- **Actores Secundarios:** Sistema Operativo
- **Descripción:** Permite al usuario crear y almacenar un nuevo archivo en el sistema dentro de una categoría específica (*imágenes, documentos, videos, audios*).
- **Precondiciones:** 
  1. El sistema se encuentra activo y disponible.
  2. El usuario está autenticado en la sesión.

### Flujo Principal (Camino Feliz)
1. El **Usuario** solicita la opción de crear un nuevo archivo especificando nombre, tipo/categoría y contenido/tamaño.
2. El **Sistema** invoca la verificación de espacio disponible en disco (`«include» Verificar Espacio en Disco`).
3. El **Sistema Operativo** confirma que existe espacio suficiente en el disco.
4. El **Sistema** crea el registro del archivo asignando la fecha de creación actual y estado inicial `visible`.
5. El **Sistema** clasifica y ubica el archivo en la jerarquía correspondiente según su tipo.
6. El **Sistema** muestra una confirmación de creación exitosa al usuario.

### Postcondiciones
- El archivo queda registrado en el sistema con su nombre, fecha, tamaño y estado `visible`.

### Flujos Alternativos

#### A1: Espacio Insuficiente en Disco
- **Paso 3 del flujo principal:** El **Sistema Operativo** detecta que el espacio disponible en disco es inferior al tamaño del archivo a crear.
- **Acción:** Se ejecuta el caso de uso extendido (`«extend» Notificar Falta de Espacio`).
- **Resultado:** El **Sistema** interrumpe la creación y despliega un aviso de alerta informando la falta de espacio disponible.

#### A2: Nombre de Archivo Duplicado en el mismo directorio
- **Paso 4 del flujo principal:** El **Sistema** detecta que ya existe un archivo con el mismo nombre y tipo en la misma ubicación.
- **Acción:** El sistema solicita al usuario renombrar el archivo o reemplazar el existente.

---

## 📋 Escenario 2: Eliminar Archivo

- **Caso de Uso:** Eliminar Archivo
- **Actor Principal:** Usuario
- **Actores Secundarios:** Ninguno
- **Descripción:** Permite al usuario remover un archivo existente del sistema de archivos.
- **Precondiciones:**
  1. El archivo a eliminar existe en el sistema.
  2. El archivo se encuentra en estado `visible` u `oculto`.

### Flujo Principal (Camino Feliz)
1. El **Usuario** selecciona un archivo y solicita la acción de eliminación.
2. El **Sistema** solicita la confirmación de la acción de baja al usuario.
3. El **Usuario** confirma la eliminación.
4. El **Sistema** procesa la baja del archivo retirándolo de la estructura jerárquica activa.
5. El **Sistema** ejecuta automáticamente la actualización del historial de eliminados (`«include» Actualizar Historial de Eliminados`).
6. El **Sistema** confirma la eliminación exitosa al usuario.

### Postcondiciones
- El archivo es removido de la lista de archivos activos.
- El historial de eliminados se actualiza registrando el nombre del archivo, fecha de baja y tamaño.

### Flujos Alternativos

#### A1: Cancelación por parte del Usuario
- **Paso 3 del flujo principal:** El **Usuario** cancela la confirmación de eliminación.
- **Acción:** El **Sistema** cancela el proceso y el archivo permanece inalterado en su ubicación original.
