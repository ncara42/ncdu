# ncdu - NCurses Disk Usage

## ¿Qué es ncdu?

**ncdu** (NCurses Disk Usage) es un analizador de uso de disco para sistemas Linux y Unix que proporciona una interfaz de usuario basada en texto (TUI - Text User Interface) construida con la biblioteca ncurses. Es una alternativa moderna y más eficiente al comando tradicional `du` de Unix.

### Características principales:

- **Interfaz interactiva**: Navegación fácil con el teclado a través de directorios
- **Visualización clara**: Muestra el tamaño de archivos y directorios ordenados por tamaño
- **Eficiente**: Escanea rápidamente el sistema de archivos y cachea los resultados
- **Operaciones de archivo**: Permite eliminar archivos y directorios directamente desde la interfaz
- **Multiplataforma**: Funciona en Linux, BSD, macOS y otros sistemas Unix

## Instalación

### En Ubuntu/Debian:
```bash
sudo apt-get update
sudo apt-get install ncdu
```

### En Fedora/RHEL/CentOS:
```bash
sudo dnf install ncdu
# o en versiones antiguas:
sudo yum install ncdu
```

### En Arch Linux:
```bash
sudo pacman -S ncdu
```

### En macOS (usando Homebrew):
```bash
brew install ncdu
```

### Desde el código fuente:
```bash
git clone https://dev.yorhel.nl/ncdu
cd ncdu
./configure
make
sudo make install
```

## Instrucciones de ejecución

### Uso básico:

```bash
# Analizar el directorio actual
ncdu

# Analizar un directorio específico
ncdu /ruta/al/directorio

# Analizar el directorio home del usuario
ncdu ~

# Analizar la raíz del sistema (requiere permisos)
sudo ncdu /
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

### Ejemplo 2: Encontrar archivos grandes en /var

```bash
$ sudo ncdu /var
```

Navega con las flechas para encontrar qué está consumiendo espacio en /var:
```
ncdu 1.17 ~ Use the arrow keys to navigate, press ? for help
--- /var ------------------------------------------
   45.2 GiB [##########] /log
   23.8 GiB [#####     ] /lib
   12.4 GiB [##        ] /cache
    8.7 GiB [#         ] /tmp
    2.1 GiB [          ] /spool
  Total disk usage: 92.2 GiB  Apparent size: 90.1 GiB  Items: 78234
```

### Ejemplo 3: Comparación con tree

El comando `tree` muestra la estructura jerárquica de directorios:

```bash
$ tree -L 2 -h /home/usuario/proyecto
```

**Salida de tree:**
```
/home/usuario/proyecto
├── [4.0K]  src
│   ├── [2.3K]  main.py
│   ├── [1.8K]  utils.py
│   └── [1.2K]  config.py
├── [4.0K]  tests
│   ├── [3.4K]  test_main.py
│   └── [2.1K]  test_utils.py
├── [4.0K]  docs
│   ├── [ 15K]  README.md
│   └── [8.9K]  CONTRIBUTING.md
├── [ 856]  requirements.txt
└── [1.2K]  setup.py

3 directories, 9 files
```

Mientras que `ncdu` para el mismo directorio mostraría:

```bash
$ ncdu /home/usuario/proyecto
```

**Salida de ncdu:**
```
ncdu 1.17 ~ Use the arrow keys to navigate, press ? for help
--- /home/usuario/proyecto ------------------------
   24.0 KiB [##########] /docs
   16.0 KiB [######    ] /src
    8.0 KiB [###       ] /tests
    2.0 KiB [          ]  setup.py
  856.0   B [          ]  requirements.txt
  Total disk usage: 50.8 KiB  Apparent size: 45.7 KiB  Items: 12
```

### Ejemplo 4: Exportar e importar análisis

```bash
# Exportar análisis de un servidor a un archivo
ssh servidor "ncdu -o- /var/log" > logs-servidor.ncdu

# Visualizar el análisis localmente
ncdu -f logs-servidor.ncdu
```

### Ejemplo 5: Excluir directorios

```bash
# Analizar / excluyendo directorios temporales y montajes
sudo ncdu / -x /tmp -x /proc -x /sys -x /dev -x /run -x /mnt
```

## Diferencias entre ncdu y tree

| Característica | ncdu | tree |
|----------------|------|------|
| **Propósito** | Análisis de uso de disco | Visualización de estructura de directorios |
| **Interfaz** | Interactiva (TUI) | Salida estática |
| **Información** | Tamaños de archivos/directorios | Estructura jerárquica |
| **Navegación** | Navegación interactiva | Solo visualización |
| **Ordenamiento** | Por tamaño, nombre, cantidad | Alfabético o cronológico |
| **Uso típico** | Encontrar archivos grandes | Entender organización de archivos |
| **Operaciones** | Puede eliminar archivos | Solo lectura |

## Casos de uso comunes

### 1. Liberar espacio en disco
```bash
# Encontrar qué está llenando tu disco
sudo ncdu /
# Navega y presiona 'd' para eliminar archivos innecesarios
```

### 2. Analizar logs del sistema
```bash
sudo ncdu /var/log
# Identificar logs que están creciendo demasiado
```

### 3. Limpiar cachés
```bash
ncdu ~/.cache
# Eliminar cachés antiguos de aplicaciones
```

### 4. Auditoría de directorios compartidos
```bash
sudo ncdu /home
# Ver qué usuarios están usando más espacio
```

### 5. Análisis de proyectos de desarrollo
```bash
ncdu ~/proyectos
# Encontrar directorios node_modules, build, etc. que ocupan espacio
```

## Tips y trucos

1. **Guardar análisis frecuentes**: Exporta análisis de directorios grandes para revisarlos después sin re-escanear:
   ```bash
   ncdu -o ~/analisis-sistema.ncdu /
   ```

2. **Análisis remoto**: Analiza servidores remotos sin instalar ncdu en ellos:
   ```bash
   ssh usuario@servidor "du -ab /ruta" | ncdu -f-
   ```

3. **Combinación con otros comandos**: 
   ```bash
   # Encontrar los 10 directorios más grandes
   ncdu -o- / | grep "^[0-9]" | sort -rn | head -10
   ```

4. **Modo batch**: Para scripts, usa `du` con las opciones de ncdu:
   ```bash
   ncdu --exclude /proc --exclude /sys -o resultado.json /
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