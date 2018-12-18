---
title: Criar um VSPackage de controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0d9513410aa3bb4773629846abbd70159ec6aa77
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39499732"
---
# <a name="create-a-source-control-vspackage"></a>Criar um VSPackage de controle do código-fonte
Esta documentação inclui links para a visão geral da arquitetura de um pacote de controle do código-fonte integrado com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], a API que é definida por as interfaces a serem implementados e os serviços a serem consumidos e um exemplo que ilustra uma simple fonte controle a implementação do pacote.  
  
 Com um controle do código-fonte VSPackage, você pode criar um caminho de integração profunda para controle de origem integrar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Ele permite que o pacote ignorar o controle de fonte padrão da interface do usuário hospedada por [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]responder a solicitações de controle do código-fonte do sistema de projeto e interagir com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] componentes, tais como **Gerenciador de soluções**. O [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] capacita [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] com um mecanismo para criar um VSPackage que pode se integrar a parceiros [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usando um modelo de serviço.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Introdução](../../extensibility/internals/getting-started-with-source-control-vspackages.md)  
 Discute o pacote de controle do código-fonte, que é uma alternativa mais avançada para o plug-in para implementar recursos de controle do código-fonte no controle de fonte [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
 [Arquitetura](../../extensibility/internals/source-control-vspackage-architecture.md)  
 Apresenta um diagrama e explica os componentes de um pacote de controle do código-fonte.  
  
 [Recursos](../../extensibility/internals/source-control-vspackage-features.md)  
 Descreve os vários recursos de um pacote de controle do código-fonte.  
  
 [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)  
 Descreve a estrutura de VSPackage que um pacote de controle de origem deve implementar para integração profunda.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criar um controle de fonte plug-in](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 Discute como criar um plug-in de controle de fonte que fornece funcionalidade de controle do código-fonte no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interface de usuário de controle do código-fonte (UI).  
  
 [Controle de origem](../../extensibility/internals/source-control.md)  
 Discute as opções para implementar o controle de origem como um recurso integrado do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].
