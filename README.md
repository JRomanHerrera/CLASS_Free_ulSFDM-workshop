<p align="center">
  <img src="figures/portada_taller.png" width="900">
</p>

# CLASS_Free_ulSFDM-workshop
This repository contains the notebooks and installation instructions used during the CLASS-ulSFDM workshop.  The CLASS source code is hosted in a separate repository:  https://github.com/JRomanHerrera/class_public_ulSFDM
# Taller: Cosmología con CLASS-ulSFDM

Bienvenido al repositorio del taller **Cosmología con CLASS-ulSFDM**.

Este repositorio contiene los **notebooks de Jupyter**, el ambiente de Python y las instrucciones necesarias para instalar y utilizar la versión modificada del código **CLASS-ulSFDM**, la cual implementa un modelo de **Materia Oscura Escalar Ultraligera Libre (free ultralight Scalar Field Dark Matter, ulSFDM)**.

El código fuente de CLASS-ulSFDM se encuentra en un repositorio independiente:

> https://github.com/JRomanHerrera/class_publicSFDM

---

# Requisitos

Antes de comenzar necesitarás:

- Una conexión a Internet.
- Git.
- Miniconda.
- Un compilador de C/C++.
- Jupyter Notebook o JupyterLab (se instalará automáticamente con el ambiente).

El procedimiento funciona en:

- macOS
- Linux
- Windows (mediante WSL2)

---

# 1. Instalar Miniconda

Si aún no tienes instalado Miniconda, descárgalo desde

https://www.anaconda.com/download

Sigue las instrucciones correspondientes a tu sistema operativo.

Una vez instalado, verifica que Conda funciona correctamente:

```bash
conda --version
```

---

# 2. Crear el ambiente de Python

Desde la carpeta de este repositorio ejecuta

```bash
conda env create -f environment.yml
```

Una vez finalizada la instalación activa el ambiente

```bash
conda activate class-ulsfdm
```

Verifica que Python corresponde al ambiente recién creado

```bash
python --version
```

La salida debe ser similar a:

```text
Python 3.11.x
```

También puedes comprobar que se está utilizando el Python del ambiente de Conda:

```bash
which python
```

La salida debe ser similar a:

```text
.../miniconda3/envs/class-ulsfdm/bin/python
```

Si ambas comprobaciones son correctas, puedes continuar con la descarga de **CLASS-ulSFDM**.

---

# 3. Descargar CLASS-ulSFDM

Clona el repositorio del código fuente:

```bash
git clone https://github.com/JRomanHerrera/class_publicSFDM.git
```

Entra al directorio:

```bash
cd class_publicSFDM
```

---
# 4. Configurar el Makefile

Antes de compilar CLASS-ulSFDM, verifica qué compiladores de C y C++ están disponibles en tu sistema.

## macOS

Comprueba las versiones de `clang` y `clang++`:

```bash
clang --version
clang++ --version
```

Si ambos comandos muestran correctamente la información de los compiladores, abre el archivo `Makefile`. Localiza las líneas correspondientes a los compiladores:

```make
# your C compiler:
CC       = clang
#CC       = icc
#CC       = pgcc

CPP      = clang++ --std=c++11 -fpermissive -Wno-write-strings
```

Verifica que queden exactamente de esta forma:

```make
CC       = clang
CPP      = clang++ --std=c++11 -fpermissive -Wno-write-strings
```

Guarda los cambios y cierra el editor.

---

## Linux / Windows (WSL2)

Comprueba las versiones de `gcc` y `g++`:

```bash
gcc --version
g++ --version
```

Si ambos comandos muestran correctamente la información de los compiladores, abre el archivo `Makefile`. Localiza las líneas correspondientes a los compiladores y modifícalas para que queden así:

```make
CC       = gcc
CPP      = g++ --std=c++11 -fpermissive -Wno-write-strings
```

Guarda los cambios y cierra el editor.

Una vez configurado el `Makefile`, puedes continuar con la compilación de CLASS-ulSFDM.

---
# 5. Compilar CLASS

```bash
make clean
make 
```

Al finalizar deberá generarse correctamente la biblioteca de CLASS y el módulo de Python `classy`.

---

# 6. Verificar la instalación

Ejecute el archivo de ejemplo incluido en el repositorio:

```bash
./class sfdm.ini
```

Si la instalación fue correcta, CLASS calculará la evolución cosmológica sin mostrar errores.

También puedes verificar que el módulo de Python `classy` fue compilado correctamente ejecutando:

```bash
find python/build -maxdepth 1 -type d -name "lib.*"
```

La salida debe ser similar a:

```text
python/build/lib.macosx-15.0-arm64-cpython-311
```

o

```text
python/build/lib.linux-x86_64-cpython-311
```

dependiendo del sistema operativo.

Nota: No es necesario, pero puedes comprobar que Python encuentra correctamente el módulo `classy`

```bash
python -c "from classy import Class; print('CLASS instalado correctamente.')"
```

---

# 7. Iniciar Jupyter

Regrese a la carpeta del taller y ejecute

```bash
jupyter lab
```

o bien

```bash
jupyter notebook
```

Se abrirá automáticamente el navegador.

---

# 8. Abrir los notebooks

Dentro de Jupyter abra la carpeta

```
notebooks/
```

Los notebooks están organizados para seguir el mismo orden del taller.

Se recomienda ejecutarlos secuencialmente.

---

# Contenido del taller

Los notebooks están organizados para introducir progresivamente el uso de **CLASS-ulSFDM**, desde la instalación y las primeras simulaciones hasta el cálculo de observables cosmológicos.

El contenido incluye:

## Introducción

- Introducción a CLASS y `classy`.
- Primera simulación con ΛCDM.
- Primeras gráficas cosmológicas.

## Modelo ulSFDM

- Estructura del archivo `sfdm.ini`.
- Evolución del fondo cosmológico.
- Condiciones iniciales.
- Evolución de perturbaciones lineales.

## Observables cosmológicos

- Espectro de potencia de materia.
- Anisotropías del CMB.
- Comparación entre ΛCDM y ulSFDM.

---

# Referencias

La implementación de **free ulSFDM** utilizada en este taller está basada en una versión modificada del código **CLASS (Cosmic Linear Anisotropy Solving System)**.

Si utiliza este código en trabajos de investigación, por favor cite tanto CLASS como la publicación asociada a esta implementación.

Repositorio de CLASS

https://github.com/lesgourg/class_public

Repositorio de CLASS-ulSFDM

https://github.com/JRomanHerrera/class_publicSFDM

Repositorio del taller

https://github.com/JRomanHerrera/class_public_ulSFDM-workshop
