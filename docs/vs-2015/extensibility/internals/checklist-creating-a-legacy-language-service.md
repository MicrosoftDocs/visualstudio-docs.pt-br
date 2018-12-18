---
title: 'Lista de verificação: Criar um serviço de linguagem herdado | Microsoft Docs'
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
- language services
- language services, native code
ms.assetid: 8b73b341-a33a-4ab5-9390-178c9e563d2d
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 330270b34d55e88c883b9d8a6270b4abad02d9c1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782980"
---
# <a name="checklist-creating-a-legacy-language-service"></a>Lista de verificação: criando um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A lista de verificação a seguir resume as etapas básicas que você deve executar para criar um serviço de linguagem para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] editor de núcleo. Integre seu serviço de linguagem em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], você deve criar um avaliador de expressão de depuração. Para obter mais informações, consulte [escrever um avaliador de expressão de CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md) na [extensibilidade do depurador do Visual Studio](../../extensibility/debugger/visual-studio-debugger-extensibility.md).  
  
## <a name="steps-for-creating-a-language-service"></a>Etapas para criar um serviço de linguagem  
  
1.  Implementar a interface <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>.  
  
    -   O VSPackage, implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> interface para fornecer o serviço de linguagem.  
  
    -   Disponibilizar seu serviço de linguagem para o ambiente de desenvolvimento integrado (IDE) no seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> implementação.  
  
2.  Implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface na classe de serviço de idioma principal.  
  
     O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface é o ponto de partida de interação entre o editor principal e o serviço de linguagem.  
  
### <a name="optional-features"></a>Recursos opcionais  
 Os recursos a seguir são opcionais e podem ser implementados em qualquer ordem. Esses recursos aumentam a funcionalidade do seu serviço de linguagem.  
  
- Coloração de sintaxe  
  
   Implementar a interface <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>. As informações do analisador para retornar as informações de cor apropriado deve ser sua implementação dessa interface.  
  
   O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> método retorna o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> interface. Uma instância de colorizador separada é criada para cada buffer de texto, portanto, você deve implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> interface separadamente. Para obter mais informações, consulte [coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md).  
  
- Janela de código  
  
   Implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> interface para habilitar o serviço de linguagem receber uma notificação quando uma nova janela de código é criado.  
  
   O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> método retorna o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> interface. O serviço de linguagem, em seguida, pode adicionar a interface do usuário especial na janela de código <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A>. O serviço de linguagem também pode fazer qualquer processamento especial, como a adição de um filtro de exibição de texto em <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.OnNewView%2A>.  
  
- Filtro de exibição de texto  
  
   Para fornecer o preenchimento de declaração do IntelliSense em um serviço de linguagem, você deve interceptar alguns dos comandos que trataria a exibição de texto. Para interceptar esses comandos, conclua as seguintes etapas:  
  
  - Implemente <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> participar os comandos de editor de cadeia e o identificador de comando.  
  
  - Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método e passar em seu <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> implementação.  
  
  - Chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RemoveCommandFilter%2A> método ao desanexar do modo de exibição para que esses comandos não são passados para você.  
  
    Comandos que devem ser tratados dependem os serviços que são fornecidos. Para obter mais informações, consulte [comandos importantes para filtros do serviço de linguagem](../../extensibility/internals/important-commands-for-language-service-filters.md).  
  
  > [!NOTE]
  >  O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> interface deve ser implementada no mesmo objeto como o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface.  
  
- Conclusão da instrução  
  
   Implementar a interface <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>.  
  
   Suporte para o comando de conclusão de instrução (ou seja, <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>) e chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface, passando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> interface. Para obter mais informações, consulte [preenchimento de declaração em um serviço de linguagem herdado](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md).  
  
- Dicas de método  
  
   Implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> interface para fornecer dados para a janela de dica de método.  
  
   Instale o filtro de exibição de texto para manipular comandos apropriadamente, para que você saiba quando mostrar uma janela de dica de dados do método. Para obter mais informações, consulte [informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md).  
  
- Marcadores de erro  
  
   Implementar a interface <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>.  
  
   O erro de criação de objetos de marcador que implementam o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface e a chamada a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> método, passando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface do objeto de marcador de erro.  
  
   Normalmente, cada marcador de erro gerencia um item na janela de lista de tarefas.  
  
- Itens de lista de tarefas  
  
   Implementar uma classe de item de tarefa fornecendo o <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskItem> interface.  
  
   Implementar uma classe de provedor de tarefa fornecendo o <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider> interface e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2> interface.  
  
   Implementar uma classe de enumerador de tarefa fornecendo o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumTaskItems> interface.  
  
   Registrar o provedor de tarefa com a lista de tarefas <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RegisterTaskProvider%2A> método.  
  
   Obter o <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> interface chamando o provedor de serviço do serviço de linguagem com o GUID do serviço <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList>.  
  
   Criar objetos de item de tarefa e a chamada a <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RefreshTasks%2A> método no <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> interface quando há novas ou tarefas atualizadas.  
  
- Itens de tarefas de comentário  
  
   Use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> interface e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> interface para obter tokens de tarefa de comentário.  
  
   Obter um <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> da interface do <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> service.  
  
   Obter o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> da interface do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo.EnumTokens%2A> método.  
  
   Implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskListEvents> interface para ouvir alterações na lista de token.  
  
- Estrutura de tópicos  
  
   Há várias opções para dar suporte a estrutura de tópicos. Por exemplo, você pode dar suporte a **recolher para definições de** de comando, fornecer regiões controlado pelo editor de estrutura de tópicos ou suporte a regiões controlado pelo cliente. Para obter mais informações, consulte [como: fornecer expandido de estrutura de tópicos suporte em um serviço de linguagem herdado](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md).  
  
- Registro do serviço de linguagem  
  
   Para obter mais informações sobre como registrar um serviço de linguagem, consulte [registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service2.md) e [gerenciar VSPackages](../../extensibility/managing-vspackages.md).  
  
- Ajuda contextual  
  
   Fornece contexto para o editor em uma das seguintes maneiras:  
  
  -   Fornecer contexto para os marcadores de texto, Implementando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> interface.  
  
  Fornecer todo o contexto de usuário ao implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> interface.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolver um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)   
 [Escrevendo um avaliador de expressão do CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

