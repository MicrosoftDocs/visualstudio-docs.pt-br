---
title: T4 Diretiva Import | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 713ca975-b9aa-4210-bf6d-b7660f5b193b
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 00033640ec7810f97785b38437795906500a7866
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163668"
---
# <a name="t4-import-directive"></a>Diretiva de importação T4
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em blocos de código de um modelo de texto T4 do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], a diretiva `import` permite que você referencie os elementos em outro namespace sem fornecer um nome totalmente qualificado. É o equivalente de `using` em C# ou `imports` em [!INCLUDE[vb_current_short](../includes/vb-current-short-md.md)].  
  
 Para obter uma visão geral da gravação de modelos de texto T4, consulte [gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md).  
  
## <a name="using-the-import-directive"></a>Usando a diretiva de importação  
  
```  
<#@ import namespace="namespace" #>  
```  
  
 Neste exemplo, o código do modelo pode omitir um namespace explícito para membros de System.IO:  
  
```  
<#@ import namespace="System.IO" #>  
<#   
   string fileContent = File.ReadAllText("C:\x.txt"); // System.IO.File  
#>   
The file contains: <#=  fileContent #>  
```  
  
## <a name="standard-imports"></a>Importações padrão  
 O seguinte namespace é importado automaticamente, para que não seja necessário gravar uma diretiva de importação para ele:  
  
- `System`  
  
  Além disso, se você usar uma diretiva personalizada, o processador de diretriz pode importar alguns namespaces automaticamente.  
  
  Por exemplo, se você gravar modelos para uma linguagem específica do domínio (DSL), você não precisa gravar diretivas de importação para os namespaces a seguir:  
  
- `Microsoft.VisualStudio.Modeling`  
  
- O namespace de sua DSL  
  
## <a name="see-also"></a>Consulte também  
 [Diretiva de assembly T4](../modeling/t4-assembly-directive.md)
