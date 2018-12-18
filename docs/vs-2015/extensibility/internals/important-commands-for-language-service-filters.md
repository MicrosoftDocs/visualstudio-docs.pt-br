---
title: Filtros de serviço de comandos importantes para idioma | Microsoft Docs
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
- language services, filters
- language services, commands to support
ms.assetid: 4948c494-3d4d-4f50-b3f9-959e73f90e4d
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 2c99fdefdd8a215be04bb16b88f56be56b7fff67
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787082"
---
# <a name="important-commands-for-language-service-filters"></a>Comandos importantes para filtros do serviço de linguagem
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Se você quiser criar um filtro de serviço de linguagem com recursos completos, considere a manipulação de comandos a seguir. A lista completa de identificadores de comando é definida na <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> enumeração para código gerenciado e o cabeçalho Stdidcmd.h do arquivo para não gerenciado [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] código. Você pode encontrar o arquivo Stdidcmd.h na *caminho de instalação do SDK do Visual Studio*\visualstudiointegration\common\inc.  
  
## <a name="commands-to-handle"></a>Comandos para identificador  
  
> [!NOTE]
>  Não é obrigatório para filtrar todos os comandos na tabela a seguir.  
  
|Comando|Descrição|  
|-------------|-----------------|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário clica. Este comando indica que é hora de fornecer um menu de atalho. Se você não tratar esse comando, o editor de texto fornece um menu de atalho padrão sem quaisquer comandos específicos do idioma. Para incluir seus próprios comandos nesse menu, lidar com o comando e exibir um menu de atalho por conta própria.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Normalmente, enviadas quando o usuário digita CTRL + J. Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para mostrar a caixa de conclusão de instrução.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário digita um caractere. Monitore esse comando para determinar quando um caractere disparador for digitado e para fornecer a instrução de conclusão, dicas de método e marcadores de texto, como coloração de sintaxe, correspondência de chaves e marcadores de erro. Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para conclusão da instrução e o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> para obter dicas de método. Para dar suporte a marcadores de texto, monitore esse comando para determinar se o caractere que está sendo digitado requer que você atualize seus marcadores.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário digita a tecla Enter. Monitorar esse comando para determinar quando deve ignorar uma janela de dica de método chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>. Por padrão, a exibição de texto manipula esse comando.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário digita a tecla Backspace. Monitor para determinar quando deve ignorar uma janela de dica de método chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>. Por padrão, a exibição de texto manipula esse comando.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado de um menu ou uma tecla de atalho. Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para atualizar a janela de dica com as informações de parâmetro.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário passa o mouse sobre uma variável ou posiciona o cursor em uma variável e seleciona **informações rápidas** de **IntelliSense** no **editar** menu. Retorna o tipo da variável em uma dica chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>. Se a depuração estiver ativa, a dica também deve mostrar o valor da variável.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Normalmente, enviadas quando o usuário digita CTRL + espaço. Este comando informa o serviço de linguagem para chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado de um menu, normalmente **seleção como comentário** ou **Descomente seleção** do **avançado** no **editar** menu. <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> indica que o usuário deseja comentar o texto selecionado. <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> indica que o usuário deseja remover os comentários do texto selecionado. Esses comandos podem ser implementados somente pelo serviço de linguagem.|  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolver um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)

