---
title: IManagedAddin::Load
description: Chamado quando um suplemento do VSTO gerenciado é carregado.
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords: ''
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: fc89ba13e9fc0f62b264cdb926e1a8392c0b41bd
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102469756"
---
# <a name="imanagedaddinload"></a>IManagedAddin::Load
  Chamado quando um suplemento do VSTO gerenciado é carregado.

## <a name="syntax"></a>Sintaxe

```csharp
HRESULT Load([in] BSTR bstrManifestURL,
             [in] IDispatch *pdispApplication);
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------------|-----------------|
|*bstrManifestURL*|O caminho completo do manifesto para o suplemento do VSTO.|
|*pdispApplication*|Um ponteiro para um IDispatch que representa o aplicativo host que está carregando o suplemento do VSTO.|

## <a name="return-value"></a>Valor Retornado
 Um valor HRESULT que indica se o método foi concluído com êxito.

## <a name="remarks"></a>Comentários
 Um manifesto é um arquivo (normalmente, um arquivo XML) que fornece informações que são usadas para ajudar a carregar o suplemento do VSTO. Por exemplo, um manifesto pode especificar o local do assembly do suplemento do VSTO e a classe do ponto de entrada para instanciar quando o suplemento do VSTO for carregado.

 O parâmetro *bstrManifestURL* contém o valor da `Manifest` entrada na chave do registro **HKEY_CURRENT_USER\Software\Microsoft\Office\\ _\<application name>_ \Addins \\ _\<add-in ID>_** para o suplemento do VSTO. Para obter mais informações, consulte [interface IManagedAddin](../vsto/imanagedaddin-interface.md).

 Implemente o método [IManagedAddin:: Load](../vsto/imanagedaddin-load.md) para executar tarefas como configurar o domínio do aplicativo e a política de segurança para o suplemento do VSTO que está sendo carregado.

## <a name="see-also"></a>Confira também
- [Interface IManagedAddin](../vsto/imanagedaddin-interface.md)
- [IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)
