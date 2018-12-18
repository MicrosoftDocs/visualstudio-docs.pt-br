---
title: 'Como: fornecer contexto para editores | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - provide context
ms.assetid: 12df4d06-df6b-4eaf-a7bf-c83655a0c683
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 848778506bdea1b7bf61b6a94a1fb14908a7b930
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49908894"
---
# <a name="how-to-provide-context-for-editors"></a>Como: fornecer contexto para editores
Para um editor, o contexto está ativo somente quando o editor tem o foco ou imediatamente antes do foco foi movido para uma janela de ferramentas tinha o foco. Você pode fornecer contexto para um editor, fazendo as seguintes tarefas:  
  
1. Crie um recipiente de contexto.  
  
2. Publica o recipiente de contexto para o identificador de elemento de seleção (SEID).  
  
3. Manter o contexto no recipiente de.  
  
   Essas tarefas são cobertas pelos procedimentos a seguir. Para obter mais informações sobre como fornecer o contexto, consulte **programação robusta** mais adiante neste artigo.  
  
## <a name="to-create-a-context-bag-for-an-editor-or-a-designer"></a>Para criar um recipiente de contexto para um editor ou designer  
  
1.  Chame `QueryService` em seu <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> interface para o <xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext> service.  
  
     Um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext> interface será retornado.  
  
2.  Chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext.CreateEmptyContext%2A> método para criar um novo recipiente de contexto ou subcontexto.  
  
     Um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext> interface será retornado.  
  
3.  Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A> método para adicionar atributos, palavras-chave de pesquisa, ou **F1** palavras-chave para o recipiente de contexto ou subcontexto.  
  
4.  Se você estiver criando um recipiente de subcontexto, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddSubcontext%2A> método para vincular o recipiente de subcontexto ao recipiente de contexto de pai.  
  
5.  Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A> para receber uma notificação quando o **ajuda dinâmica** janela está prestes a atualizar.  
  
     Ter o **ajuda dinâmica** janela chamar seu editor quando ele estiver pronto para atualizar lhe dá a oportunidade de atraso até que a atualização ocorre como alterar o contexto. Isso pode melhorar o desempenho, porque ele permite que você atrasar a execução demorados algoritmos até que o tempo ocioso do sistema está disponível.  
  
## <a name="to-publish-the-context-bag-to-the-seid"></a>Para publicar o recipiente de contexto para o SEID  
  
1.  Chamar `QueryService` sobre o <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> serviço para retornar um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> interface.  
  
2.  Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>, especificando um identificador de elemento (`elementid` parâmetro) valor de SEID_UserContext para indicar que você está passando o contexto para o nível global.  
  
3.  Quando o editor ou designer fica ativa, os valores em seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> objeto são propagadas para a seleção global. Você só precisa concluir esse processo uma vez por sessão e, em seguida, armazenar o ponteiro para o contexto global criado quando você chamou <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>.  
  
## <a name="to-maintain-the-context-bag"></a>Para manter o recipiente de contexto  
  
1.  Implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext> para garantir que o **ajuda dinâmica** janela chama o editor ou designer antes que ela seja atualizada.  
  
     Para cada pacote de contexto que chamou <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A> depois que o recipiente de contexto é criado e implementou <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate>, as chamadas IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A> para notificar o provedor de contexto que o recipiente de contexto será atualizado. Você pode usar essa chamada para alterar os atributos e palavras-chave no recipiente de contexto e, em qualquer sacos subcontexto, antes de **ajuda dinâmica** janela atualização ocorrer.  
  
2.  Chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A> no recipiente de contexto para indicar que o editor ou designer tem o novo contexto.  
  
     Quando o **ajuda dinâmica** janela chamadas <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A> para indicar que ele está sendo atualizado, o editor ou designer pode atualizar o contexto corretamente para o recipiente de contexto de pai e qualquer recipientes de subcontexto nesse momento.  
  
    > [!NOTE]
    >  O `SetDirty` sinalizador é definido automaticamente como `true` sempre que o contexto é adicionado ou removido do recipiente de contexto. O **ajuda dinâmica** janela só chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A> no conjunto de contexto se o `SetDirty` sinalizador é definido como `true`. Ele é redefinido para `false` após a atualização.  
  
3.  Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A> para adicionar contexto à coleção de contexto ativo ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.RemoveAttribute%2A> para remover o contexto.  
  
## <a name="robust-programming"></a>Programação robusta  
 Se você estiver escrevendo seu próprio editor, você deve concluir todas as três dos procedimentos neste artigo para fornecer contexto para o editor.  
  
> [!NOTE]
>  Para ativar corretamente uma janela do editor ou designer e certifique-se de que o roteamento de comando é atualizado corretamente, você deve chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> no componente para torná-lo a janela de foco.  
  
 O SEID é uma coleção de propriedades que são alteradas com base na seleção. Informações de SEID estão disponíveis por meio da seleção global. A seleção global é conectados com eventos disparados pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> interface, e tem uma lista de tudo que está selecionado (editor atual, a janela de ferramentas atual, hierarquia atual e assim por diante).  
  
 Para editores e designers, no qual contexto pode ser alterado sempre que o cursor se move dentro de uma palavra, é ineficiente para atualização constante de recipiente de contexto. Para facilitar a atualização mais eficiente sempre que você detecte o cursor movendo dentro do editor ou a janela do designer, você pode chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A>. Isso permite que você mantenha as alterações de contexto até que haja tempo ocioso e o serviço de contexto do IDE envia notificação para o editor ou designer de **ajuda dinâmica** janela está sendo atualizado. Essa abordagem é usada na **para manter o recipiente de contexto** procedimento neste artigo.  
  
 Depois de fornecer contexto para atividades em seu editor ou designer, você deve fornecer um determinado **F1** palavra-chave para permitir que os usuários obter ajuda para o editor ou designer em si.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.RemoveAttribute%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx>