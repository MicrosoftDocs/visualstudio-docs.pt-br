---
title: Projeto de modelagem | Microsoft Docs
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
- automation [Visual Studio SDK], implementing project objects
- project models, automation
ms.assetid: c8db8fdb-88c1-4b12-86fe-f3c30a18f9ee
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 37b237a462900735ea641407d10719d43334262e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51808408"
---
# <a name="project-modeling"></a>Modelagem do projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A próxima etapa no fornecimento de automação para seu projeto é implementar os objetos de projeto padrão: o <xref:EnvDTE.Projects> e `ProjectItems` coleções; o `Project` e <xref:EnvDTE.ProjectItem> objetos; e os objetos restantes exclusivos para sua implementação. Esses objetos padrão são definidos no arquivo Dteinternal.h. Uma implementação dos objetos padrão é fornecida no exemplo BscPrj. Você pode usar essas classes como modelos para criar seus próprios objetos de projeto padrão que estão no lado a lado com os objetos de outros tipos de projeto do projeto.  
  
 Presume que um consumidor de automação para ser capaz de chamar <xref:EnvDTE.Solution>("`<UniqueProjName>")` e <xref:EnvDTE.ProjectItems> (`n`) em que n é um número de índice para a obtenção de um projeto específico na solução. Fazer essa chamada de automação faz com que o ambiente chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.GetProperty%2A> na hierarquia do projeto apropriado, passando VSITEMID_ROOT como o parâmetro ItemID e VSHPROPID_ExtObject como parâmetro VSHPROPID. `IVsHierarchy::GetProperty` Retorna um `IDispatch` ponteiro para o objeto de automação, fornecer os principais `Project` interface, que você implementou.  
  
 A seguir está a sintaxe de `IVsHierarchy::GetProperty`.  
  
 `HRESULT GetProperty (`  
  
 `VSITEMID` `itemid`,  
  
 `VSHPROPID` `propid`,  
  
 `VARIANT` `*pvar`  
  
 `);`  
  
 Projetos de acomodar o aninhamento e usam coleções para criar grupos de itens de projeto. A hierarquia tem esta aparência.  
  
```  
Projects  
  |– Project  
      |– ProjectItems (a collection of ProjectItem)  
          |– ProjectItem (single object) or ProjectItems (another collection)  
```  
  
 Aninhar significa que um <xref:EnvDTE.ProjectItem> objeto pode ser <xref:EnvDTE.ProjectItems> coleção ao mesmo tempo porque um `ProjectItems` coleção pode conter os objetos aninhados. O exemplo de projeto básico não Demonstre desse aninhamento. Implementando o `Project` do objeto, você participa de estrutura de árvore que caracteriza o design do modelo de automação geral.  
  
 A automação de projeto segue o caminho no diagrama a seguir.  
  
 ![Objetos de projeto do Visual Studio](../../extensibility/internals/media/projectobjects.gif "ProjectObjects")  
Automação de projeto  
  
 Se você implementar uma `Project` do objeto, o ambiente ainda retornará um genérico `Project` objeto que contém apenas o nome do projeto.  
  
## <a name="see-also"></a>Consulte também  
 <xref:EnvDTE.Projects>   
 <xref:EnvDTE.ProjectItem>   
 <xref:EnvDTE.ProjectItems>

