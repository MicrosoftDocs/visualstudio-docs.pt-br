---
title: IDispatchEx::InvokeEx | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.InvokeEx
apilocation:
- scrobj.dll
helpviewer_keywords:
- InvokeEx method
ms.assetid: d90783e6-4b89-4423-8a56-a9c8b4b2c813
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6302228b110e2b0a6296190079bf60b3d92980bd
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24730076"
---
# <a name="idispatchexinvokeex"></a>IDispatchEx::InvokeEx
Fornece acesso às propriedades e métodos expostos por um `IDispatchEx` objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT InvokeEx(  
   DISPID id,  
   LCID lcid,  
   WORD wFlags,  
   DISPARAMS *pdp,  
   VARIANT *pVarRes,   
   EXCEPINFO *pei,   
   IServiceProvider *pspCaller   
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `id`  
 Identifica o membro. Usa `GetDispID` ou `GetNextDispID` para obter o identificador de distribuição.  
  
 `lcid`  
 O contexto de localidade no qual interpretar argumentos. O `lcid` é passado para `InvokeEx` para permitir que o objeto interpretar os argumentos para uma localidade específicos.  
  
 `wFlags`  
 Valores legais para `wFlags` são:  
  
 DISPATCH_PROPERTYGET &#124; DISPATCH_METHOD &#124; DISPATCH_PROPERTYPUT &#124; DISPATCH_PROPERTYPUTREF &#124; DISPATCH_CONSTRUCT  
  
 Sinalizadores que descrevem o contexto da `InvokeEx` chamar:  
  
|Valor|Significado|  
|-----------|-------------|  
|DISPATCH_METHOD|O membro é um método invocado. Se uma propriedade tiver o mesmo nome, isso e o sinalizador DISPATCH_PROPERTYGET pode ser definido (definido pelo `IDispatch`).|  
|DISPATCH_PROPERTYGET|O membro é recuperado como um propriedade ou membro de dados (definidos por `IDispatch`).|  
|DISPATCH_PROPERTYPUT|O membro é alterado como um propriedade ou membro de dados (definidos por `IDispatch`).|  
|DISPATCH_PROPERTYPUTREF|O membro é alterado por uma atribuição de referência em vez de uma atribuição de valor. Esse sinalizador é válido somente quando a propriedade aceita uma referência a um objeto (definido pelo `IDispatch`).|  
|DISPATCH_CONSTRUCT|O membro está sendo usado como um construtor. (Este é um novo valor definido por `IDispatchEx`). Valores legais para `wFlags` são:<br /><br /> DISPATCH_PROPERTYGET DISPATCH_METHOD DISPATCH_PROPERTYPUT DISPATCH_PROPERTYPUTREF DISPATCH_CONSTRUCT|  
  
 `pdp`  
 Ponteiro para uma estrutura contendo uma matriz de argumentos, uma matriz de DISPIDs de argumento para argumentos nomeados e contagens para o número de elementos nas matrizes. Consulte o `IDispatch` documentação para obter uma descrição completa da estrutura de DISPPARAMS.  
  
 `pVarRes`  
 Ponteiro para o local onde o resultado será armazenado ou nulo se o chamador não espera que nenhum resultado. Esse argumento será ignorado se DISPATCH_PROPERTYPUT ou DISPATCH_PROPERTYPUTREF é especificado.  
  
 `pei`  
 Ponteiro para uma estrutura que contém informações de exceção. Essa estrutura deve ser preenchida se `DISP_E_EXCEPTION` é retornado. Pode ser Null. Consulte o `IDispatch` documentação para obter uma descrição completa de `EXCEPINFO` estrutura.  
  
 `pspCaller`  
 Ponteiro para um objeto de provedor de serviço fornecido pelo chamador, que permite que o objeto obter os serviços do chamador. Pode ser Null.  
  
 `IDispatchEx::InvokeEx`fornece todos os mesmos recursos `IDispatch::Invoke` e adiciona algumas extensões:  
  
|||  
|-|-|  
|DISPATCH_CONSTRUCT|Indica que o item está sendo usado como um construtor.|  
|`pspCaller`|O `pspCaller` permite o acesso de objeto para os serviços fornecidos pelo chamador. Serviços específicos podem ser tratados pelo chamador em si ou delegados para chamadores ainda mais a cadeia de chamada. Por exemplo, se um mecanismo de script dentro de um navegador faz uma `InvokeEx` chamada para um objeto externo, o objeto pode seguir o `pspCaller` cadeia para obter os serviços do mecanismo de script ou navegador. (Observe que a cadeia de chamada não é o mesmo que a cadeia de criação — também conhecido como a cadeia de contêiner ou a cadeia de site. A cadeia de criação pode estar disponível por meio de outro mecanismo, como `IObjectWithSite`.)|  
|Ponteiro `this`|Quando DISPATCH_METHOD é definida na `wFlags`, pode haver um "parâmetro nomeado" para o valor "this". O DISPID será DISPID_THIS e ele deve ser o primeiro parâmetro nomeado.|  
  
 Não usada `riid` parâmetro `IDispatch::Invoke` foi removido.  
  
 O `puArgArr` parâmetro `IDispatch::Invoke` foi removido.  
  
 Consulte o `IDispatch::Invoke` documentação para os exemplos a seguir:  
  
 "Chamando um método sem argumentos"  
  
 "Obter e definir propriedades"  
  
 "Passando parâmetros de"  
  
 "Propriedades indexadas"  
  
 "Gerar exceções durante Invoke"  
  
 "Retornando erros"  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|||  
|-|-|  
|`S_OK`|Êxito.|  
|DISP_E_BADPARAMCOUNT|O número de elementos fornecido para DISPPARAMS é diferente do número de argumentos aceitos pelo método ou propriedade.|  
|DISP_E_BADVARTYPE|Um dos argumentos em `rgvarg` não é um tipo de variável válido.|  
|DISP_E_EXCEPTION|O aplicativo deve gerar uma exceção. Nesse caso, a estrutura é passado no `pei` devem ser preenchidos.|  
|DISP_E_MEMBERNOTFOUND|O membro solicitado não existe, ou a chamada para `InvokeEx` tentou definir o valor de uma propriedade somente leitura.|  
|DISP_E_NONAMEDARGS|Essa implementação de `IDispatch` não dá suporte a argumentos nomeados.|  
|DISP_E_OVERFLOW|Um dos argumentos em `rgvarg` não pôde ser forçado para o tipo especificado.|  
|DISP_E_PARAMNOTFOUND|Um dos parâmetros DISPIDs não corresponde a um parâmetro no método.|  
|DISP_E_TYPEMISMATCH|Não foi possível forçar um ou mais argumentos.|  
|DISP_E_UNKNOWNLCID|O membro que está sendo invocado interpreta argumentos da cadeia de acordo com o LCID e o LCID não é reconhecido. Se o LCID não é necessária para interpretar os argumentos, esse erro não deve ser retornado.|  
|DISP_E_PARAMNOTOPTIONAL|Um parâmetro necessário foi omitido.|  
  
## <a name="example"></a>Exemplo  
  
```  
VARIANT var;  
   BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;  
   DISPPARAMS dispparamsNoArgs = {NULL, NULL, 0, 0};  
  
   // Assign to pdex and bstrName  
   if (SUCCEEDED(pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid)))  
   {  
      pdex->InvokeEx(dispid, LOCALE_USER_DEFAULT,  
         DISPATCH_PROPERTYGET, &dispparamsNoArgs,   
         &var, NULL, NULL);  
   }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDispatchEx](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)