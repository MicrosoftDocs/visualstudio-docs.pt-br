---
title: Interfaces e campos da janela Propriedades | Microsoft Docs
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
- Properties window, fields and interfaces
ms.assetid: 0328f0e5-2380-4a7a-a872-b547cb775050
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8b9e7705af131bdc8c81b6cbeeac3ed4dda80aa4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51721031"
---
# <a name="properties-window-fields-and-interfaces"></a>Interfaces e campos da janela Propriedades
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O modelo para a seleção determinar quais informações são exibidas na **propriedades** janela baseia-se na janela que tem o foco no IDE. Cada janela e o objeto dentro da janela selecionada, podem ter seu objeto de contexto de seleção enviados por push para o contexto da seleção global. O ambiente atualiza o contexto da seleção global com valores de um quadro de janela quando essa janela tem o foco. Quando o foco é alterado, portanto, não o contexto da seleção.  
  
## <a name="tracking-selection-in-the-ide"></a>Seleção do controle no IDE  
 O quadro de janela ou site, pertencentes a IDE, tem um serviço chamado <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>. As etapas a seguir mostram como uma alteração em uma seleção, causada pelo usuário alterando o foco para outra janela aberta ou selecionando um item de projeto diferente em **Gerenciador de soluções**, é implementado para alterar o conteúdo exibido na  **Propriedades** janela.  
  
1. O objeto criado pelo VSPackage que é localizado em chamadas a janela selecionada <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> ter <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> invocar <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>.  
  
2. O contêiner de seleção, fornecido pela janela selecionada, cria seu próprio <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> objeto. Quando a seleção é alterada, o VSPackage chama <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> notificar todos os ouvintes no ambiente, incluindo o **propriedades** janela, da alteração. Ele também fornece acesso às informações de hierarquia e de item relacionados à nova seleção.  
  
3. Chamando <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> e passando-os itens da hierarquia selecionada na `VSHPROPID_BrowseObject` parâmetro preenche o <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> objeto.  
  
4. Um objeto derivado de [IDispatch Interface](http://msdn.microsoft.com/en-us/ebbff4bc-36b2-4861-9efa-ffa45e013eb5) é retornado para <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> para o item solicitado e o ambiente encapsula-o em um <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> (consulte a etapa a seguir). Se a chamada falhar, o ambiente torna uma segunda chamada para `IVsHierarchy::GetProperty`, passando-o contêiner de seleção <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> que forneçam o item de hierarquia ou itens.  
  
    Seu projeto de VSPackage não cria <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> como a janela fornecida pelo ambiente de VSPackage que o implementa (por exemplo, **Gerenciador de soluções**) constrói <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> em seu nome.  
  
5. O ambiente chama os métodos do <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> para obter os objetos com base em de `IDispatch` interface para preencher o **propriedades** janela.  
  
   Quando um valor na **propriedades** janela for alterada, implementar os VSPackages `IVsTrackSelectionEx::OnElementValueChangeEx` e `IVsTrackSelectionEx::OnSelectionChangeEx` para relatar a alteração para o valor do elemento. O ambiente, em seguida, invoca <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ou <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> para manter as informações exibidas na **propriedades** janela sincronizados com os valores de propriedade. Para obter mais informações, consulte [atualizando valores de propriedade na janela propriedades](../../misc/updating-property-values-in-the-properties-window.md).  
  
   Além de selecionar uma opção diferente de item de projeto no **Gerenciador de soluções** para exibir as propriedades relacionadas a esse item, você também pode escolher um objeto diferente de dentro de uma janela de formulário ou documento usando a lista suspensa disponível no **Propriedades** janela. Para obter mais informações, consulte [lista de objetos de janela de propriedades](../../extensibility/internals/properties-window-object-list.md).  
  
   Você pode alterar o modo de exibição de informações na **propriedades** grade da janela de em ordem alfabética em categórica, e, se disponível, você também pode abrir uma página de propriedades para um objeto selecionado clicando nos botões apropriados na  **Propriedades** janela. Para obter mais informações, consulte [botões da janela propriedades](../../extensibility/internals/properties-window-buttons.md) e [páginas de propriedade](../../extensibility/internals/property-pages.md).  
  
   Por fim, a parte inferior da **propriedades** janela também contém uma descrição do campo selecionado na **propriedades** grade da janela. Para obter mais informações, consulte [obtendo descrições do campo da janela propriedades](../../misc/getting-field-descriptions-from-the-properties-window.md).  
  
## <a name="see-also"></a>Consulte também  
 [Estender as propriedades](../../extensibility/internals/extending-properties.md)

