---
author: v-demjoh
manager: nitinme
ms.service: cognitive-services
ms.topic: include
ms.date: 05/15/2020
ms.author: v-demjoh
ms.openlocfilehash: 6011bf90d5a97dcc027f8a9a0916c28226c5c354
ms.sourcegitcommit: 16c7fd8fe944ece07b6cf42a9c0e82b057900662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2020
ms.locfileid: "96584586"
---
## <a name="download-and-install"></a>Descargar e instalar

#### <a name="windows-install"></a>[Instalación de Windows](#tab/windowsinstall)

Siga estos pasos para instalar la CLI de Voz en Windows:

1. En Windows, necesita [Microsoft Visual C++ Redistributable para Visual Studio 2019](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) para su plataforma. Durante la primera instalación es posible que deba reiniciar.
2. Descargue el [archivo ZIP](https://aka.ms/speech/spx-zips.zip) de la CLI de Voz y extráigalo.
3. Vaya al directorio en el que extrajo `spx-zips`. Esta carpeta contiene los archivos de programa de la CLI de Voz para varias plataformas. 
4. Extraiga los archivos para su plataforma (`spx-net471` para .NET Framework 4.7 o `spx-netcore-win-x64` para .NET Core 3.0 en una CPU x64). Tenga en cuenta que ejecutará `spx` desde este directorio.

### <a name="run-the-speech-cli"></a>Ejecución de la CLI de Voz

1. Abra el símbolo del sistema o PowerShell y vaya hasta el directorio en el que extrajo la CLI de Voz.  
2. Escriba `spx` para ver los comandos de ayuda de la CLI de Voz.

> [!NOTE]
> PowerShell no comprueba el directorio local al buscar un comando. En PowerShell, cambie el directorio a la ubicación de `spx` y llame a la herramienta escribiendo `.\spx`.
> Si agrega este directorio a su ruta de acceso, PowerShell y el símbolo del sistema de Windows buscarán `spx` en cualquier directorio sin incluir el prefijo `.\`.

### <a name="font-limitations"></a>Limitaciones de fuentes

En Windows, la CLI de Voz solo puede mostrar las fuentes disponibles para el símbolo del sistema en el equipo local.
El [terminal de Windows](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701) admite todas las fuentes que genera de forma interactiva la CLI de Voz.

Si se genera la salida a un archivo, un editor de texto como el Bloc de notas o un explorador Web como Microsoft Edge también pueden mostrar todas las fuentes.

#### <a name="linux-install"></a>[Instalación de Linux](#tab/linuxinstall)

Siga estos pasos para instalar la CLI de Voz en Linux en una CPU x64:

1. Instale [.NET Core 3.0](https://dotnet.microsoft.com/download/dotnet-core/3.0).
2. Descargue el [archivo ZIP](https://aka.ms/speech/spx-zips.zip) de la CLI de Voz y extráigalo.
3. Vaya al directorio raíz `spx-zips` que extrajo de la descarga y extraiga `spx-netcore-30-linux-x64` en un nuevo directorio `~/spx`.
4. En un terminal, escriba estos comandos:
   1. `cd ~/spx`
   2. `sudo chmod +r+x spx`
   3. `PATH=~/spx:$PATH`

Escriba `spx` para ver la ayuda de la CLI de Voz.

#### <a name="docker-install-windows-linux-macos"></a>[Instalación de Docker (Windows, Linux, macOS)](#tab/dockerinstall)

Siga estos pasos para instalar la CLI de Voz en un contenedor de Docker:

1. <a href="https://www.docker.com/get-started" target="_blank">Instale Docker Desktop<span class="docon docon-navigate-external x-hidden-focus"></span></a> para su plataforma si aún no está instalado.
2. En un nuevo símbolo del sistema o terminal, escriba este comando: 
   ```shell   
   docker pull msftspeech/spx
   ```
3. Escriba este comando. Debería ver la información de ayuda de la CLI de Voz: 
   ```shell 
   docker run -it --rm msftspeech/spx help
   ```

### <a name="mount-a-directory-in-the-container"></a>Montaje de un directorio en el contenedor

La herramienta CLI de Voz guarda los valores de configuración como archivos y los carga al ejecutar cualquier comando (excepto los de ayuda).
Al usar la CLI de Voz dentro de un contenedor de Docker, debe montar un directorio local desde el contenedor, de modo que la herramienta pueda almacenar o buscar los valores de configuración y, por tanto, leer o escribir los archivos necesarios para el comando, como los de audio de la voz.

En Windows, escriba este comando para crear un directorio local que la CLI de Voz pueda usar desde dentro del contenedor:

`mkdir c:\spx-data`

En Linux o Mac, escriba este comando en un terminal para crear un directorio y ver su ruta de acceso absoluta:

```bash
mkdir ~/spx-data
cd ~/spx-data
pwd
```

Usará la ruta de acceso absoluta al llamar a la CLI de Voz.

### <a name="run-speech-cli-in-the-container"></a>Ejecución de la CLI de Voz en el contenedor

En esta documentación se muestra el comando `spx` de la CLI de Voz que se usa en instalaciones que no son de Docker.
Al llamar al comando `spx` en un contenedor de Docker, debe montar un directorio en el contenedor para el sistema de archivos donde la CLI de Voz pueda almacenar y buscar los valores de configuración, y leer y escribir los archivos.

En Windows, los comandos se iniciarán de la siguiente manera:

```shell
docker run -it -v c:\spx-data:/data --rm msftspeech/spx
```

En Linux o macOS, los comandos tendrán un aspecto similar al del ejemplo siguiente. Reemplace `ABSOLUTE_PATH` por la ruta de acceso absoluta del directorio montado. El comando `pwd` de la sección anterior devolvió esta ruta de acceso. 

Si ejecuta este comando antes de establecer la clave y la región, recibirá un error indicándole que las establezca:
```shell   
sudo docker run -it -v ABSOLUTE_PATH:/data --rm msftspeech/spx
```

Para usar el comando `spx` instalado en un contenedor, escriba siempre el comando completo mostrado anteriormente, seguido de los parámetros de la solicitud.
Por ejemplo, en Windows, este comando establece la clave:

```shell
docker run -it -v c:\spx-data:/data --rm msftspeech/spx config @key --set SUBSCRIPTION-KEY
```

> [!WARNING]
> No puede usar el micrófono del equipo al ejecutar la CLI de Voz dentro de un contenedor de Docker. Sin embargo, puede leer y guardar archivos de audio en el directorio montado local. 

<!-- Need to troubleshoot issues with docker pull image

### Optional: Create a command line shortcut

If you're running the the Speech CLI from a Docker container on Linux or macOS you can create a shortcut. 

Follow these instructions to create a shortcut:
1. Open `.bash_profile` with your favorite text editor. For example:
   ```shell
   nano ~/.bash_profile
   ```
2. Next, add this function to your `.bash_profile`. Make sure you update this function with the correct path to your mounted directory:
   ```shell   
   spx(){
       sudo docker run -it -v ABSOLUTE_PATH:/data --rm msftspeech/spx
   }
   ```
3. Source your profile:
   ```shell
   source ~/.bash_profile
   ```
4. Now instead of running `sudo docker run -it -v ABSOLUTE_PATH:/data --rm msftspeech/spx`, you can just type `spx` followed by arguments. For example: 
   ```shell
   // Get some help
   spx help recognize

   // Recognize speech from an audio file 
   spx recognize --file /mounted/directory/file.wav
   ```

> [!WARNING]
> If you change the mounted directory that Docker is referencing, you need to update the function in `.bash_profile`.
--->
***

## <a name="create-subscription-config"></a>Creación de la configuración de la suscripción

Si desea empezar a usar la CLI de Voz, debe especificar la clave de la suscripción al servicio de voz y la información de la región. Para obtener estas credenciales, siga los pasos descritos en [Prueba gratuita del servicio Voz](../overview.md#try-the-speech-service-for-free).
Una vez que tenga la clave de suscripción y el identificador de región (p. ej., `eastus`, `westus`), ejecute los comandos siguientes.

```shell
spx config @key --set SUBSCRIPTION-KEY
spx config @region --set REGION
```

La autenticación de la suscripción se almacena ahora para futuras solicitudes de SPX. Si tiene que quitar cualquiera de estos valores almacenados, ejecute `spx config @region --clear` o `spx config @key --clear`.
