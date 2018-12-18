---
title: Aplicar chaves do produto (Product Keys) durante a implantação do Visual Studio
description: Saiba como aplicar chaves de produto de forma programática quando você implanta o Visual Studio.
ms.date: 08/14/2017
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.assetid: d79260be-6234-4fd3-89b5-a9756b4a93c1
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fea2ffa8fd81a5012c89289df36d7f698fb60c4e
ms.sourcegitcommit: 6b092e7d466377f06913d49d183dbbdca16730f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2018
ms.locfileid: "43138710"
---
# <a name="automatically-apply-product-keys-when-deploying-visual-studio"></a>Aplicar chaves do produto (Product Keys) durante a implantação do Visual Studio

É possível aplicar a chave do produto (Product Key) de forma programática como parte de um script usado para automatizar a implantação do Visual Studio. Você pode definir a chave do produto (Product Key) em um dispositivo de forma programática durante a instalação do Visual Studio ou após a conclusão de uma instalação.

## <a name="apply-the-license-after-installation"></a>Aplicar a licença após a instalação

 É possível ativar uma versão instalada do Visual Studio com uma chave do produto (Product Key) usando o utilitário `StorePID.exe` nos computadores de destino no modo sem confirmação. `StorePID.exe` é um utilitário instalado com o Visual Studio 2017 no seguinte local padrão: <br> `C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE`

 Execute `StorePID.exe` com privilégios elevados, usando um agente do System Center ou em um prompt de comandos com privilégios elevados. Em seguida, informe a chave do produto (Product Key) e o MPC (código de produto da Microsoft).

>[!IMPORTANT]
> Verifique se você incluiu os traços na chave do produto (Product Key).

 ```cmd
 StorePID.exe [product key including the dashes] [MPC]
 ```

 O exemplo a seguir mostra uma linha de comando para aplicar a licença ao Visual Studio 2017 Enterprise, que tem um MPC de 08860, uma chave do produto (Product Key) `AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE` e pressupõe um local padrão para a instalação:

 ```cmd
 "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\StorePID.exe" AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE 08860
 ```

 A seguinte tabela lista os códigos MPC para cada edição do Visual Studio:

| Edição do Visual Studio                | MPC   |
|--------------------------------------|-------|
| Visual Studio Enterprise 2017        | 08860 |
| Visual Studio Professional 2017      | 08862 |
| Visual Studio Test Professional 2017 | 08866 |

Se `StorePID.exe` aplicar a chave do produto (Product Key) com êxito, ele retornará um `%ERRORLEVEL%` de 0. Se encontrar erros, ele retornará um dos códigos a seguir, dependendo da condição de erro:

| Erro                     | Código |
|---------------------------|------|
| `PID_ACTION_SUCCESS`      | 0    |
| `PID_ACTION_NOTINSTALLED` | 1    |
| `PID_ACTION_INVALID`      | 2    |
| `PID_ACTION_EXPIRED`      | 3    |
| `PID_ACTION_INUSE`        | 4    |
| `PID_ACTION_FAILURE`      | 5    |
| `PID_ACTION_NOUPGRADE`    | 6    |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Instalar o Visual Studio](../install/install-visual-studio.md)
* [Criar uma instalação offline do Visual Studio](../install/create-an-offline-installation-of-visual-studio.md)
