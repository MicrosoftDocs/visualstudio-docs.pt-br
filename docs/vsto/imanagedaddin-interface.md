---
title: Interface IManagedAddin
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IManagedAddin interface
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b436d76164b1744cffe16593149f64d219d04bf1
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541122"
---
# <a name="imanagedaddin-interface"></a>Interface IManagedAddin
  Implemente a interface IManagedAddin para criar um componente que carregue suplementos do VSTO gerenciados. Essa interface foi adicionada no sistema de Microsoft Office de 2007.

## <a name="syntax"></a>Sintaxe

```csharp
[
    object,
    uuid(B9CEAB65-331C-4713-8410-DDDAF8EC191A),
    pointer_default(unique),
    oleautomation
]
interface IManagedAddin : IUnknown
{
    HRESULT Load(
        [in] BSTR bstrManifestURL,
        [in] IDispatch *pdispApplication);
    HRESULT Unload();
};
```

## <a name="methods"></a>Métodos
 A tabela a seguir lista os métodos que são definidos pela interface IManagedAddin.

|Name|Descrição|
|----------|-----------------|
|[IManagedAddin::Load](../vsto/imanagedaddin-load.md)|Chamado quando um aplicativo Microsoft Office carrega um suplemento VSTO gerenciado.|
|[IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)|Chamado logo antes de um Microsoft Office aplicativo descarrega um suplemento do VSTO gerenciado.|

## <a name="remarks"></a>Comentários
 Microsoft Office aplicativos, começando com o sistema de 2007 Microsoft Office, use a interface IManagedAddin para ajudar a carregar os suplementos do VSTO do Office. Você pode implementar a interface IManagedAddin para criar seu próprio carregador de suplemento do VSTO e tempo de execução para suplementos do VSTO gerenciados, em vez de usar o carregador de suplemento do VSTO (*VSTOLoader.dll*) e o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] . Para obter mais informações, consulte [arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md).

## <a name="how-managed-add-ins-are-loaded"></a>Como os suplementos gerenciados são carregados
 As etapas a seguir ocorrem quando um aplicativo é iniciado:

1. O aplicativo descobre os suplementos do VSTO procurando entradas na seguinte chave do registro:

    **HKEY_CURRENT_USER \Software\Microsoft\Office \\ *\<application name>* \Addins\\**

    Cada entrada nessa chave do registro é uma ID exclusiva do suplemento do VSTO. Normalmente, esse é o nome do assembly do suplemento do VSTO.

2. O aplicativo procura uma `Manifest` entrada sob a entrada de cada suplemento do VSTO.

    Os suplementos do VSTO gerenciados podem armazenar o caminho completo de um manifesto na `Manifest` entrada em **HKEY_CURRENT_USER \Software\Microsoft\Office \\ _\<application name>_ \Addins \\ _\<add-in ID>_ **. Um manifesto é um arquivo (normalmente, um arquivo XML) que fornece informações que são usadas para ajudar a carregar o suplemento do VSTO.

3. Se o aplicativo encontrar uma `Manifest` entrada, o aplicativo tentará carregar um componente de carregador de suplementos do VSTO gerenciado. O aplicativo faz isso tentando criar um objeto COM que implementa a interface IManagedAddin.

    O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] inclui um componente de carregador de suplemento do VSTO (*VSTOLoader.dll*) ou você pode criar o seu próprio implementando a interface IManagedAddin.

4. O aplicativo chama o método [IManagedAddin:: Load](../vsto/imanagedaddin-load.md) e passa o valor da `Manifest` entrada.

5. O método [IManagedAddin:: Load](../vsto/imanagedaddin-load.md) executa tarefas necessárias para carregar o suplemento do VSTO, como configurar o domínio do aplicativo e a política de segurança para o suplemento do VSTO que está sendo carregado.

   Para obter mais informações sobre as chaves do registro que Microsoft Office aplicativos usam para descobrir e carregar suplementos do VSTO gerenciados, consulte [entradas do registro para suplementos do VSTO](../vsto/registry-entries-for-vsto-add-ins.md).

## <a name="guidance-to-implement-imanagedaddin"></a>Diretrizes para implementar o IManagedAddin
 Se você implementar IManagedAddin, deverá registrar a DLL que contém a implementação usando o seguinte CLSID:

 99D651D7-5F7C-470E-8A3B-774D5D9536AC

 Microsoft Office aplicativos usam esse CLSID para criar o objeto COM que implementa IManagedAddin.

> [!CAUTION]
> Esse CLSID também é usado pelo *VSTOLoader.dll* no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] . Portanto, se você usar o IManagedAddin para criar seu próprio carregador de suplemento do VSTO e o componente de tempo de execução, não será possível implantar seu componente em computadores que executam suplementos do VSTO que dependem do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] .

## <a name="see-also"></a>Consulte também
- [Referência de API não gerenciada &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/unmanaged-api-reference-office-development-in-visual-studio.md)
