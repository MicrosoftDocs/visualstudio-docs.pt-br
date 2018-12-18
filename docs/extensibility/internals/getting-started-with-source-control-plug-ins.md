---
title: Introdução ao Plug-ins de controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting started
- getting started, source control plug-ins
ms.assetid: 46ac1f9f-4ecc-4a72-88d3-4c7e1647e1cb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2f1eb4f76616f6a5f6791cbcd1b8a5770d1dcabb
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39498094"
---
# <a name="get-started-with-source-control-plug-ins"></a>Introdução ao plug-ins de controle de origem
Para criar um controle de fonte plug-in, você deve criar uma DLL que implementa as funções definidas a API de plug-in de controle do código-fonte, e, em seguida, para registrar a DLL com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para torná-lo disponível para uso no controle de versão do código de origem.  
  
 Três versões da API de plug-in de controle do código-fonte (versões 1.1, 1.2 e 1.3) estão disponíveis para o plug-ins de controle de origem. A API de plug-in de controle do código-fonte documentado aqui é a versão 1.3. Ele foi projetado para ser totalmente compatível com o plug-ins de controle de origem que dão suporte a versões 1.1 e 1.2. O [o que há de novo no código-fonte controle plug-in API versão 1.3](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md) seção detalha os novos recursos de suporte para a versão mais recente da API de plug-in de controle de origem.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Como: instalar um plug-in de controle do código-fonte](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)  
 Descreve como criar as entradas do registro que são necessárias para o plug-in de uma DLL de controle do código-fonte.  
  
 [O que há de novo no código-fonte controle plug-in API versão 1.3](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)  
 Fornece uma visão geral das alterações que foram feitas para a API de plug-in de controle do código-fonte na versão 1.3.  
  
 [O que há de novo no controle de fonte de plug-in API versão 1.2](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)  
 Fornece uma visão geral das alterações que foram feitas para a API de plug-in de controle do código-fonte na versão 1.2.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Plug-ins de controle de origem](../../extensibility/source-control-plug-ins.md)  
 Fornece uma lista completa de todos os elementos na API de plug-in de controle de origem.  
  
 [Criar um controle de fonte plug-in](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 Define o SDK do plug-in de controle de origem e descreve os recursos incluídos.