---
title: 'Como: implementar projetos aninhados | Microsoft Docs'
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
- nested projects, implementing
- projects [Visual Studio SDK], nesting
ms.assetid: d20b8d6a-f0e0-4115-b3a3-edda893ae678
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8a392b8b336c57c47055357147075f29ba173d8f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810124"
---
# <a name="how-to-implement-nested-projects"></a>Como: implementar projetos aninhados
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Quando você cria um tipo de projeto aninhado existe são uma várias etapas adicionais que devem ser implementadas. Um projeto pai leva em algumas das mesmas responsabilidades que a solução tem para seus projetos aninhados (filho). O projeto pai é um contêiner de projetos semelhantes a uma solução. Em particular, há vários eventos que devem ser gerados pela solução e pelos projetos pai para criar a hierarquia de projetos aninhados. Esses eventos são descritos no seguinte processo para a criação de projetos aninhados.  
  
### <a name="to-create-nested-projects"></a>Para criar projetos aninhados  
  
1. O ambiente de desenvolvimento integrado (IDE) carrega as informações de inicialização e o arquivo de projeto do projeto pai, chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> interface. O projeto pai é criado e adicionado à solução.  
  
   > [!NOTE]
   >  Neste ponto, é muito cedo no processo para o projeto pai criar o projeto aninhado porque o projeto pai deve ser criado antes que os projetos filho podem ser criados. Seguindo essa sequência, o projeto pai pode aplicar configurações aos projetos filho e os projetos filho podem adquirir informações dos projetos pai, se necessário. Essa sequência é se ela é necessária por clientes como o controle do código fonte (SCC) e o Gerenciador de soluções.  
  
    O projeto pai deve aguardar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> método a ser chamado pelo IDE para criar seu aninhado (filho) projeto ou projetos.  
  
2. As chamadas IDE `QueryInterface` no projeto pai para <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject>. Se essa chamada for bem-sucedida, o IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> método do pai para abrir todos os projetos aninhados para o projeto pai.  
  
3. As chamadas de projeto pai o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnBeforeOpeningChildren%2A> método para notificar os ouvintes que aninhado projetos estão prestes a ser criado. Por exemplo, o SCC, está escutando a esses eventos para saber se as etapas no processo de criação de solução e projeto estão ocorrendo em ordem. Se as etapas ocorrerão fora de ordem, a solução não pode ser registrada com o controle do código fonte corretamente.  
  
4. As chamadas de projeto pai <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProject%2A> método ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProjectEx%2A> método em cada um dos seus projetos filho.  
  
    Você passa <xref:Microsoft.VisualStudio.Shell.Interop.__VSADDVPFLAGS> para o `AddVirtualProject` método para indicar que o projeto (aninhado) virtual deve ser adicionado à janela do projeto, excluída da compilação, adicionado ao controle do código fonte e assim por diante. `VSADDVPFLAGS` permite controlar a visibilidade do projeto aninhado e indicar qual funcionalidade está associada a ele.  
  
    Se você recarregar um projeto anteriormente existente filho que tem um projeto GUID armazenado no arquivo de projeto do projeto pai, as chamadas de projeto pai `AddVirtualProjectEx`. A única diferença entre `AddVirtualProject` e `AddVirtualProjectEX` é que `AddVirtualProjectEX` tem um parâmetro para permitir que o projeto pai especificar um por instância `guidProjectID` para o projeto filho habilitar <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfGuid%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfProjref%2A> para função corretamente.  
  
    Se não houver nenhum GUID disponível, como quando você adiciona um novo projeto aninhado, a solução cria um para o projeto no momento, ele é adicionado ao pai. É responsabilidade do projeto para manter esse GUID em seu arquivo de projeto do projeto pai. Se você excluir um projeto aninhado, o GUID para o projeto também pode ser excluído.  
  
