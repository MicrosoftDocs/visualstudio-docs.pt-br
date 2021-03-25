---
title: Introdução com plug-ins de controle do código-fonte | Microsoft Docs
description: Saiba como criar um plug-in de controle do código-fonte que implementa as funções definidas na API de plug-in de controle do código-fonte para uso no controle de versão do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting started
- getting started, source control plug-ins
ms.assetid: 46ac1f9f-4ecc-4a72-88d3-4c7e1647e1cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1c1279fd425e8519ede49763ee2a307778c91e9e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061245"
---
# <a name="get-started-with-source-control-plug-ins"></a>Introdução aos plug-ins de controle do código-fonte
Para criar um plug-in de controle do código-fonte, você deve criar uma DLL que implemente as funções definidas na API de plug-in de controle do código-fonte e, em seguida, registrar a DLL com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para disponibilizá-la para uso no controle de versão do código-fonte.

 Três versões da API de plug-in de controle do código-fonte (versões 1,1, 1,2 e 1,3) estão disponíveis para plug-ins de controle do código-fonte. A API de plug-in de controle do código-fonte documentada aqui é a versão 1,3. Ele foi projetado para ser totalmente compatível com os plug-ins de controle do código-fonte que dão suporte às versões 1,1 e 1,2. A seção o que há de [novo na API de plug-in de controle do código-fonte versão 1,3](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md) detalha os novos recursos com suporte na versão mais recente da API de plug-in de controle do código-fonte.

## <a name="in-this-section"></a>Nesta seção
- [Como instalar um plug-in de controle do código-fonte](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)

 Descreve como fazer as entradas do registro que são necessárias para conectar uma DLL de controle do código-fonte.

- [O que há de novo na API de plug-in de controle do código-fonte versão 1,3](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)

 Fornece uma breve visão geral das alterações que foram feitas na API de plug-in de controle do código-fonte na versão 1,3.

- [O que há de novo na API de plug-in de controle do código-fonte versão 1,2](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

 Fornece uma breve visão geral das alterações que foram feitas na API de plug-in de controle do código-fonte na versão 1,2.

## <a name="related-sections"></a>Seções relacionadas
- [Plug-ins de controle do código-fonte](../../extensibility/source-control-plug-ins.md)

 Fornece uma listagem completa de todos os elementos na API de plug-in de controle do código-fonte.

- [Criar um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)

 Define o SDK de plug-in de controle do código-fonte e descreve os recursos incluídos.
