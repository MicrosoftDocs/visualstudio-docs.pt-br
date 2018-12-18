---
title: 'Como: configurar a análise de código para um projeto de código gerenciado | Microsoft Docs'
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
- vs.codeanalysis.propertypages.csvb
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
ms.assetid: 618f6ff3-db0e-46cb-b08d-dfa35e62c9e7
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 98f3d14b73b0219d0fcec4312648bf613f37378e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49239181"
---
# <a name="how-to-configure-code-analysis-for-a-managed-code-project"></a>Como configurar a análise de código para um projeto de código gerenciado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] e [!INCLUDE[vsPro](../includes/vspro-md.md)], você pode escolher entre uma lista de análise de código *conjuntos de regra* para aplicar a um projeto de código gerenciado. O conjunto de regras padrão é a regras mínimo recomendado da Microsoft. Você pode aplicar outra regra definida para um projeto ou para todos os projetos em uma solução.  
  
> [!NOTE]
>  Para obter informações sobre como configurar uma regra definida para aplicativos Web ASP.NET, consulte [como: configurar a análise de código para um aplicativo Web ASP.NET](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md).  
  
### <a name="to-configure-a-rule-set-for-a-net-framework-project"></a>Para configurar uma regra definida para um projeto do .NET Framework  
  
1.  Na **Gerenciador de soluções**, clique no projeto.  
  
2.  Sobre o **Analyze** menu, clique em **configurar a análise de código para** *ProjectName*.  
  
3.  No **Configuration** e **plataforma** listas, clique na plataforma de destino e a configuração de compilação.  
  
4.  Para executar análise de código sempre que o projeto é compilado usando a configuração selecionada, selecione a **habilitar análise de código na compilação (define a constante CODE_ANALYSIS)** caixa de seleção. Você também pode executar a análise de código manualmente abrindo o **Analyze** menu e clicando em **executar análise de código na** *ProjectName*.  
  
5.  Por padrão, a análise de código não relate os avisos de código que é gerado automaticamente por ferramentas externas. Para exibir avisos do código gerado, desmarque a **Suprimir resultados do código gerado** caixa de seleção.  
  
    > [!NOTE]
    >  Essa opção não suprime erros de análise de código e avisos do código gerado quando os erros e avisos que aparecem em formulários e modelos. Você pode exibir e manter o código-fonte para um formulário ou um modelo.  
  
6.  No **executar este conjunto de regras** lista, siga um destes procedimentos:  
  
    -   Clique o conjunto de regras que você deseja usar.  
  
    -   Clique em  **\<procurar... >** especificar uma regra personalizada existente definida que não está na lista.  
  
    -   Defina um conjunto de regras personalizadas.  
  
         Para obter mais informações, consulte [criação de conjuntos de regras personalizado](../code-quality/creating-custom-code-analysis-rule-sets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: configurando e usando um conjunto de regras personalizado](../code-quality/walkthrough-configuring-and-using-a-custom-rule-set.md)



