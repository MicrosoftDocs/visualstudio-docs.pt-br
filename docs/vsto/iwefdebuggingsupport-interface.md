---
title: Interface IWefDebuggingSupport
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0a4883d36c1833c66a2539380184521b070f5c2a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544723"
---
# <a name="iwefdebuggingsupport-interface"></a>Interface IWefDebuggingSupport
  Implementado por um ambiente de depuração, como o Visual Studio, para facilitar a depuração de aplicativos para o Office. O aplicativo do Office, como o Word ou o Excel, obtém essa interface do Visual Studio e, em seguida, chama métodos na interface em determinados pontos durante a sessão de depuração.

## <a name="syntax"></a>Sintaxe

```csharp
[
    uuid(ccaf1a90-ce1c-4199-9cd6-b40c5c57a671),
    oleautomation
]
interface IWefDebuggingSupport : IUnknown
{
    HRESULT SetWefProcessId(
        [in] DWORD dwProcessId);
    HRESULT GetAutoInsertExtensions(
        [out, retval] SAFEARRAY(BSTR)* psaExtensionNames);
}
```

## <a name="methods"></a>Métodos
 A tabela a seguir lista os métodos que a interface IWefDebuggingSupport define.

|Nome|Descrição|
|----------|-----------------|
|[Método GetAutoInsertExtensions](../vsto/getautoinsertextensions-method.md)|Obtém informações sobre os aplicativos para o Office que devem ser inseridos automaticamente durante a depuração.|
|[Método SetWefProcessId](../vsto/setwefprocessid-method.md)|Fornece o identificador do processo que executará o conteúdo do WEF (Web Extensions Framework).|
