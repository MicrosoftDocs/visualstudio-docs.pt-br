---
title: Criando um controle de fonte plug-in | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: c7e69fa4-150e-469a-a6fc-fa1260bdbb07
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 361ad46c781f9e29c7c99fa4340433583571d811
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497882"
---
# <a name="create-a-source-control-plug-in"></a>Criar um controle de fonte plug-in
O SDK do Visual Studio fornece recursos que permitem que você adicione funcionalidade de controle do código-fonte para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o ambiente de desenvolvimento integrado (IDE). Ele permite usar qualquer DLL de plug-in que está em conformidade com a API de plug-in de controle do código-fonte descritos nesta documentação.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Introdução](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)  
 Descreve como instalar um plug-in de controle do código-fonte e realça as versões de API de plug-in de controle do código-fonte está disponíveis.  
  
 [Arquitetura](../../extensibility/internals/source-control-plug-in-architecture.md)  
 Usa um diagrama de arquitetura para explicar a integração de controle de origem plug-in com o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.  
  
 [Guia de teste](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)  
 Fornece orientação sobre como testar a instalação e operação de um plug-in de controle de origem.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criar um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md)  
 Discute como criar um controle de fonte VSPackage que não apenas fornece a funcionalidade de controle do código-fonte, mas substitui [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] da interface do usuário do controle de origem.  
  
 [Plug-ins de controle de origem](../../extensibility/source-control-plug-ins.md)  
 Fornece uma lista completa de todos os elementos na API de plug-in de controle de origem.  
  
 [Controle de origem](../../extensibility/internals/source-control.md)  
 Discute as opções para implementar o controle de origem como um recurso integrado do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].
