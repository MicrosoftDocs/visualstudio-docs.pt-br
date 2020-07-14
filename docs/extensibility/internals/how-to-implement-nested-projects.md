---
title: 'Como: implementar projetos aninhados | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- nested projects, implementing
- projects [Visual Studio SDK], nesting
ms.assetid: d20b8d6a-f0e0-4115-b3a3-edda893ae678
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3b1ac3c147962b943499172435c3f601115d36a9
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905347"
---
# <a name="how-to-implement-nested-projects"></a>Como: implementar projetos aninhados

Quando você cria um tipo de projeto aninhado, há várias etapas adicionais que devem ser implementadas. Um projeto pai assume algumas das mesmas responsabilidades que a solução tem para seus projetos aninhados (filho). O projeto pai é um contêiner de projetos semelhantes a uma solução. Em particular, há vários eventos que devem ser gerados pela solução e pelos projetos pai para criar a hierarquia de projetos aninhados. Esses eventos são descritos no processo a seguir para criar projetos aninhados.

## <a name="create-nested-projects"></a>Criar projetos aninhados

1. O ambiente de desenvolvimento integrado (IDE) carrega o arquivo de projeto do projeto pai e as informações de inicialização chamando a <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> interface. O projeto pai é criado e adicionado à solução.

    > [!NOTE]
    > Neste ponto, é muito cedo no processo para o projeto pai criar o projeto aninhado porque o projeto pai deve ser criado antes que os projetos filho possam ser criados. Após essa sequência, o projeto pai pode aplicar as configurações aos projetos filho e os projetos filho podem adquirir informações dos projetos pai, se necessário. Essa sequência é se necessária em clientes como o SCC (controle de código-fonte) e o **Gerenciador de soluções**.

     O projeto pai deve aguardar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> método ser chamado pelo IDE antes de poder criar seu projeto ou projetos aninhados (filho).

2. O IDE chama `QueryInterface` o projeto pai para <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject> . Se essa chamada for realizada com sucesso, o IDE chamará o <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> método do pai para abrir todos os projetos aninhados do projeto pai.

3. O projeto pai chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnBeforeOpeningChildren%2A> método para notificar os ouvintes que os projetos aninhados estão prestes a serem criados. O SCC, por exemplo, está ouvindo esses eventos para saber se as etapas no processo de criação da solução e do projeto estão ocorrendo na ordem. Se as etapas ocorrerem fora de ordem, a solução poderá não ser registrada corretamente com o controle do código-fonte.

4. O projeto pai chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProject%2A> o método ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProjectEx%2A> método em cada um de seus projetos filho.

     Você passa <xref:Microsoft.VisualStudio.Shell.Interop.__VSADDVPFLAGS> para o `AddVirtualProject` método para indicar que o projeto virtual (aninhado) deve ser adicionado à janela do projeto, excluído da compilação, adicionado ao controle do código-fonte e assim por diante. `VSADDVPFLAGS`permite que você controle a visibilidade do projeto aninhado e indique qual funcionalidade está associada a ele.

     Se você recarregar um projeto filho anteriormente existente que tenha um GUID de projeto armazenado no arquivo de projeto do projeto pai, o projeto pai chamará `AddVirtualProjectEx` . A única diferença entre `AddVirtualProject` e `AddVirtualProjectEX` é que `AddVirtualProjectEX` tem um parâmetro para habilitar o projeto pai para especificar um por instância `guidProjectID` para o projeto filho habilitar <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfGuid%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfProjref%2A> funcionar corretamente.

     Se não houver nenhum GUID disponível, como quando você adicionar um novo projeto aninhado, a solução criará um para o projeto no momento em que ele for adicionado ao pai. É responsabilidade do projeto pai persistir o GUID do projeto em seu arquivo de projeto. Se você excluir um projeto aninhado, o GUID desse projeto também poderá ser excluído.

