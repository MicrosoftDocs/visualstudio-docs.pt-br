---
title: Criar um VSPackage de controle do código-fonte | Microsoft Docs
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
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
caps.latest.revision: 24
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0e85c25f1a5d935d36466e922659b5c2021b4c71
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779028"
---
# <a name="creating-a-source-control-vspackage"></a>Criar um VSPackage de controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Esta documentação inclui links para a visão geral da arquitetura de um pacote de controle do código-fonte integrado com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], a API que é definida por as interfaces a serem implementados e os serviços a serem consumidos e um exemplo que ilustra uma simple fonte controle a implementação do pacote.  
  
 Com um controle do código-fonte VSPackage, você pode criar um caminho de integração profunda para controle de origem integrar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Ele permite que o pacote ignorar o controle de fonte padrão da interface do usuário hospedada por [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]responder a solicitações de controle do código-fonte do sistema de projeto e interagir com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] componentes, tais como **Gerenciador de soluções**. O [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] capacita [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] com um mecanismo para criar um VSPackage que pode se integrar a parceiros [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] usando um modelo de serviço.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Introdução](../../extensibility/internals/getting-started-with-source-control-vspackages.md)  
 Discute o pacote de controle do código-fonte, que é uma alternativa mais avançada para o plug-in para implementar recursos de controle do código-fonte no controle de fonte [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 [Arquitetura](../../extensibility/internals/source-control-vspackage-architecture.md)  
 Apresenta um diagrama e explica os componentes de um pacote de controle do código-fonte.  
  
 [Recursos](../../extensibility/internals/source-control-vspackage-features.md)  
 Descreve os vários recursos de um pacote de controle do código-fonte.  
  
 [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)  
 Descreve a estrutura de VSPackage que um pacote de controle de origem deve implementar para integração profunda.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criar um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 Discute como criar um plug-in de controle de fonte que fornece funcionalidade de controle do código-fonte no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] interface de usuário de controle do código-fonte (UI).  
  
 [Controle do código-fonte](../../extensibility/internals/source-control.md)  
 Discute as opções para implementar o controle de origem como um recurso integrado do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].

