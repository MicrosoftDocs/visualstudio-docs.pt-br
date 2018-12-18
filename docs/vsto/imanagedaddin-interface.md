---
title: Interface IManagedAddin
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IManagedAddin interface
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ddede8542cda7499a9781c19a6baf1c58acfd125
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839538"
---
# <a name="imanagedaddin-interface"></a>Interface IManagedAddin
  Implementar a interface IManagedAddin para criar um componente que carrega gerenciados VSTO Add-ins. Essa interface foi adicionada no 2007 Microsoft Office system.  
  
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
  
|Nome|Descrição|  
|----------|-----------------|  
|[IManagedAddin::Load](../vsto/imanagedaddin-load.md)|Chamado quando um Microsoft Office aplicativo carrega um gerenciado suplemento VSTO.|  
|[IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)|Chamado pouco antes de um Microsoft Office aplicativo descarrega um gerenciado suplemento VSTO.|  
  
## <a name="remarks"></a>Comentários  
 Aplicativos do Microsoft Office, começando com o 2007 Microsoft Office system, usam a interface IManagedAddin para ajudar a carregar suplementos do VSTO do Office. Você pode implementar a interface IManagedAddin para criar seu próprio carregador de suplemento do VSTO e tempo de execução para gerenciados VSTO Add-ins, em vez de usar o carregador de suplemento do VSTO (*vstoloader. dll*) e [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Para obter mais informações, consulte [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md).  
  
## <a name="how-managed-add-ins-are-loaded"></a>Como os suplementos gerenciados são carregados  
 Quando um aplicativo é iniciado, ocorrem as seguintes etapas:  
  
1. O aplicativo descobre VSTO Add-ins procurando por entradas na seguinte chave do registro:  
  
    **HKEY_CURRENT_USER\Software\Microsoft\Office\\*\<nome do aplicativo >* \Addins\\**  
  
    Cada entrada sob essa chave do registro é uma ID exclusiva do suplemento do VSTO. Normalmente, isso é o nome do assembly do suplemento do VSTO.  
  
2. O aplicativo procura um `Manifest` entrada sob a entrada para cada suplemento do VSTO.  
  
    Gerenciado VSTO Add-ins pode armazenar o caminho completo de um manifesto na `Manifest` entrada sob **HKEY_CURRENT_USER\Software\Microsoft\Office\\_\<nome do aplicativo >_ \Addins\\  _\<suplemento ID >_**. Um manifesto é um arquivo (normalmente, um arquivo XML) que fornece informações que são usadas para ajudar a carregar o suplemento do VSTO.  
  
3. Se o aplicativo encontra uma `Manifest` entrada, o aplicativo tenta carregar um componente do carregador do suplemento do VSTO gerenciado. O aplicativo faz isso ao tentar criar um objeto COM que implementa a interface IManagedAddin.  
  
    O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] inclui um componente de carregador de suplemento do VSTO (*vstoloader. dll*), ou você pode criar seus próprios Implementando a interface IManagedAddin.  
  
4. O aplicativo chama o [IManagedAddin::Load](../vsto/imanagedaddin-load.md) método e passa o valor da `Manifest` entrada.  
  
5. O [IManagedAddin::Load](../vsto/imanagedaddin-load.md) método executa as tarefas necessárias para carregar o suplemento VSTO, como configurar a política de segurança e de domínio de aplicativo para o suplemento VSTO que está sendo carregado.  
  
   Para obter mais informações sobre o registro de chaves usado por aplicativos do Microsoft Office para descobrir e carregar gerenciadas VSTO Add-ins, consulte [entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md).  
  
## <a name="guidance-to-implement-imanagedaddin"></a>Diretrizes para implementar IManagedAddin  
 Se você implementar IManagedAddin, você deve registrar a DLL que contém a implementação por meio do seguinte CLSID:  
  
 99D651D7-5F7C-470E-8A3B-774D5D9536AC  
  
 Aplicativos do Microsoft Office usam este CLSID para criar o objeto COM que implementa IManagedAddin.  
  
> [!CAUTION]  
>  Este CLSID também é usado pelo *vstoloader. dll* no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Portanto, se você usar IManagedAddin para criar seu próprio carregador de suplemento do VSTO e o componente de tempo de execução, você não pode implantar seu componente para computadores que estão executando suplementos do VSTO que dependem de [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API não gerenciada &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/unmanaged-api-reference-office-development-in-visual-studio.md)  
  
  