5. As chamadas IDE a `M:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren` método em cada projeto filho do projeto pai.  
  
    O projeto pai deve implementar `IVsParentProject` se você quiser aninhar projetos. Mas o pai do projeto nunca chama `QueryInterface` para `IVsParentProject` , mesmo se ele tiver projetos pai abaixo dela. A solução lida com a chamada para `IVsParentProject` e, se ele for implementado, chama `OpenChildren` para criar os projetos aninhados. `AddVirtualProjectEX` sempre é chamado de `OpenChildren`. Nunca deve ser chamada pelo projeto pai para manter a hierarquia de eventos de criação na ordem.  
  
6. As chamadas IDE a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> método no projeto filho.  
  
7. As chamadas de projeto pai o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpeningChildren%2A> método para notificar os ouvintes que foram criados os projetos filho do pai.  
  
8. As chamadas IDE a <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpenProject%2A> método no projeto pai depois que todos os projetos filho foram abertos.  
  
    Se ele ainda não existir, o projeto pai cria um GUID para cada projeto aninhado chamando `CoCreateGuid`.  
  
   > [!NOTE]
   >  `CoCreateGuid` uma API COM é chamada quando um GUID deve ser criado. Para obter mais informações, consulte `CoCreateGuid` e GUIDs na biblioteca MSDN.  
  
    O projeto pai armazena esse GUID em seu arquivo de projeto a ser recuperado na próxima vez que ele é aberto no IDE. Consulte a etapa 4 para obter mais informações relacionadas a chamada de `AddVirtualProjectEX` para recuperar o `guidProjectID` para o projeto filho.  
  
9. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> método é chamado para o pai ItemID por convenção, delegar para o projeto aninhado. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> recupera as propriedades do nó que aninha um projeto que você deseja delegar no quando o pai é chamado.  
  
     Porque os projetos pai e filho são instanciados por meio de programação, você pode definir propriedades para projetos aninhados neste momento.  
  
    > [!NOTE]
    >  Não apenas você recebe as informações de contexto do projeto aninhado, mas você também pode fazer se o projeto pai tem qualquer contexto para esse item, marcando <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>. Dessa forma, você pode adicionar atributos adicionais de ajuda dinâmica e opções de menu específicas para projetos aninhados individuais.  
  
10. A hierarquia é criada para exibição no Gerenciador de soluções com uma chamada para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A> método.  
  
     Você passa a hierarquia para o ambiente por meio de `GetNestedHierarchy` para criar a hierarquia para exibição no Gerenciador de soluções. Dessa forma, a solução sabe que o projeto existe e pode ser gerenciado pelo Gerenciador de build para compilar ou pode permitir que os arquivos no projeto a ser colocada sob controle do código-fonte.  
  
11. Quando todos os projetos aninhados para Projeto1 tiverem sido criados, o controle é passado de volta para a solução e o processo é repetido para Project2.  
  
     Esse mesmo processo para a criação de projetos aninhados ocorre para um projeto filho que tem um filho. Nesse caso, se BuildProject1, que é um filho do Projeto1, tinha projetos filho, eles seriam criados após BuildProject1 e antes Project2. O processo é recursiva e a hierarquia é compilada de cima para baixo.  
  
     Quando um projeto aninhado é fechado porque o usuário fechou a solução ou específicos do projeto em si, o outro método na `IVsParentProject`, <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.CloseChildren%2A>, é chamado. O projeto pai encapsula chamadas para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.RemoveVirtualProject%2A> método com o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeClosingChildren%2A> e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterClosingChildren%2A> métodos para notificar os ouvintes de eventos de solução a que os projetos aninhados estão sendo fechados.  
  
    Os tópicos a seguir lidam com vários outros conceitos a serem considerados ao implementar projetos aninhados:  
  
    [Considerações para descarregar e recarregar projetos aninhados](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)  
  
    [Suporte do assistente para projetos aninhados](../../extensibility/internals/wizard-support-for-nested-projects.md)  
  
    [Implementar manipulação de comando para projetos aninhados](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)  
  
    [Filtrar a caixa de diálogo Adicionar Item para projetos aninhados](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)  
  
## <a name="see-also"></a>Consulte também  
 [Adição de itens para a adicionar novo Item caixas de diálogo](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [Registrar modelos de projeto e Item](../../extensibility/internals/registering-project-and-item-templates.md)   
 [Lista de verificação: Criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)   
 [Arquivo do assistente (.Vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)

