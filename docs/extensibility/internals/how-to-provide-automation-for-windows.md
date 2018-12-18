---
title: 'Como: fornecer automação para Windows | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d9158ac7d133d30ae5fbca0281cbc55138e041f6
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39510732"
---
# <a name="how-to-provide-automation-for-windows"></a>Como: fornecer automação para windows
Você pode fornecer automação para janelas de documento e ferramenta. Fornecer automação é recomendável sempre que você deseja disponibilizar os objetos de automação em uma janela, e o ambiente já não fornecem um objeto de automação prontas para uso, como ocorre com uma lista de tarefas.

## <a name="automation-for-tool-windows"></a>Automação das janelas de ferramentas
 O ambiente fornece automação em uma janela de ferramentas, retornando um padrão <xref:EnvDTE.Window> objeto conforme explicado no procedimento a seguir:

### <a name="to-provide-automation-for-tool-windows"></a>Fornecer automação para janelas de ferramentas

1.  Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> método por meio do ambiente com <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> como `VSFPROPID` para obter o `Window` objeto.

2.  Quando um chamador solicita um objeto de automação de VSPackage específico para sua janela da ferramenta por meio <xref:EnvDTE.Window.Object%2A>, as chamadas de ambiente `QueryInterface` para `IExtensibleObject`, <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>, ou o `IDispatch` interfaces. Ambos `IExtensibleObject` e `IVsExtensibleObject` fornecem um <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A> método.

3.  Quando o ambiente, em seguida, chama o `GetAutomationObject` método passando `NULL`, responder, passando de volta o objeto específico do VSPackage.

4.  Se chamar `QueryInterface` para `IExtensibleObject` e `IVsExtensibleObject` falhar, então, o ambiente chama `QueryInterface` para `IDispatch`.

## <a name="automation-for-document-windows"></a>Automação para janelas de documento
 Um padrão <xref:EnvDTE.Document> objeto também está disponível no ambiente, embora um editor pode ter sua própria implementação do <xref:EnvDTE.Document> objeto implementando `IExtensibleObject` interface e respondendo a `GetAutomationObject`.

 Além disso, um editor pode fornecer um objeto de automação específicos de VSPackage, recuperado por meio de <xref:EnvDTE.Document.Object%2A> método, Implementando o `IVsExtensibleObject` ou `IExtensibleObject` interfaces. O [exemplos de VSSDK](http://aka.ms/vs2015sdksamples) contribui com um objeto de automação específicos do documento RTF.

## <a name="see-also"></a>Consulte também
    
<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>