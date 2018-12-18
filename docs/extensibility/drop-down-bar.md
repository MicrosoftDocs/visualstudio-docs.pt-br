---
title: Barra de menu suspenso | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - drop-down bar
ms.assetid: 4bb621bd-72f5-43d5-916f-9f66617da049
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 030ee092909c7faa519c68ac9800d051a96f6b42
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39636922"
---
# <a name="drop-down-bar"></a>Barra de menu suspenso
A barra de menu suspenso é fornecida na parte superior da janela de código e contém duas listas de lista suspensa.  
  
## <a name="drop-down-bar-interfaces"></a>Interfaces de barra de menu suspenso  
 Na [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)], por exemplo, a barra de menu suspenso contém listas para [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] itens e [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] funções de membro de itens, conforme mostrado na imagem a seguir.  
  
 ![Remova&#45;para baixo de barras](../extensibility/media/vsdropdown_bar.gif "vsDropdown_bar")  
Barra de menu suspenso  
  
 Ao implementar uma barra de menu suspenso, há quatro interfaces de importância fundamental:  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarClient>  
  
     Implemente essa interface para inserir o conteúdo da barra de menu suspenso. Cada combinação de lista suspensa pode conter texto sem formatação ou texto sofisticado (negrito, sublinhado ou itálico), pode ter cores de fonte do texto de janela ou cores de fonte cinza e, opcionalmente, pode fornecer um bitmap pequeno ao lado do item de lista suspensa. Semelhante ao <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> interface, imagens de bitmap são fornecidas em listas de imagens. Cada combinação de lista suspensa pode ter uma lista de imagem diferente; No entanto, cada lista de imagens deve conter imagens da mesma altura. Além disso, usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarClient.GetComboTipText%2A> método, você pode fornecer uma dica de ferramenta para cada combinação.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager>  
  
     Chame essa interface para criar ou destruir a barra de menu suspenso para uma janela de código. Essa interface também pode ser usada para determinar se uma barra de menu suspenso já está anexada a uma janela de código chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.GetDropdownBar%2A> método. Chame <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager> de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar>  
  
     Chame essa interface para se comunicar diretamente com a barra de menu suspenso. Você pode usar essa interface para forçar uma atualização de lista suspensa da barra conteúdo ou para alterar a seleção de uma das caixas de listagem.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManagerEvents>  
  
     Se você tiver registrado o `ShowDropdownBarOption` na sua chave de registro do serviço de linguagem, em seguida, seu Gerenciador de janelas de código deve monitorar esse evento para sincronizar com as preferências do usuário sobre se a barra de menu deve ser exibida. Se você não registrar essa opção em sua chave de serviço de linguagem, então a opção para mostrar ou ocultar a barra de menu suspenso está desabilitada na **opções** menu.  
  
## <a name="attach-a-drop-down-bar-to-a-code-window"></a>Anexar uma barra de menu suspenso para uma janela de código  
 Para anexar uma barra de menu suspenso para a janela de código quando ele é criado, um serviço de linguagem deve ser anexado à lista suspensa de barra quando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> método é chamado. Se uma chamada para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.GetDropdownBar%2A> método indica que uma barra de menu suspenso ainda não existir, e então chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.AddDropdownBar%2A>. Para acessar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager> interface, chame <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> da <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> ponteiro retornado para você quando seu <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> implementação foi anexada.  
  
## <a name="see-also"></a>Consulte também  
 [Personalizar janelas de código usando a API herdada](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)   
 [Suporte para a barra de navegação em um serviço de linguagem herdado](../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)