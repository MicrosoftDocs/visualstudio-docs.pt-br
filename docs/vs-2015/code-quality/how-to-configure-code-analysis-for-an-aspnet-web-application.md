---
title: 'Como: configurar a análise de código para um aplicativo Web ASP.NET | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.codeanalysis.propertypages.asp
ms.assetid: b3000b31-fd9d-489e-81a2-a4bee49453ba
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: bf7450341dd166977d67639f4f3762fae6ef89c8
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49283901"
---
# <a name="how-to-configure-code-analysis-for-an-aspnet-web-application"></a>Como configurar a análise de código para um aplicativo Web do ASP.NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)] e [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)] você pode selecionar em uma lista de análise de código *conjuntos de regra* para aplicar a [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] aplicativo Web. O conjunto de regras padrão é a regras Mininimum recomendado da Microsoft. Você pode selecionar outro conjunto de regras para aplicar ao site da Web.  
  
### <a name="to-configure-a-rule-set-for-an-aspnet-page-framework-project"></a>Para configurar uma regra definida para um projeto de estrutura de página ASP.NET  
  
1.  Selecione o site da Web **Gerenciador de soluções**.  
  
2.  Sobre o **Analyze** menu, clique em **configurar a análise de código para o Site da Web**.  
  
3.  Se você tiver selecionado a solução e a solução tem mais de um projeto, selecione a configuração e destino operacional sistema de compilação do **Configuration** e **plataforma** lista.  
  
4.  Para cada projeto na solução, clique o **do conjunto de regras** coluna e, em seguida, clique o nome da regra é definida para ser executada.  
  
5.  Por padrão, a análise de código é executada em todos os projetos na solução. Para desabilitar ou habilitar a análise de código para um projeto específico, siga estas etapas:  
  
    1.  Clique com botão direito no nome do projeto e, em seguida, clique em Propriedades.  
  
    2.  Marque ou desmarque a **Enable Code Analysis** caixa de seleção. Você também pode executar a análise de código manualmente selecionando **executar a análise de código no Site da Web** da **analisar** menu.  
  
6.  No **executar este conjunto de regras** suspensa lista, siga estas etapas:  
  
    -   Selecione o conjunto de regras que você deseja usar.  
  
    -   Selecione  **\<procurar >** especificar uma regra personalizada existente definida que não está na lista.  
  
    -   Defina um conjunto de regras personalizadas. Para obter mais informações, consulte [criação de conjuntos de regras personalizado](../code-quality/creating-custom-code-analysis-rule-sets.md).



