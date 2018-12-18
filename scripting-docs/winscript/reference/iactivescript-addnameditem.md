---
title: IActiveScript::AddNamedItem | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.AddNamedItem
apilocation:
- scrobj.dll
helpviewer_keywords:
- AddNamedItem method, IActiveScript interface
ms.assetid: a7c6317d-948f-4bb3-b169-1bbe5b7c7cc5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: db65361e4bde14e803d9085a4530a505ccaf9fcb
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24642016"
---
# <a name="iactivescriptaddnameditem"></a>IActiveScript::AddNamedItem
Adiciona o nome de um item de nível raiz ao espaço para nome do mecanismo de script. Um item de nível raiz é um objeto com propriedades e métodos, uma fonte de evento ou todos os três.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT AddNamedItem(  
    LPCOLESTR pstrName,  // address of item name  
    DWORD dwFlags          // item flags  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstrName`  
 [in] Endereço de um buffer que contém o nome do item conforme exibido a partir do script. O nome deve ser exclusivo e persistente.  
  
 `dwFlags`  
 [in] Sinalizadores associados a um item. Pode ser uma combinação desses valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|SCRIPTITEM_CODEONLY|Indica que o item nomeado representa um objeto somente código e que o host não tem `IUnknown` a ser associado este objeto somente código. O host tem apenas um nome para este objeto. Em idiomas orientada a objeto, como C++, este sinalizador pode criar uma classe. Nem todos os idiomas oferecem suporte a esse sinalizador.|  
|SCRIPTITEM_GLOBALMEMBERS|Indica que o item é uma coleção de propriedades globais e os métodos associados com o script. Normalmente, um mecanismo de script deve ignorar o nome do objeto (em vez de com a finalidade de usá-lo como um cookie para o [IActiveScriptSite::GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md) método, ou para a resolução de escopo explícito) e expor seus membros como global variáveis e métodos. Isso permite que o host estender a biblioteca (funções de tempo de execução e assim por diante) disponível para o script. Ele é da esquerda para o mecanismo de script para lidar com o nome está em conflito (por exemplo, quando dois itens SCRIPTITEM_GLOBALMEMBERS tem métodos de mesmo nome), embora não deve ser retornado um erro devido a essa situação.|  
|SCRIPTITEM_ISPERSISTENT|Indica que o item deve ser salvo se o mecanismo de script é salvo. Da mesma forma, defina esse sinalizador indica que uma transição para o estado inicializado deve reter informações nome e o tipo do item (o mecanismo de script deve, porém, liberar todos os ponteiros para interfaces no objeto real).|  
|SCRIPTITEM_ISSOURCE|Indica que o item de fontes de eventos que o script pode coletar. Os objetos filho (Propriedades do objeto em si objetos) também podem fonte de eventos para o script. Isso não é recursiva, mas ele fornece um mecanismo prático para o caso comum, por exemplo, de criação de um contêiner e todos os seus membros controles.|  
|SCRIPTITEM_ISVISIBLE|Indica que o nome do item está disponível no espaço para nome do script, permitindo o acesso para as propriedades, métodos e eventos do item. Por convenção, as propriedades do item incluem filhos do item; Portanto, todas as propriedades do objeto filho e métodos (e seus filhos, recursivamente) poderá ser acessado.|  
|SCRIPTITEM_NOCODE|Indica que o item é simplesmente um nome que está sendo adicionado ao espaço para nome do script e não deve ser tratado como um item para o qual código deve ser associado. Por exemplo, sem esse sinalizador definido, VBScript criará um módulo separado para o objeto nomeado e C++ pode criar uma classe wrapper separado para o objeto nomeado.|  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado).|  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript](../../winscript/reference/iactivescript.md)