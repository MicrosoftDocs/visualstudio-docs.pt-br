---
title: Os serviços fornecidos (VSPackage de controle do código-fonte) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 750710cdc381573f8aa6fd064e1fc980030cf359
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202699"
---
# <a name="services-provided-source-control-vspackage"></a>Serviços fornecidos (VSPackage de controle do código-fonte)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Os serviços são o mecanismo principal por meio do qual funcionalidade é compartilhada entre os VSPackages e entre o ambiente de desenvolvimento integrado (IDE) do Visual Studio e seu VSPackages instalado. Para obter uma descrição detalhada dos serviços e sua importância no IDE do Visual Studio, consulte[Using e fornecendo serviços](../../extensibility/using-and-providing-services.md).  
  
## <a name="the-source-control-service"></a>O serviço de controle do código-fonte  
 O Visual Studio fornece duas camadas de serviços, serviços de nível de IDE e serviços de nível de pacote. Modo nativo, o IDE do Visual Studio fornece serviços de nível de IDE. O pacote de controle de origem consome alguns desses serviços. O pacote de controle do código-fonte como um VSPackage compartilha sua funcionalidade de controle do código-fonte, fornecendo um serviço de controle de origem particular do seu próprio. O pacote de controle do código-fonte encapsula o conjunto de interfaces relacionadas ao controle de origem implementada por ele na forma de um contrato que pode ser usado pelo IDE do Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)
