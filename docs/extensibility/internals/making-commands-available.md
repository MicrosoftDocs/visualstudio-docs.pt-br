---
title: Disponibilizando comandos | Microsoft Docs
description: Saiba como controlar a disponibilidade de comandos que são adicionados ao IDE do Visual Studio no VSPackages, usando carregamento, contexto e visibilidade atrasados.
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- best practices, menu and toolbar commands
- toolbars [Visual Studio], best practices
- menu commands, best practices
ms.assetid: 3ffc4312-c6db-4759-a946-a4bb85f4a17a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 29f5e5c634c1bf360409e35c87684282a26e8a07
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095206"
---
# <a name="making-commands-available"></a>Disponibilizando comandos

Quando várias VSPackages são adicionadas ao Visual Studio, a interface do usuário pode se tornar supertorcida com comandos. Você pode programar seu pacote para ajudar a reduzir esse problema, da seguinte maneira:

- Programe o pacote para que ele seja carregado somente quando um usuário o exigir.

- Programe o pacote de forma que seus comandos sejam exibidos somente quando eles puderem ser necessários no contexto do estado atual do IDE (ambiente de desenvolvimento integrado).

## <a name="delayed-loading"></a>Carregamento atrasado

A maneira típica de habilitar o carregamento atrasado é criar o VSPackage para que seus comandos sejam exibidos na interface do usuário, mas o pacote em si não é carregado até que um usuário clique em um dos comandos. Para fazer isso, no arquivo. vsct, crie comandos que não têm nenhum sinalizador de comando.

O exemplo a seguir mostra a definição de um comando de menu de um arquivo. vsct. Esse é o comando que é gerado pelo modelo de pacote do Visual Studio quando a opção de **comando de menu** no modelo é selecionada.

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

No exemplo, se o grupo pai, `MyMenuGroup` , for um filho de um menu de nível superior, como o menu **ferramentas** , o comando ficará visível nesse menu, mas o pacote que executa o comando não será carregado até que o comando seja clicado por um usuário. No entanto, ao programar o comando para implementar a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface, você pode habilitar o pacote a ser carregado quando o menu que contém o comando for primeiro expandido.

Observe que o carregamento atrasado também pode melhorar o desempenho de inicialização.

## <a name="current-context-and-the-visibility-of-commands"></a>Contexto atual e a visibilidade dos comandos

Você pode programar comandos VSPackage para que fiquem visíveis ou ocultos, dependendo do estado atual dos dados do VSPackage ou das ações que são relevantes no momento. Você pode habilitar o VSPackage para definir o estado de seus comandos, normalmente usando uma implementação do <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> método da <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface, mas isso requer que o VSPackage seja carregado antes de poder executar o código. Em vez disso, recomendamos que você habilite o IDE para gerenciar a visibilidade dos comandos sem carregar o pacote. Para fazer isso, no arquivo. vsct, associe os comandos a um ou mais contextos de interface do usuário especiais. Esses contextos de interface do usuário são identificados por um GUID conhecido como um *GUID de contexto de comando*.

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] monitora alterações que resultam de ações do usuário, como carregar um projeto ou ir da edição para a compilação. À medida que ocorrem alterações, a aparência do IDE é modificada automaticamente. A tabela a seguir mostra quatro contextos principais de alteração do IDE que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] monitora.

| Tipo de contexto | Descrição |
|-------------------------| - |
| Tipo de projeto ativo | Para a maioria dos tipos de projeto, esse `GUID` valor é o mesmo que o GUID do VSPackage que implementa o projeto. No entanto, [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] os projetos usam o tipo de projeto `GUID` como o valor. |
| Janela ativa | Normalmente, esta é a última janela do documento ativo que estabelece o contexto da interface do usuário atual para associações de chave. No entanto, também pode ser uma janela de ferramentas que tem uma tabela de associação de chave que se assemelha ao navegador da Web interno. Para janelas de documentos com várias guias, como o editor de HTML, cada guia tem um contexto de comando diferente `GUID` . |
| Serviço de linguagem ativa | O serviço de idioma que está associado ao arquivo que é exibido atualmente em um editor de texto. |
| Janela de ferramentas ativas | Uma janela de ferramentas aberta e tem foco. |

Uma quinta área de contexto principal é o estado da interface do usuário do IDE. Os contextos da interface do usuário são identificados por s do contexto de comando ativo `GUID` , da seguinte maneira:

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Dragging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.FullScreenMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.DesignMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.NoSolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.CodeWindow_guid>

Essas GUIDs são marcadas como ativas ou inativas, dependendo do estado atual do IDE. Vários contextos de interface do usuário podem estar ativos ao mesmo tempo.

### <a name="hide-and-display-commands-based-on-context"></a>Ocultar e exibir comandos com base no contexto

Você pode exibir ou ocultar um comando de pacote no IDE sem carregar o pacote em si. Para fazer isso, defina o comando no arquivo. vsct do pacote usando os `DefaultDisabled` sinalizadores de comando, `DefaultInvisible` , e `DynamicVisibility` e adicionando um ou mais elementos [VisibilityItem](../../extensibility/visibilityitem-element.md) à seção [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) . Quando um contexto de comando especificado `GUID` se torna ativo, o comando é exibido sem carregar o pacote.

### <a name="custom-context-guids"></a>GUIDs de contexto personalizado

Se um GUID de contexto de comando apropriado ainda não estiver definido, você poderá definir um em seu VSPackage e, em seguida, programá-lo para estar ativo ou inativo conforme necessário para controlar a visibilidade de seus comandos. Use o <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> serviço para:

- Registre GUIDs de contexto (chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> método).

- Obter o estado de um contexto `GUID` (chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> método).

- Ativar `GUID` e desativar os s de contexto (chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> método).

    > [!CAUTION]
    > Certifique-se de que o VSPackage não afeta o estado de qualquer GUID de contexto existente porque outros VSPackages podem depender deles.

## <a name="example"></a>Exemplo

O exemplo a seguir de um comando VSPackage demonstra a visibilidade dinâmica de um comando que é gerenciado por contextos de comando sem carregar o VSPackage.

O comando é definido para ser habilitado e exibido sempre que existir uma solução; ou seja, sempre que um dos seguintes GUIDs de contexto de comando estiver ativo:

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

No exemplo, observe que cada sinalizador de comando é um elemento de [sinalizador de comando](../../extensibility/command-flag-element.md) separado.

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

Observe também que cada contexto de interface do usuário deve ser fornecido em um `VisibilityItem` elemento separado, da seguinte maneira.

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

## <a name="see-also"></a>Confira também

- [Adicionar um comando à barra de ferramentas Gerenciador de Soluções](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)
- [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Roteamento de comando em VSPackages](../../extensibility/internals/command-routing-in-vspackages.md)
- [Adicionar itens de menu dinamicamente](../../extensibility/dynamically-adding-menu-items.md)
