---
title: Elemento IDSymbol | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDSymbol element (VSCT XML schema)
- VSCT XML schema elements, IDSymbol
ms.assetid: 760cfd20-3c06-422c-9103-98bfa1f387f8
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8d88acb221abfc26c45c9002abb92f704936334b
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39500375"
---
# <a name="idsymbol-element"></a>Elemento IDSymbol
O `IDSymbol` elemento contém a ID do par GUID:ID que representa um menu, um grupo ou um comando. O GUID é proveniente do pai `GuidSymbol` elemento. O `IDSymbol` elemento tem um `name` que fornece um nome amigável para a ID, que está contida no atributo de `value` atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<IDSymbol name=ElementName value="0x0010" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|name|Necessário. Nome do símbolo de ID.|  
|Valor |Necessário. Valor numérico da ID do símbolo de ID.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento GuidSymbol](../extensibility/guidsymbol-element.md)|Contém o GUID do par GUID:ID que representa um menu, um grupo ou um comando. Agrupa elementos `IDSymbol`.|  
  
## <a name="remarks"></a>Comentários  
 Cada `IDSymbol` elemento em um determinado `GuidSymbol` elemento deve ter um único `value`. No entanto, `IDSymbol` elementos que têm valores idênticos podem existir em um pacote, desde que eles tenham pais diferentes.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)