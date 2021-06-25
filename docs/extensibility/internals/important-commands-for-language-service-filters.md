---
title: Comandos importantes para filtros de serviço de idioma | Microsoft Docs
description: Saiba mais sobre os comandos importantes que você deve dar suporte ao criar um filtro de serviço de linguagem totalmente em destaque no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- language services, filters
- language services, commands to support
ms.assetid: 4948c494-3d4d-4f50-b3f9-959e73f90e4d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8dd5f65248411a7ea6b892d5b4c800718456339f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899050"
---
# <a name="important-commands-for-language-service-filters"></a>Comandos importantes para filtros do serviço de linguagem
Se você quiser criar um filtro de serviço de linguagem totalmente em destaque, considere a manipulação dos comandos a seguir. A lista completa de identificadores de comando é definida na <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> enumeração para código gerenciado e o arquivo de cabeçalho Stdidcmd. h para código não gerenciado [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] . Você pode encontrar o arquivo Stdidcmd. h no *caminho de instalação do SDK do Visual Studio*\VisualStudioIntegration\Common\Inc.

## <a name="commands-to-handle"></a>Comandos a serem tratados

> [!NOTE]
> Não é obrigatório filtrar para cada comando na tabela a seguir.

|Comando|Descrição|
|-------------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário clica com o botão direito do mouse. Esse comando indica que é hora de fornecer um menu de atalho. Se você não tratar esse comando, o editor de texto fornecerá um menu de atalho padrão sem nenhum comando específico do idioma. Para incluir seus próprios comandos nesse menu, manipule o comando e exiba um menu de atalho por conta própria.|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Normalmente enviado quando o usuário digita CTRL + J. Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para mostrar a caixa de conclusão da instrução.|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário digita um caractere. Monitore esse comando para determinar quando um caractere de gatilho é digitado e fornecer conclusão de instrução, dicas de método e marcadores de texto, como coloração de sintaxe, correspondência de chaves e marcadores de erro. Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> conclusão da instrução for e o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> para obter dicas de método. Para dar suporte a marcadores de texto, monitore esse comando para determinar se o caractere que está sendo digitado requer que você atualize seus marcadores.|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário digita a tecla Enter. Monitore esse comando para determinar quando ignorar uma janela de dica de método chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> . Por padrão, a exibição de texto manipula esse comando.|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário digita a tecla BACKSPACE. Monitor para determinar quando ignorar uma janela de dica de método chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> . Por padrão, a exibição de texto manipula esse comando.|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado de um menu ou de uma tecla de atalho. Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para atualizar a janela tip com as informações do parâmetro.|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado quando o usuário passa o mouse sobre uma variável ou posiciona o cursor em uma variável e seleciona **informações rápidas** do **IntelliSense** no menu **Editar** . Retorne o tipo da variável em uma dica chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> . Se a depuração estiver ativa, a dica também deverá mostrar o valor da variável.|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Normalmente enviado quando o usuário digita CTRL + barra de espaços. Esse comando informa ao serviço de linguagem para chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> .|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|Enviado de um menu, normalmente **comentar seleção** ou remover marca de **Comentário** de **avançado** no menu **Editar** . <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> indica que o usuário deseja comentar o texto selecionado; <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> indica que o usuário deseja remover o comentário do texto selecionado. Esses comandos podem ser implementados somente pelo serviço de linguagem.|

## <a name="see-also"></a>Confira também
- [Desenvolvendo um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)
