# NCurses Disk Usage

## ¿Qué es ncdu?

**ncdu** (NCurses Disk Usage) es compartido por **ncaravac** para piscineros y estudiantes de 42. Analizador de uso de disco para sistemas Linux y Unix que proporciona una interfaz de usuario basada en texto (TUI - Text User Interface) construida con la biblioteca ncurses. Es una alternativa moderna y más eficiente al comando tradicional `du` de Unix.

### Características principales:

- **Interfaz interactiva**: Navegación fácil con el teclado a través de directorios
- **Visualización clara**: Muestra el tamaño de archivos y directorios ordenados por tamaño
- **Eficiente**: Escanea rápidamente el sistema de archivos y cachea los resultados
- **Operaciones de archivo**: Permite eliminar archivos y directorios directamente desde la interfaz
- **Multiplataforma**: Funciona en Linux, BSD, macOS y otros sistemas Unix

## Instalación

ncdu es un binario. Descárgalo con total tranquilidad. Guárdalo en la raíz. 

## Instrucciones de ejecución

### Uso básico:

```bash
# Analizar el directorio actual
ncdu
```

### Opciones comunes:

```bash
# Modo de solo lectura (no permite borrar archivos)
ncdu -r /ruta/directorio

# Excluir directorios específicos
ncdu -x /tmp -x /var/log /

# Exportar resultado a un archivo
ncdu -o resultado.ncdu /home

# Importar y visualizar resultado previamente guardado
ncdu -f resultado.ncdu

# Seguir enlaces simbólicos
ncdu -L /ruta/directorio

# Mostrar porcentajes y gráficos
ncdu --color dark /ruta/directorio
```

## Navegación en la interfaz

Una vez dentro de ncdu, puedes usar las siguientes teclas:

- **↑/↓** o **k/j**: Navegar hacia arriba/abajo
- **Enter**: Entrar a un directorio
- **←** o **h**: Volver al directorio padre
- **d**: Eliminar archivo o directorio seleccionado
- **t**: Ordenar por nombre
- **s**: Ordenar por tamaño
- **c**: Ordenar por cantidad de items
- **a**: Alternar entre mostrar tamaño aparente y uso real en disco
- **g**: Mostrar/ocultar porcentajes y gráficos
- **i**: Mostrar información del item seleccionado
- **r**: Refrescar el directorio actual
- **q**: Salir de ncdu
- **?**: Mostrar ayuda

## Ejemplos prácticos

### Ejemplo 1: Analizar el directorio home

```bash
$ ncdu ~
```

**Salida esperada:**
```
ncdu 1.17 ~ Use the arrow keys to navigate, press ? for help
--- /home/usuario ---------------------------------
  148.2 GiB [##########] /Documentos
   89.4 GiB [######    ] /Descargas
   45.7 GiB [###       ] /Videos
   23.1 GiB [#         ] /.cache
   12.8 GiB [          ] /Imágenes
    8.9 GiB [          ] /.local
    2.3 GiB [          ] /Música
    1.1 GiB [          ] /.config
  524.0 MiB [          ] /.mozilla
  Total disk usage: 331.6 GiB  Apparent size: 328.4 GiB  Items: 245891
```

## Conclusión

ncdu es una herramienta esencial para administradores de sistemas y usuarios que necesitan gestionar el espacio en disco de manera eficiente. Su interfaz interactiva hace que sea mucho más fácil y rápido identificar y eliminar archivos grandes comparado con comandos tradicionales como `du` y `df`.

Para más información, consulta:
- Página oficial: https://dev.yorhel.nl/ncdu
- Manual: `man ncdu`
- Ayuda interactiva: Ejecuta `ncdu` y presiona `?`

## Contribuciones

Este README es un recurso educativo sobre ncdu. Para contribuir al proyecto ncdu oficial, visita:
- Repositorio oficial: https://dev.yorhel.nl/ncdu
- Código fuente: https://g.blicky.net/ncdu.git/