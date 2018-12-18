---
title: Elementos de Design de VSPackage de controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control packages, design elements
ms.assetid: edd3f2ff-ca32-4465-8ace-4330493b67bb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: eb741a7dc7423c27baed2cd79476239f4e41a170
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130213"
---
# <a name="source-control-vspackage-design-elements"></a>Elementos de Design de VSPackage de controle do código-fonte
Os tópicos nesta seção descrevem a estrutura de controle de origem de VSPackage deve implementar para integração profunda. Também lista as interfaces e serviços que a fonte de controle VSPackage podem implementar e os serviços e interfaces o VSPackage do controle de origem pode usar outros [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] componentes para dar suporte a sua fonte de modelo e a funcionalidade de controle.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Estrutura VSPackage](../../extensibility/internals/vspackage-structure-source-control-vspackage.md)  
 Define a estrutura do controle de origem VSPackage.  
  
 [Interfaces e serviços relacionados](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)  
 Lista de serviços e interfaces relacionadas a pacotes de controle de origem.  
  
 [Serviços fornecidos](../../extensibility/internals/services-provided-source-control-vspackage.md)  
 Descreve o serviço de controle de origem fornecido pelo controle de origem VSPackage.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criar um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md)  
 Discute como criar um controle de origem VSPackage que não só fornece a funcionalidade de controle de origem, mas pode ser usado para personalizar o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] da interface do usuário do controle de origem.