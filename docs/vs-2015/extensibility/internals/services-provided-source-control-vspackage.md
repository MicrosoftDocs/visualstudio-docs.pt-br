---
title: Os serviços fornecidos (VSPackage de controle do código-fonte) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: d3131acfb26dc1e973314f69fab69cad46df6295
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786633"
---
# <a name="services-provided-source-control-vspackage"></a>Serviços fornecidos (VSPackage de controle do código-fonte)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Os serviços são o mecanismo principal por meio do qual funcionalidade é compartilhada entre os VSPackages e entre o ambiente de desenvolvimento integrado (IDE) do Visual Studio e seu VSPackages instalado. Para obter uma descrição detalhada dos serviços e sua importância no IDE do Visual Studio, consulte[Using e fornecendo serviços](../../extensibility/using-and-providing-services.md).  
  
## <a name="the-source-control-service"></a>O serviço de controle do código-fonte  
 O Visual Studio fornece duas camadas de serviços, serviços de nível de IDE e serviços de nível de pacote. Modo nativo, o IDE do Visual Studio fornece serviços de nível de IDE. O pacote de controle de origem consome alguns desses serviços. O pacote de controle do código-fonte como um VSPackage compartilha sua funcionalidade de controle do código-fonte, fornecendo um serviço de controle de origem particular do seu próprio. O pacote de controle do código-fonte encapsula o conjunto de interfaces relacionadas ao controle de origem implementada por ele na forma de um contrato que pode ser usado pelo IDE do Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)

