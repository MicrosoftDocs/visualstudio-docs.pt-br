---
title: Como substituir parâmetros em um modelo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- template parameters, substituting
- Visual Studio templates, using parameters
ms.assetid: a62924a7-4ba0-413d-b606-fdbe1fcf2807
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: bab1d1fd7cd08813dadefbcbec27dbd84bd7b66b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49279730"
---
# <a name="how-to-substitute-parameters-in-a-template"></a>Como substituir parâmetros em um modelo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode substituir parâmetros de modelo, como nomes de classes e namespaces, quando um arquivo baseado em um modelo for criado. Para ver uma lista completa dos parâmetros de modelo, consulte [Parâmetros de Modelo](../ide/template-parameters.md).  
  
## <a name="procedure"></a>Procedimento  
 Você pode substituir parâmetros nos arquivos de um modelo sempre que um projeto baseado nesse modelo for criado. Este procedimento explica como criar um modelo que substitui o nome de um namespace pelo nome do projeto seguro quando um novo projeto for criado com o modelo.  
  
#### <a name="to-use-a-parameter-to-replace-namespace-name-with-the-project-name"></a>Para usar um parâmetro para substituir o nome do namespace pelo nome do projeto  
  
1.  Insira o parâmetro em um ou mais dos arquivos de código no modelo. Por exemplo:  
  
    ```  
    namespace $safeprojectname$  
    ```  
  
    > [!NOTE]
    >  Parâmetros de modelo são escritos no formato $*parâmetro*$.  
  
2.  No arquivo .vstemplate do modelo, localize o elemento `ProjectItem` que inclui esse arquivo.  
  
3.  Defina o atributo `ReplaceParameters` como `true` para o elemento `ProjectItem`. Por exemplo:  
  
    ```  
    <ProjectItem ReplaceParameters="true">Class1.cs</ProjectItem>  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Parâmetros de modelo](../ide/template-parameters.md)   
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Elemento ProjectItem (Modelos de item do Visual Studio)](../extensibility/projectitem-element-visual-studio-item-templates.md)



