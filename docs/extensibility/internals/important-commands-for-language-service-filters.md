---
title: Filtros de serviço de comandos importantes para o idioma | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services, filters
- language services, commands to support
ms.assetid: 4948c494-3d4d-4f50-b3f9-959e73f90e4d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1e7affdbcad2b935a05420a2817c5d8bda5cd9cf
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130646"
---
# <a name="important-commands-for-language-service-filters"></a>Comandos importantes para filtros do serviço de linguagem
Se você quiser criar um filtro de serviço com recursos de idioma, considere os seguintes comandos de tratamento. A lista completa de identificadores de comando é definida no <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> para não gerenciado de enumeração para código gerenciado e o cabeçalho de Stdidcmd.h arquivos [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] código. Você pode encontrar o arquivo Stdidcmd.h *caminho de instalação do SDK do Visual Studio*\VisualStudioIntegration\Common\Inc.  
  
## <a name="commands-to-handle"></a>Comandos para identificador  
  
> [!NOTE]
>  Não é obrigatório para filtrar todos os comandos na tabela a seguir.  
  
|Comando|Descrição|  
|-------------|-----------------|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário clica. Este comando indica que se trata de tempo para fornecer um menu de atalho. Se você não lidar com este comando, o editor de texto fornece um menu de atalho padrão sem quaisquer comandos específicos do idioma. Para incluir seus próprios comandos nesse menu, tratar o comando e exibir um menu de atalho por conta própria.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Normalmente enviado quando o usuário digitar CTRL + J. Chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método sobre o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para mostrar a caixa de conclusão de instrução.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário digita um caractere. Monitore esse comando para determinar quando um gatilho de caractere é digitado e para fornecer a instrução de conclusão, dicas de método e marcadores de texto, como coloração de sintaxe, a correspondência chaves e marcadores de erro. Chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para conclusão de instrução e o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> para obter dicas de método. Para oferecer suporte a marcadores de texto, monitore esse comando para determinar se o caractere que está sendo digitado requer que você atualize seus marcadores.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário digita a tecla Enter. Monitorar esse comando para determinar quando fechar uma janela de dica de método chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> método sobre o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>. Por padrão, a exibição de texto trata esse comando.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário digita a tecla Backspace. Monitor para determinar quando fechar uma janela de dica de método chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> método sobre o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>. Por padrão, a exibição de texto trata esse comando.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado de um menu ou uma tecla de atalho. Chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> método sobre o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para atualizar a janela de dica com as informações de parâmetro.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário passar o mouse sobre uma variável ou posiciona o cursor em uma variável e seleciona **informações rápidas** de **IntelliSense** no **editar** menu. Retorna o tipo da variável em uma dica chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> método o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>. Se a depuração estiver ativa, a dica também deve mostrar o valor da variável.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Normalmente enviado quando o usuário digitar CTRL + barra de espaços. Esse comando informa o serviço de linguagem para chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método sobre o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado de um menu, geralmente **comentário de seleção** ou **seleção Descomente** de **avançado** no **editar** menu. <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> indica que o usuário deseja comentar o texto selecionado. <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> indica que o usuário deseja remover comentário do texto selecionado. Esses comandos podem ser implementados somente pelo serviço de linguagem.|  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolver um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)