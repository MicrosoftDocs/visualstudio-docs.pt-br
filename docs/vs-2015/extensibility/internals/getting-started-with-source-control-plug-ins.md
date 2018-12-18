---
title: Introdução ao Plug-ins de controle do código-fonte | Microsoft Docs
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
- source control plug-ins, getting started
- getting started, source control plug-ins
ms.assetid: 46ac1f9f-4ecc-4a72-88d3-4c7e1647e1cb
caps.latest.revision: 22
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e521c239f474d803da5b615de8dcf1cf56d37df3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755240"
---
# <a name="getting-started-with-source-control-plug-ins"></a>Introdução aos plug-ins do controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Para criar um controle de fonte plug-in, você deve criar uma DLL que implementa as funções definidas a API de plug-in de controle do código-fonte, e, em seguida, para registrar a DLL com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para torná-lo disponível para uso no controle de versão do código de origem.  
  
 Três versões da API de plug-in de controle do código-fonte (versões 1.1, 1.2 e 1.3) estão disponíveis para o plug-ins de controle de origem. A API de plug-in de controle do código-fonte documentado aqui é a versão 1.3. Ele foi projetado para ser totalmente compatível com o plug-ins de controle de origem que dão suporte a versões 1.1 e 1.2. O [o que há de novo no código-fonte controle plug-in API versão 1.3](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md) seção detalha os novos recursos de suporte para a versão mais recente da API de plug-in de controle de origem.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Como instalar um plug-in de controle do código-fonte](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)  
 Descreve como criar as entradas do registro que são necessárias para o plug-in de uma DLL de controle do código-fonte.  
  
 [Novidades na Versão 1.3 da API do plug-in de controle de código-fonte](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)  
 Fornece uma visão geral das alterações que foram feitas para a API de plug-in de controle do código-fonte na versão 1.3.  
  
 [Novidades na Versão 1.2 da API do plug-in de controle de código-fonte](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)  
 Fornece uma visão geral das alterações que foram feitas para a API de plug-in de controle do código-fonte na versão 1.2.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Plug-ins de controle do código-fonte](../../extensibility/source-control-plug-ins.md)  
 Fornece uma lista completa de todos os elementos na API de plug-in de controle de origem.  
  
 [Criar um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 Define o SDK do plug-in de controle de origem e descreve os recursos incluídos.

