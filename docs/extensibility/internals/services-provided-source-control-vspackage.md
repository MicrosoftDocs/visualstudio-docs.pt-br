---
title: Serviços fornecidos (VSPackage de controle do código-fonte) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6a52ffa7067a91582d8bfe31e09d6b03be54c4ea
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31129596"
---
# <a name="services-provided-source-control-vspackage"></a>Serviços fornecidos (VSPackage de controle de origem)
Serviços são o mecanismo principal por meio do qual funcionalidade é compartilhada entre VSPackages e entre o ambiente de desenvolvimento integrado (IDE) do Visual Studio e seus VSPackages instalado. Para obter uma descrição detalhada dos serviços e sua importância no IDE do Visual Studio, consulte[usando e fornecer serviços](../../extensibility/using-and-providing-services.md).  
  
## <a name="the-source-control-service"></a>O serviço de controle de origem  
 O Visual Studio fornece duas camadas de serviços, serviços de nível de IDE e serviços de nível de pacote. Modo nativo, o IDE do Visual Studio fornece serviços de nível de IDE. O pacote de controle de origem consome alguns desses serviços. O pacote de controle de origem como um VSPackage compartilha sua funcionalidade de controle de origem, fornecendo um serviço de controle de fonte privada de seu próprio. O pacote de controle do código-fonte encapsula o conjunto de interfaces relacionada ao controle de origem implementado na forma de um contrato que pode ser usado pelo Visual Studio IDE.  
  
## <a name="see-also"></a>Consulte também  
 [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)