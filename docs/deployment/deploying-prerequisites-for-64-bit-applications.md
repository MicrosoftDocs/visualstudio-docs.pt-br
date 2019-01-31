---
title: Implantando pré-requisitos para aplicativos de 64 bits | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [Visual Studio], 64-bit
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- 64-bit applications [Visual Studio]
ms.assetid: 87399e20-5510-41e4-b5b7-4a87c5773f21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6aab5fb7487cc2e79bc2e0e1a7a5dffce96447f9
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55024546"
---
# <a name="deploy-prerequisites-for-64-bit-applications"></a>Implantar pré-requisitos para aplicativos de 64 bits
A implantação do ClickOnce oferece suporte à instalação de aplicativos em plataformas de 64 bits. As plataformas de destino são plataformas **x86** para 32 bits, **x64** para máquinas compatíveis com o conjunto de instruções AMD64 e EM64T e Itanium para o processador **Itanium** de 64 bits.  

## <a name="prerequisites"></a>Pré-requisitos  
 A tabela a seguir lista os redistribuíveis que você pode usar como pré-requisitos para a instalação do seu aplicativo de 64 bits.  

 Se você selecionar um pré-requisito que não tem componentes de 64 bits, poderá ver um aviso informando que os pacotes selecionados não estão disponíveis para a plataforma de 64 bits.  


| Redistribuível | Suporte a x64 | Suporte a IA64 |
| - |-------------|--------------|
| [!INCLUDE[vsto_runtime](../deployment/includes/vsto_runtime_md.md)] | Sim | Não |
| Bibliotecas de tempo de execução do Visual C++ 2010 (IA64) | Não | Sim |
| Bibliotecas de Tempo de Execução do Visual C++ 2010 (x64) | Sim | Não |
| Microsoft .NET Framework 4 (x86 e x64) | Sim | |
| Perfil de cliente do Microsoft .NET Framework 4 (x86 e x64) | Sim | |

## <a name="see-also"></a>Consulte também  
 [Implantar aplicativos, serviços e componentes](../deployment/deploying-applications-services-and-components.md)   
 [Como: Instalar pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [Aplicativos de 64 bits](/dotnet/framework/64-bit-apps)