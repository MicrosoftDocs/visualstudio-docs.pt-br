---
title: IActiveScriptProperty::GetProperty | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProperty.GetProperty
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetProperty method, IActiveScriptProperty interface
ms.assetid: a43383db-b148-4d76-83bd-4f0e899b7cb1
caps.latest.revision: 24
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7cd5c7ac948a9001688de69f9db9ee31624ca33d
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44284130"
---
# <a name="iactivescriptpropertygetproperty"></a>IActiveScriptProperty::GetProperty
Obtém a propriedade que é especificada pelo parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetProperty(  
// The property value:  
    uint dwProperty,    
// Not used:  
    IntPtr pvarIndex,    
// The value of the property:   
    out object pvarValue,    
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwProperty`  
 O valor de propriedade a ser obtido.  
  
 `pvarIndex`  
 Não usado.  
  
 `pvarValue`  
 O valor da propriedade.  
  
 Os valores permitidos para `dwProperty` são descritos na tabela a seguir.  
  
|Constante|Valor|Significado|  
|--------------|-----------|-------------|  
|SCRIPTPROP_INTEGERMODE|0x00003000|Força o mecanismo de script para dividir no modo de inteiro em vez do modo de ponto flutuante.|  
|SCRIPTPROP_STRINGCOMPAREINSTANCE|0x00003001|Permite que a função de comparação de cadeia de caracteres do mecanismo de script a ser substituído.|  
|SCRIPTPROP_ABBREVIATE_GLOBALNAME_RESOLUTION|0x70000002|Informa ao mecanismo de script que não há outros mecanismos de script existem para contribuir com o objeto global.|  
|SCRIPTPROP_INVOKEVERSIONING|0x00004000|Força o [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] mecanismo de script para selecionar um conjunto de recursos de linguagem com suporte. O conjunto padrão de recursos de idioma com suporte a [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] mecanismo de script é equivalente ao conjunto de recursos de linguagem que apareceu na versão 5.7 do [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] mecanismo de script.|  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_INVALIDARG`|Um argumento não é válido.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado).|  
  
## <a name="remarks"></a>Comentários  
 O host pode usar a propriedade SCRIPTPROP_ABBREVIATE_GLOBALNAME_RESOLUTION para informar ao mecanismo de script que não há outros mecanismos de script existem para contribuir com o objeto global. Por exemplo, o Internet Explorer pode informar a [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] mecanismo de que a página que está sendo renderizada contém apenas [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] scripts. Assim, somente o [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] mecanismo pode adicionar novas propriedades para a janela do objeto global e não há nenhum mecanismo de Visual Basic Scripting Edition (VBScript) para fazer o mesmo. O mecanismo pode ignorar esse sinalizador ou pode usá-lo a otimizar o gerenciamento de novos membros que são adicionados ao objeto global.  
  
 O host pode usar a propriedade SCRIPTPROP_INVOKEVERSIONING para selecionar o conjunto de recursos de linguagem a serem suportados quando o [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] mecanismo de script é iniciado. Se essa propriedade é definida como 1 (SCRIPTLANGUAGEVERSION_5_7), os recursos de linguagem disponíveis são as mesmas que apareceu na versão 5.7 do [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] mecanismo de script. Se ele for definido como 2 (SCRIPTLANGUAGEVERSION_5_8), os recursos de linguagem disponíveis são aquelas que apareceu na versão 5.7, além de recursos que foram adicionados na versão 5.8. Por padrão, essa propriedade é definida como 0 (SCRIPTLANGUAGEVERSION_DEFAULT), que é equivalente ao conjunto de recursos de linguagem que apareceu na versão 5.7, a menos que o host oferece suporte a um comportamento diferente do padrão. Por exemplo, o Internet Explorer 8 aceita a [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] recursos de linguagem compatíveis com a versão 5.8 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] mecanismo de script por padrão quando o modo de documento do Internet Explorer 8 é o modo de "Padrões do Internet Explorer 8".  
  
## <a name="see-also"></a>Consulte também  
 [Definindo a compatibilidade de documentos](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/compatibility/cc288325(v=vs.85))   
 [IActiveScriptProperty](../../winscript/reference/iactivescriptproperty.md)   
 [Informações de versão](../../javascript/reference/javascript-version-information.md)