5. O IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren> método em cada projeto filho do projeto pai.

     O projeto pai deve implementar `IVsParentProject` se você deseja aninhar projetos. Mas o projeto pai nunca chama `QueryInterface` `IVsParentProject` , mesmo que ele tenha projetos pai abaixo dele. A solução manipula a chamada para `IVsParentProject` e, se for implementada, chama `OpenChildren` para criar os projetos aninhados. `AddVirtualProjectEX`é sempre chamado de `OpenChildren` . Ele nunca deve ser chamado pelo projeto pai para manter os eventos de criação de hierarquia na ordem.

6. O IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> método no projeto filho.

7. O projeto pai chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpeningChildren%2A> método para notificar os ouvintes que os projetos filho para o pai foram criados.

8. O IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpenProject%2A> método no projeto pai após a abertura de todos os projetos filho.

     Se ele ainda não existir, o projeto pai criará um GUID para cada projeto aninhado chamando `CoCreateGuid` .

    > [!NOTE]
    > `CoCreateGuid`é uma API COM chamada quando um GUID deve ser criado. Para obter mais informações, consulte `CoCreateGuid` e GUIDs na biblioteca MSDN.

     O projeto pai armazena esse GUID em seu arquivo de projeto para ser recuperado da próxima vez que for aberto no IDE. Consulte a etapa 4 para obter mais informações relacionadas à chamada de `AddVirtualProjectEX` para recuperar o `guidProjectID` para o projeto filho.

9. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> método é chamado para o ItemId pai que, por convenção, você delega para o projeto aninhado. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> recupera as propriedades do nó que Aninha um projeto que você deseja delegar quando ele é chamado no pai.

     Como os projetos pai e filho são instanciados programaticamente, você pode definir propriedades para projetos aninhados neste ponto.

    > [!NOTE]
    > Você não só recebe as informações de contexto do projeto aninhado, mas também pode perguntar se o projeto pai tem qualquer contexto para esse item, verificando [__VSHPROPID. VSHPROPID_UserContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_UserContext>). Dessa forma, você pode adicionar atributos de ajuda dinâmica extras e opções de menu específicas para projetos individuais aninhados.

10. A hierarquia é criada para exibição no **Gerenciador de soluções** com uma chamada para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A> método.

     Você passa a hierarquia para o ambiente por meio do `GetNestedHierarchy` para criar a hierarquia para exibição no Gerenciador de soluções. Dessa maneira, a solução sabe que o projeto existe e pode ser gerenciado para criação pelo Gerenciador de compilação, ou pode permitir que arquivos no projeto sejam colocados no controle do código-fonte.

11. Quando todos os projetos aninhados para Projeto1 tiverem sido criados, o controle será passado de volta para a solução e o processo será repetido para Projeto2.

     Esse mesmo processo para a criação de projetos aninhados ocorre para um projeto filho que tem um filho. Nesse caso, se BuildProject1, que é um filho de Projeto1, tinha projetos filho, eles seriam criados após BuildProject1 e antes de Projeto2. O processo é Recursivo e a hierarquia é criada de cima para baixo.

     Quando um projeto aninhado é fechado porque o usuário fechou a solução ou o próprio projeto específico, o outro método em `IVsParentProject` , <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.CloseChildren%2A> , é chamado. O projeto pai encapsula chamadas para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.RemoveVirtualProject%2A> método com o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeClosingChildren%2A> e os <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterClosingChildren%2A> métodos para notificar os ouvintes sobre eventos de solução que os projetos aninhados estão sendo fechados.

Os tópicos a seguir lidam com vários outros conceitos a serem considerados ao implementar projetos aninhados:

- [Considerações para descarregar e recarregar projetos aninhados](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [Suporte do assistente para projetos aninhados](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [Implementar manipulação de comandos para projetos aninhados](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [Filtrar a caixa de diálogo AddItem para projetos aninhados](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)

## <a name="see-also"></a>Confira também

- [Adicionar itens à caixa de diálogo Adicionar novo item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [Registrar modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md)
- [Lista de verificação: criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)
- [Arquivo do assistente (. vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)
