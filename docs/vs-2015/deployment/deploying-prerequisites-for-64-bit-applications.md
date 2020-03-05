---
title: Implantando pré-requisitos para aplicativos de 64 bits | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
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
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 92f30e8e059475c907da184aa59a8e4b7a2cf19f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65675579"
---
# <a name="deploying-prerequisites-for-64-bit-applications"></a>Implantando pré-requisitos para aplicativos de 64 bits
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A implantação do ClickOnce oferece suporte à instalação de aplicativos em plataformas de 64 bits. As plataformas de destino são plataformas **x86** para 32 bits, **x64** para máquinas compatíveis com o conjunto de instruções AMD64 e EM64T e Itanium para o processador **Itanium** de 64 bits.  
  
## <a name="prerequisites"></a>Prerequisites  
 A tabela a seguir lista os redistribuíveis que você pode usar como pré-requisitos para a instalação do seu aplicativo de 64 bits.  
  
 Se você selecionar um pré-requisito que não tem componentes de 64 bits, poderá ver um aviso informando que os pacotes selecionados não estão disponíveis para a plataforma de 64 bits.  
  
|Redistribuível|Suporte a x64|Suporte a IA64|  
|---------------------|-----------------|------------------|  
|[!INCLUDE[vsto_runtime](../includes/vsto-runtime-md.md)]|Sim|Não|  
|Bibliotecas de runtime do Visual C++ 2010 (IA64)|Não|Sim|  
|Bibliotecas de runtime do Visual C++ 2010 (x64)|Sim|Não|  
|Microsoft .NET Framework 4 (x86 e x64)|Sim||  
|Perfil de cliente do Microsoft .NET Framework 4 (x86 e x64)|Sim||  
  
## <a name="see-also"></a>Consulte também  
 [Implantando aplicativos, serviços e componentes](../deployment/deploying-applications-services-and-components.md)   
 [Como: Instalar pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [Aplicativos de 64 bits](https://msdn.microsoft.com/library/fd4026bc-2c3d-4b27-86dc-ec5e96018181)
