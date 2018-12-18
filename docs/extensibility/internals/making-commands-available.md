---
title: Disponibilizar comandos | Microsoft Docs
ms.date: 03/22/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- best practices, menu and toolbar commands
- toolbars [Visual Studio], best practices
- menu commands, best practices
ms.assetid: 3ffc4312-c6db-4759-a946-a4bb85f4a17a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c1292dc3879effa53f3b4a41b87374a3a5f46ff0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49857127"
---
# <a name="making-commands-available"></a>Disponibilizando comandos
Quando vários VSPackages são adicionados ao Visual Studio, a interface do usuário (IU) pode ficar sobrecarregada com comandos. Você pode programar seu pacote para ajudar a reduzir esse problema, da seguinte maneira:

-   O pacote do programa para que ele seja carregado apenas quando um usuário requer que ela.

-   O pacote do programa para que seus comandos são exibidos somente quando elas podem ser necessárias no contexto do estado atual do ambiente de desenvolvimento integrado (IDE).

## <a name="delayed-loading"></a>Carregamento atrasado
 Habilitar uma forma comum de carregamento com atraso é projetar o VSPackage, de forma que seus comandos são exibidos na interface do usuário, mas o próprio pacote não será carregado até que um usuário clica em um dos comandos. Para fazer isso, no arquivo. VSCT, crie comandos que não têm nenhum sinalizador de comando.

 O exemplo a seguir mostra a definição de um comando de menu de um arquivo. VSCT. Esse é o comando que é gerado pelo modelo de pacote do Visual Studio quando o **comando de Menu** está selecionada no modelo.

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

No exemplo, se o grupo pai, `MyMenuGroup`, é um filho de um menu de nível superior, como o **ferramentas** menu, o comando estará visível nesse menu, mas o pacote que executa o comando não será carregado até que o comando é clicado por um usuário. No entanto, por programação o comando para implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface, você pode permitir que o pacote a ser carregado quando o menu que contém o comando pela primeira vez é expandido.

Observe que o carregamento atrasado também pode melhorar o desempenho de inicialização.

## <a name="current-context-and-the-visibility-of-commands"></a>Contexto atual e a visibilidade de comandos
 Você pode programar comandos de VSPackage para ser visível ou oculto, dependendo do estado atual dos dados VSPackage ou as ações que são relevantes no momento. Você pode habilitar o VSPackage definir o estado de seus comandos, normalmente por meio de uma implementação do <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> método a partir de <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface, mas isso requer o VSPackage a ser carregado antes de poder executar o código. Em vez disso, é recomendável que você habilite o IDE gerenciar a visibilidade dos comandos sem carregar o pacote. Para fazer isso, no arquivo. VSCT, associar comandos com um ou mais contextos de interface do usuário especiais. Esses contextos de interface do usuário são identificados por um GUID conhecido como um *GUID de contexto do comando*.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] monitora as alterações que resultam de ações do usuário como carregar um projeto ou vai da edição de construção. Quando ocorrem alterações, a aparência do IDE automaticamente será modificada. A tabela a seguir mostra quatro principais contextos do IDE alteração-la [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] monitores.


| Tipo de contexto | Descrição |
|-------------------------| - |
| Tipo de projeto ativo | Para a maioria dos tipos de projeto, isso `GUID` valor é igual ao GUID do VSPackage que implementa o projeto. No entanto, [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] projetos usam o tipo de projeto `GUID` como o valor. |
| Janela ativa | Normalmente, isso é a última janela do documento ativo que estabelece o contexto de interface do usuário atual para associações de teclas. No entanto, ele também pode ser uma janela de ferramenta que tem uma tabela de associação de teclas que se parece com o navegador da Web interno. Para janelas de documento com várias guias, como o editor de HTML, cada guia tem um contexto diferente do comando `GUID`. |
| Serviço de linguagem do Active Directory | O serviço de linguagem que está associado com o arquivo que está sendo exibido em um editor de texto. |
| Janela da ferramenta ativa | Uma janela de ferramenta que está aberto e tem o foco. |

 Uma área principal de contexto quinta é o estado da interface do usuário do IDE. Contextos de interface do usuário são identificados pelo contexto do comando ativo `GUID`s, da seguinte maneira:

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Dragging_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.FullScreenMode_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.DesignMode_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.NoSolution_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.CodeWindow_guid>

Esses GUIDs são marcadas como ativas ou inativas, dependendo do estado atual do IDE. Vários contextos de interface do usuário podem estar ativos ao mesmo tempo.

### <a name="hiding-and-displaying-commands-based-on-context"></a>Ocultando e comandos com base no contexto de exibição
 Você pode exibir ou ocultar um comando de pacote no IDE sem carregar o pacote propriamente dito. Para fazer isso, defina o comando no arquivo. VSCT do pacote usando o `DefaultDisabled`, `DefaultInvisible`, e `DynamicVisibility` comando sinalizadores e adicionando um ou mais [VisibilityItem](../../extensibility/visibilityitem-element.md) elementos para o [ VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) seção. Quando um contexto do comando especificado `GUID` se torna ativo, o comando é exibido sem carregar o pacote.

### <a name="custom-context-guids"></a>GUIDs de contexto personalizado
 Se um contexto de comando apropriado que GUID já não está definido, você pode definir um em seu VSPackage e, em seguida, programá-lo para ser ativos ou inativos conforme necessário para controlar a visibilidade de seus comandos. Use o <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> serviço para:

-   Registrar os GUIDs de contexto (chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> método).

-   Obter o estado de um contexto `GUID` (chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> método).

-   Ativar o contexto `GUID`s e desativar (chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> método).

    > [!CAUTION]
    > Certifique-se de que o VSPackage não afeta o estado de qualquer contexto existente GUID porque pode depender de outros VSPackages neles.

## <a name="example"></a>Exemplo
 O exemplo a seguir de um comando de VSPackage demonstra a visibilidade dinâmica de um comando que é gerenciado pelo contextos de comando sem carregar o VSPackage.

 O comando é definido como habilitado e exibido sempre que existe uma solução; ou seja, sempre que um contexto do seguinte comando GUIDs está ativo:

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

-   <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

No exemplo, observe que o sinalizador de cada comando é um separado [sinalizador de comando](../../extensibility/command-flag-element.md) elemento.

```xml
<Button guid="guidDynamicVisibilityCmdSet" id="cmdidMyCommand"
        priority="0x0100" type="Button">
  <Parent guid="guidDynamicVisibilityCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <CommandFlag>DefaultDisabled</CommandFlag>
  <CommandFlag>DefaultInvisible</CommandFlag>
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <CommandName>cmdidMyCommand</CommandName>
    <ButtonText>My Command name</ButtonText>
  </Strings>
</Button>
```

Além disso, observe que cada contexto de interface do usuário deve ser fornecido em um separado `VisibilityItem` elemento, da seguinte maneira.

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_EmptySolution" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                      id="cmdidMyCommand" context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

## <a name="see-also"></a>Consulte também

- [MenuCommands Vs. OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md)
- [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Roteamento de comando em VSPackages](../../extensibility/internals/command-routing-in-vspackages.md)
- [Adicionar itens de menu dinamicamente](../../extensibility/dynamically-adding-menu-items.md)
