# Instalación #

* Descargar e Instalar python3 desde https://www.python.org/downloads/

Revisar si python se instaló como python o python3 para usarse
```python
python -V
```
o
```python
python3 -V
```
Si python no funciona y python3 si, el resto de los comandos que usen python reemplazarlos por python3

* Abrir terminal o cmd y clonar Repositorio
```
git clone https://foretama@bitbucket.org/foretama/identificar_fallos_cortesuprema.git (Bitbucket Pancho)
```

* Ingresar a carpeta de repositorio clonado
```python
cd identificar_fallos_cortesuprema
```

* Crear tu virtual enviroment
```python
python -m venv venv
```
* Activar el virtual enviroment

```python
venv\Scripts\activate
```
* Actualizar pip
```python
python -m pip install --upgrade pip
```
* Instalar los paquetes con pip y requirements.txt
```python
pip install -r requirements.txt
```
* Descargar chromedriver para la version de chrome que tienes y sistema operativo
    * En Chrome Browser ir a: 3 puntos (botón abajo de la X) -> Ayuda -> Información de Google Chrome -> Obtener version
    * https://chromedriver.storage.googleapis.com/index.html -> Descargar chromedriver de acuerdo a la version de tu Chrome y de tu OS.
    * Guardar chromedriver en la carpeta code del repositorio descargado

# Uso #

En la carpeta "code", hay 2 scripts:

* 01_descarga_fallos.py
* 02_filtrar_fallos_cortos

## 01_descarga_fallos

Con el script **01_descarga_fallos** podrás descargar los fallos de un día escogido.

El código hace el siguiente flujo:

* Ingresar a https://oficinajudicialvirtual.pjud.cl/home/index.php#
* Al Apretar "Otros Servicios", escoger "Consulta de Causa"
* Ir a Estado Diario de Tribunales
* En corte Suprema, buscar fecha ingresada
* Calcular cantidad de páginas de la busqueda
* Buscar y guardar rol, año y caratula de cada causa que cumpla con los siguientes criterios:
    * Que en el 'Tipo Recurso' contenga la palabra "(Civil)"
    * Que en el 'Caratulado' no contenga alguna de las siguientes palabras ["ISAPRE", "NUEVA MÁS VIDA", "CONSALUD", "CRUZ BLANCA", "COLMENA GOLDEN CROSS", "VIDA TRES", "BANMEDICA", "MODELO"]
* Ir a consulta unificada
* En busqueda por RIT,
    * Competencia: Corte Suprema
    * Tipo Busqueda: Recurso Corte Suprema
* Por cada causa encontrada en Estado Diario de Tribunales se hará el siguiente procedimiento
    * Ingresar Rol
    * Ingresar Año
    * Apretar buscar
    * Apretar lupa
    * Guardar link de descarga de todos los documentos que tengan:
        * Que la Fecha Tramite del documento sea la misma que la fecha escogida
        * Que el nombre del tramite del documento contenga alguna de las siguientes palabras ["Resolución", "Sentencia"]
* Cerrar chrome
* Por cada causa encontrada se descarga el documento seleccionado

Los fallos descargados son guardados en la carpeta **code\downloads\FECHA\files**, donde FECHA es la fecha escogida. Un ejemplo de ruta sería **code\downloads\17_04_2020\files**

Los archivos se guardarán con nombres con el formato **FECHA&NÚMERO_DE_INGRESO&NÚMERO_DEL_DOCUMENTO&NOMBRE_DE_DOCUMENTO.pdf**, donde FECHA es la fecha escogida, el NÚMERO_DE_INGRESO es el 'rol'-'año' de la causa a descargar, el NÚMERO_DEL_DOCUMENTO es el número del documento dado que puede haber más de 1 documento adjunto a la causa y el NOMBRE_DE_DOCUMENTO es el nombre del tramite del documento. Un ejemplo del nombre de los archivos guardados es **17_04_2020&1567-2020&1&Sentencia.pdf**

Para correr el script:

Abrir terminal en carpeta del repositorios descargado
```python
cd code
python 01_descarga_fallos.py
```

## 02_filtrar_fallos_cortos

Con el script **02_filtrar_fallos_cortos** se busca todos los archivos descargados de la carpeta escogida que tengan igual o mas de **N** páginas, donde **N** es la cantidad de paginas a filtrar ingresada.

Para correr el script:
```python
python 02_filtrar_fallos_cortos.py
```
