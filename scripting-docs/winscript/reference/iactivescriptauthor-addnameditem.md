---
title: IActiveScriptAuthor::AddNamedItem | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.AddNamedItem
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::AddNamedItem
ms.assetid: 951003b6-1c4a-4086-b7ce-2f128e007280
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 83d2597f8468bb97d20da655a56a751191ec4b55
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645606"
---
# <a name="iactivescriptauthoraddnameditem"></a>IActiveScriptAuthor::AddNamedItem
Adiciona o nome de um item de nível raiz para o namespace do mecanismo de criação de script. Um *item de nível raiz* é um objeto que pode conter propriedades e métodos, e também podem conter uma fonte de evento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT AddNamedItem(  
   LPCOLESTR          pszName,  
   DWORD              dwFlags,  
   IDispatch          *pdisp  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pszName`  
 [in] O nome do item conforme exibido a partir do script. O nome deve ser exclusivo e persistente.  
  
 `dwFlags`  
 [in] Os sinalizadores que estão associados ao item nomeado. Pode ser uma combinação dos seguintes valores:  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|SCRIPTITEM_ISVISIBLE|0x00000002|Indica que o nome do item está disponível no namespace do script. Isso permite o acesso a propriedades, métodos e eventos do item.<br /><br /> Por convenção, as propriedades do item de incluem os membros filho do item. Portanto, todas as propriedades do objeto filho e métodos (e seus membros filho, recursivamente) são acessíveis.|  
|SCRIPTITEM_ISSOURCE|0x00000004|Indica eventos da origem do item que o script pode ter manipuladores de eventos de script.|  
|SCRIPTITEM_GLOBALMEMBERS|0x00000008|Indica que o item é uma coleção de propriedades e métodos que estão associados com o script globais. Seus membros são criados como métodos e as variáveis globais.|  
|SCRIPTITEM_ISPERSISTENT|0x00000040|Indica que o item deve ser salvo se o mecanismo de criação de script é salvo.|  
|SCRIPTITEM_CODEONLY|0x00000200|Indica que o item nomeado representa um objeto somente código e não tem um membro para criar.|  
|SCRIPTITEM_NOCODE|0x00000400|Indica que o objeto nomeado é apenas um nome que está sendo adicionado e não tem nada a criar.|  
  
 `pdisp`  
 [in] O `IDispatch` do `NamedItem` objeto que é usado para coletar os métodos, propriedades ou a origem do evento.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Interface IActiveScriptAuthor](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor::RemoveNamedItem](../../winscript/reference/iactivescriptauthor-removenameditem.md)