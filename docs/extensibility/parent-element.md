---
title: Elemento pai | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Parent
- Parent element (VSCT XML schema)
ms.assetid: e4624ac8-1b9a-4940-910a-528a661cefad
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9a66f9fff773fb9a9542de13ceb97ad8732c319b
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39635850"
---
# <a name="parent-element"></a>Elemento pai
O pai de um botão ou caixa de combinação só pode ser um grupo. O pai de um menu ou grupo pode ser qualquer menu ou grupo. Em um [elemento CommandPlacement](../extensibility/commandplacement-element.md), esse elemento é necessário; em todas as outras instâncias é opcional. Se esse elemento for omitido, o pai do `Group_Undefined:0` será assumida.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<Parent guid="guidMyCommandSet" id="MyParentGroupOrMenu" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|GUID|Necessário. Identificador de comando do GUID/ID de GUID.|  
|id|Necessário. Identificador de comando de ID de/ID de GUID.|  
  
### <a name="child-elements"></a>Elementos filho  
 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento CommandTable](../extensibility/commandtable-element.md)|Define todos os elementos que representam os comandos que fornece um VSPackage para o ambiente de desenvolvimento integrado (IDE). Por exemplo, itens de menu, menus, barras de ferramentas e caixas de combinação.|  
|[Elemento Buttons](../extensibility/buttons-element.md)|Grupos [elemento Button](../extensibility/button-element.md) elementos.|  
|[Elemento menus](../extensibility/menus-element.md)|Define todos os menus que implementa um VSPackage.|  
|[Elemento Groups](../extensibility/groups-element.md)|Contém entradas que definem os grupos de comando de um VSPackage.|  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)