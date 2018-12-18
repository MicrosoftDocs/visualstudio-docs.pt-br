---
title: Elemento ButtonText | Microsoft Docs
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
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 35973241d1f68965680332fb3baf7c9b13c1bbcc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51790208"
---
# <a name="buttontext-element"></a>Elemento ButtonText
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este campo permite especificar o texto que aparece em vários menus. Por padrão, o `ButtonText` elemento aparece em controladores de menu. O `ButtonText` elemento também se tornará o padrão se campos de texto estiverem em branco. O `ButtonText` elemento não pode ficar em branco, mesmo se os outros campos de texto forem especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<ButtonText>My Command</ButtonText>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
 nenhuma.  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento Strings](../extensibility/strings-element.md)|Agrupa os elementos de texto, como `ButtonText` e `CommandName`.|  
  
## <a name="text-value"></a>Valor de texto  
 O valor de texto o `ButtonText` elemento fornece o texto que é exibido para itens de menu, combos e outros elementos de (UI) de interface de usuário que tenham texto visível.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

