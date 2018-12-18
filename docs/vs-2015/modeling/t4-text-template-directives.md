---
title: T4 Diretivas de modelo de texto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, import directive
- text templates, include directive
- text templates, assembly directive
- text templates, output directive
- text templates, directives
- text templates, template directive
ms.assetid: 6898ee02-ebb2-4635-a4e9-350774c13cf2
caps.latest.revision: 83
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 00853b21ec077825337c2c360cac33775189dfdb
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49302166"
---
# <a name="t4-text-template-directives"></a>Diretivas de modelo de texto T4
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As diretivas fornecem instruções para o mecanismo de transformação do modelo de texto.  
  
 A sintaxe das diretivas é a seguinte:  
  
```  
<#@ DirectiveName [AttributeName = "AttributeValue"] ... #>  
```  
  
 Todos os valores dos atributos devem estar entre aspas duplas. Se o próprio valor contiver aspas, elas devem ser substituídas pelo caractere \.  
  
 As diretivas são normalmente os primeiros elementos de um arquivo de modelo ou de um arquivo incluído. Você não deve inseri-las em um bloco de códigos `<#...#>`, nem depois de um bloco de recursos da classe `<#+...#>`.  
  
 [Diretiva de modelo T4](../modeling/t4-template-directive.md)  
 ```  
<#@ template [language="VB"] [hostspecific="true|TrueFromBase"] [debug="true"] [inherits="templateBaseClass"] [culture="code"] [compilerOptions="options"] [visibility="internal"] [linePragmas="false"] #>  
```  
  
 [Diretiva de parâmetro T4](../modeling/t4-parameter-directive.md)  
 ```  
<#@ parameter type="Full.TypeName" name="ParameterName" #>  
```  
  
 [Diretiva de saída T4](../modeling/t4-output-directive.md)  
 ```  
<#@ output extension=".fileNameExtension" [encoding="encoding"] #>  
```  
  
 [Diretiva de assembly T4](../modeling/t4-assembly-directive.md)  
 ```  
<#@ assembly name="[assembly strong name|assembly file name]" #>  
```  
  
 [Diretiva de importação T4](../modeling/t4-import-directive.md)  
 ```  
<#@ import namespace="namespace" #>  
```  
  
 [Diretiva de inclusão T4](../modeling/t4-include-directive.md)  
 ```  
<#@ include file="filePath" #>  
```  
  
 [Diretiva CleanUpBehavior T4](../modeling/t4-cleanupbehavior-directive.md)  
 ```  
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>  
```  
  
 Além disso, você pode criar suas próprias diretivas. Para obter mais informações, consulte [criando processadores diretiva de modelo de texto do personalizado T4](../modeling/creating-custom-t4-text-template-directive-processors.md). Se você usar o SDK de Visualização e Modelagem para criar uma linguagem específica do domínio (DSL), um processador de diretriz será gerado como parte da DSL.



