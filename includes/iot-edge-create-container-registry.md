---
author: kgremban
ms.service: iot-edge
ms.topic: include
ms.date: 12/30/2019
ms.author: kgremban
ms.openlocfilehash: 8cae7ac2d3b961120cb9100f5072dc141769afff
ms.sourcegitcommit: c95e2d89a5a3cf5e2983ffcc206f056a7992df7d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/24/2020
ms.locfileid: "95562874"
---
## <a name="create-a-container-registry"></a>Creación de un Registro de contenedor

En este tutorial se usa la extensión de Azure IoT Tools para fin de compilar un módulo y crear una **imagen de contenedor** a partir de los archivos. Después, insertará esta imagen en un **Registro** donde se almacenan y administran las imágenes. Por último, implementará la imagen en el Registro para que se ejecute en el dispositivo IoT Edge.

Puede usar cualquier registro compatible con Docker para almacenar las imágenes de contenedor. Dos de los servicios de registro de Docker más conocidos son [Azure Container Registry](../articles/container-registry/index.yml) y [Docker Hub](https://docs.docker.com/docker-hub/repos/#viewing-repository-tags). En este tutorial, utilizaremos Azure Container Registry.

Si no dispone de un registro de contenedores, siga estos pasos para crear uno nuevo en Azure:

1. En [Azure Portal](https://portal.azure.com), seleccione **Crear un recurso** > **Contenedores** > **Container Registry**.

2. Especifique los siguientes valores para crear un registro de contenedor:

   | Campo | Value |
   | ----- | ----- |
   | Suscripción | Seleccione una suscripción en la lista desplegable. |
   | Resource group | Se recomienda usar el mismo grupo de recursos para todos los recursos de prueba que se crean en las guías de inicio rápido y los tutoriales de IoT Edge. Por ejemplo, **IoTEdgeResources**. |
   | Nombre de registro | Especifique un nombre único. |
   | Location | Elija una ubicación cercana a usted. |
   | SKU | Seleccione **Básica**. |

3. Seleccione **Crear**.

4. Una vez creado el registro de contenedor, vaya a él y, en el panel izquierdo, seleccione **Claves de acceso** en el menú que se encuentra en **Configuración**. 

5. Haga clic para permitir que el usuario administrador pueda ver el **nombre de usuario** y la **contraseña** del registro de contenedor.

6. Copie los valores de **Servidor de inicio de sesión**, **Nombre de usuario** y **Contraseña**, y guárdelos en cualquier lugar que le resulte práctico. Dichos valores se usan en todo el tutorial para proporcionar acceso al registro de contenedor.

   ![Copiar el servidor de inicio de sesión, nombre de usuario y contraseña del registro de contenedor](./media/iot-edge-create-container-registry/registry-access-key.png)