---
title: Elemento Symbols | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c8d28d225bd3a8d5c105bf54b9c63574002aed15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160456"
---
# <a name="symbols-element"></a>Elemento Symbols
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Define GUIDs e IDs que são usados por outros elementos VSCT. Para código não gerenciado, essas informações normalmente são provenientes dos arquivos de cabeçalho especificados pelo [elemento externo](../extensibility/extern-element.md). O código gerenciado usa os elementos filho do elemento Symbols para definir essas informações.  
  
 Se você criar um arquivo. vsct de um arquivo. CTO existente, os símbolos serão gerados como filhos do elemento Symbols. Para obter mais informações, consulte [como: criar um. Arquivo vsct de um existente. Arquivo CTO](../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md).  
  
 O elemento Symbols não deve ser confundido com o [elemento define](../extensibility/define-element.md), que define os pares de nome-valor para uso pelo pré-processador.  
  
## <a name="syntax"></a>Syntax  
  
```  
<Symbols>  
  <GuidSymbol>... </GuidSymbol>  
  <GuidSymbol>... </GuidSymbol>  
</Symbols>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|Nenhum||  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|GuidSymbol|Define um símbolo GUID. GuidSymbol tem dois atributos obrigatórios: nome e valor. O nome é o nome do símbolo e o valor é o valor do GUID como uma cadeia de caracteres.<br /><br /> Por exemplo: \<GuidSymbol name="guidVsPackage1Pkg"   value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />|  
|IDSymbol|Define um símbolo. IDSymbol tem dois atributos obrigatórios: nome e valor. O nome é o nome do símbolo e o valor é o valor do símbolo como uma cadeia de caracteres.<br /><br /> Por exemplo: \<IDSymbol name="MyMenuGroup" value="0x1020" />|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento CommandTable](../extensibility/commandtable-element.md)|O elemento raiz do arquivo. vsct.|  
  
## <a name="example"></a>Exemplo  
  
```  
<Symbols>  
  <GuidSymbol name="guidVsPackage1Pkg" value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />  
  <GuidSymbol name="guidVsPackage1CmdSet" value="{cb9dfd7f-2fcc-4a3e-aae8-f7fe30b1cfac}">  
    <IDSymbol name="MyMenuGroup" value="0x1020" />  
    <IDSymbol name="cmdidMyCommand" value="0x0100" />  
    <IDSymbol name="cmdidMyTool" value="0x0101" />  
  </GuidSymbol>  
</Symbols>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Arquivos .Vsct (Visual Studio Command Table)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
