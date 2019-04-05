---
title: Criando um controle de fonte plug-in | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: c7e69fa4-150e-469a-a6fc-fa1260bdbb07
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 37cb4cfc71b2574600bf7ca886c693b888ec821a
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58926447"
---
# <a name="creating-a-source-control-plug-in"></a>Criando um plug-in de controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O SDK do Visual Studio fornece recursos que permitem que você adicione funcionalidade de controle do código-fonte para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE). Ele permite usar qualquer DLL de plug-in que está em conformidade com a API de plug-in de controle do código-fonte descritos nesta documentação.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Introdução](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)  
 Descreve como instalar um plug-in de controle do código-fonte e realça as versões de API de plug-in de controle do código-fonte está disponíveis.  
  
 [Arquitetura](../../extensibility/internals/source-control-plug-in-architecture.md)  
 Usa um diagrama de arquitetura para explicar a integração de controle de origem plug-in com o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE.  
  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)  
 Fornece orientação sobre como testar a instalação e operação de um plug-in de controle de origem.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criar um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md)  
 Discute como criar um controle de fonte VSPackage que não apenas fornece a funcionalidade de controle do código-fonte, mas substitui [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] da interface do usuário do controle de origem.  
  
 [Plug-ins de controle do código-fonte](../../extensibility/source-control-plug-ins.md)  
 Fornece uma lista completa de todos os elementos na API de plug-in de controle de origem.  
  
 [Controle do código-fonte](../../extensibility/internals/source-control.md)  
 Discute as opções para implementar o controle de origem como um recurso integrado do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].
