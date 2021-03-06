---
title: Atalhos de teclado padrão
description: Saiba mais sobre os atalhos de teclado padrão Visual Studio que permitem que você acesse uma variedade de comandos e janelas.
ms.custom: SEO-VS-2020
ms.date: 06/21/2021
ms.topic: reference
helpviewer_keywords:
- shortcut keys [Visual Studio], keyboard binding schemes
- keyboard binding schemes [Visual Studio]
- Help [Visual Studio], shortcut keys
- keyboard shortcuts [Visual Studio], keyboard binding schemes
- keyboard shortcuts
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dec9f76f2b21e11cc79bc55efc4a2de6fb7dedc3
ms.sourcegitcommit: 15821c790d6498210f30b3268402ffad6bb70c7c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/14/2021
ms.locfileid: "113725515"
---
# <a name="default-keyboard-shortcuts-in-visual-studio"></a>Atalhos de teclado padrão no Visual Studio

Você pode acessar uma variedade de [comandos](reference/visual-studio-commands.md) e janelas no Visual Studio escolhendo o atalho de teclado apropriado. Essa página lista os atalhos de comando padrão para o perfil **Geral**, que você pode ter escolhido quando instalou o Visual Studio. Não importa qual o perfil escolhido, é possível [identificar o atalho](identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md) de um comando abrindo a caixa de diálogo **Opções**, expandindo o nó **Ambiente** e escolhendo **Teclado**. Também é possível personalizar seus atalhos atribuindo um atalho diferente a qualquer comando.

Para obter uma lista dos atalhos de teclado comuns e outras informações sobre produtividade, confira:

- [Dicas de teclado](../ide/productivity-shortcuts.md)
- [Dicas de produtividade](../ide/productivity-features.md).

Para obter mais informações sobre acessibilidade Visual Studio, consulte Dicas e truques de acessibilidade e Como usar o [teclado exclusivamente](../ide/reference/how-to-use-the-keyboard-exclusively.md). [](../ide/reference/accessibility-tips-and-tricks.md)

<a name="popular"></a>
## <a name="popular-keyboard-shortcuts-for-visual-studio"></a>Atalhos de teclado populares para o Visual Studio

Todos os atalhos nesta seção se aplicam globalmente, a menos que especificado de outra forma. O contexto *Global* significa que o atalho é aplicável em qualquer janela de ferramenta no Visual Studio.

> [!NOTE]
> É possível [pesquisar o atalho](identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md) para qualquer comando abrindo a caixa de diálogo **Opções**, expandindo o nó **Ambiente** e, em seguida, escolhendo **Teclado**.


#### <a name="build-popular-shortcuts"></a>Build: atalhos populares

|Comandos|Atalhos de teclado |ID do comando|
|-|-|-|
|Criar solução|**Ctrl+Shift+B** | Build.BuildSolution |
|Cancelar|**Ctrl+Break** | Build.Cancel |
|Compilar|**Ctrl+F7** | Build.Compile |
|Executar análise de código na solução|**Alt+F11**| Build.RunCodeAnalysisonSolution |

#### <a name="debug-popular-shortcuts"></a>Depurar: atalhos populares

|Comandos|Atalhos de teclado [Contextos especiais]|ID do comando|
|-|-|-|
|Interromper na função|**Ctrl+B**| Debug.BreakatFunction |
|Quebrar tudo|**Ctrl+Alt+Break**| Debug.BreakAll |
|Excluir todos os pontos de interrupção|**Ctrl+Shift+F9**| Debug.DeleteAllBreakpoints |
|Exceções|**Ctrl+Alt+E**| Debug.Exceptions |
|Relógio rápido|**Ctrl+Alt+Q**<br /><br />ou **Shift+F9**| Debug.QuickWatch |
|Reiniciar|**Ctrl+Shift+F5**| Debug.Restart |
|Executar até o cursor|**Ctrl+F10**| Debug.RunToCursor |
|Definir próxima instrução|**Ctrl+Shift+F10**| Debug.SetNextStatement |
|Iniciar|**F5**| Debug.Start |
|Iniciar sem depuração|**Ctrl+F5**| Debug.StartWithoutDebugging |
|Avançar|**F11**| Debug.StepInto |
|Sair|**Shift+F11**| Debug.StepOut |
|Passar por|**F10**| Debug.StepOver |
|Parar a depuração|**Shift+F5**| Debug.StopDebugging |
|Alterna um ponto de interrupção|**F9**| Debug.ToggleBreakpoint |

#### <a name="edit-popular-shortcuts"></a>Editar: atalhos populares

|Comandos|Atalhos de teclado [Contextos especiais]|ID do comando|
|-|-|-|
|Linha de quebra|**Enter** [Editor de Texto, Designer de Relatórios, Designer de Formulários do Windows]<br /><br />ou **Shift+Enter** [Editor de Texto]| Edit.BreakLine |
|Ressupsar em definições|**Ctrl+M**, **Ctrl+O** [Editor de Texto]| Edit.CollapseToDefinitions |
|Seleção de comentário|**Ctrl+K**, **Ctrl+C** [Editor de Texto]| Edit.CommentSelection |
|Completar a palavra|**Alt+Seta para a Direita** [Editor de Texto, Designer de Fluxo de Trabalho]<br /><br />ou **Ctrl+Barra de espaços** [Editor de Texto, Designer de Fluxo de Trabalho]<br /><br />ou **Ctrl+K**, **W** [Designer de Fluxo de Trabalho]<br /><br />ou **Ctrl+K, Ctrl+W** [Designer de Fluxo de Trabalho]| Edit.CompleteWord |
|Copiar|**Ctrl+C**<br /><br />ou **Ctrl+Insert**| Edit.Copy |
|Recortar|**Ctrl+X**<br /><br />ou **Shift+Delete**| Edit.Cut |
|Excluir|**Excluir** [Team Explorer]<br /><br />ou **Shift+Delete** [Diagrama de Sequência, Diagrama de Atividades UML, Diagrama de Camada]<br /><br />ou **Ctrl+Delete** [Diagrama de Classes]| Edit.Delete |
|Localizar|**Ctrl+F**| Edit.Find |
|Localizar todas as referências|**Shift+F12**| Edit.FindAllReferences |
|Localizar nos arquivos|**Ctrl+Shift+F**| Edit.FindinFiles |
|Localizar próximo|**F3**| Edit.FindNext |
|Encontrar a próxima opção selecionada|**Ctrl+F3**| Edit.FindNextSelected |
|Formatar documento|**Ctrl+K, Ctrl+D** [Editor de Texto]| Edit.FormatDocument |
|Formatar seleção|**Ctrl+K, Ctrl+F** [Editor de Texto]| Edit.FormatSelection |
|Ir para|**Ctrl+G**| Edit.GoTo |
|Ir para declaração|**Ctrl+F12**| Edit.GoToDeclaration |
|Ir para definição|**F12**| Edit.GoToDefinition |
|Ir para encontrar combinação|**Ctrl+D**| Edit.GoToFindCombo |
|Vá para o próximo local|**F8**| Edit.GoToNextLocation |
|Inserir snippet|**Ctrl+K,** **Ctrl+X**| Edit.InsertSnippet |
|Guia Inserir|**Tab** [Designer de Relatórios, Designer de Formulários do Windows, Editor de Texto]| Edit.InsertTab |
|Corte de linha|**Ctrl+L** [Editor de Texto]| Edit.LineCut |
|Coluna de extensão de linha para baixo|**Shift+Alt+Seta para Baixo** [Editor de Texto]| Edit.LineDownExtendColumn |
|Linha aberta acima|**Ctrl+Enter** [Editor de Texto]| Edit.LineOpenAbove |
|Listar os membros|**Ctrl+J** [Editor de Texto, Designer de Fluxo de Trabalho]<br /><br />ou **Ctrl+K, Ctrl+L** [Designer de Fluxo de Trabalho]<br /><br />ou **Ctrl+K, L** [Designer de Fluxo de Trabalho]| Edit.ListMembers |
|Navegar para|**Ctrl+,**| Edit.NavigateTo |
|Abrir arquivo|**Ctrl+Shift+G**| Edit.OpenFile |
|Modo overtype|**Insert** [Editor de Texto]| Edit.OvertypeMode |
|Informações de parâmetro|**Ctrl+Shift+Barra de espaços** [Editor de Texto, Designer de Fluxo de Trabalho]<br /><br />ou **Ctrl+K, Ctrl+P** [Designer de Fluxo de Trabalho]<br /><br />ou **Ctrl+K, P** [Designer de Fluxo de Trabalho]| Edit.ParameterInfo |
|Colar|**Ctrl+V**<br /><br />ou **Shift+Insert**| Edit.Paste |
|Espiar definição|**Alt+F12** [Editor de Texto]| Edit.PeekDefinition |
|Refazer|**Ctrl+Y**<br /><br />ou **Shift+Alt+Backspace**<br /><br />ou **Ctrl+Shift+Z**| Edit.Redo |
|Substitua|**Ctrl+H**| Edit.Replace |
|Selecionar tudo|**Ctrl+A**| Edit.SelectAll |
|Selecionar palavra atual|**Ctrl+W** [Editor de Texto]| Edit.SelectCurrentWord |
|Cancelar seleção|**Esc** [Editor de Texto, Designer de Relatórios, Designer de Configurações, Designer de Formulários do Windows, Editor de Recursos Gerenciados]| Edit.SelectionCancel |
|Surround com|**CTRL + K, CTRL + S**| Edit.SurroundWith |
|Tabulação à esquerda|**Shift+Tab** [Editor de Texto, Designer de Relatórios, Editor de Formulários do Windows]| Edit.TabLeft |
|Ativar/desativar toda a estrutura de tópicos|**Ctrl+M, Ctrl+L** [Editor de Texto]| Edit.ToggleAllOutlining |
|Ativar/desativar indicador|**Ctrl+K, Ctrl+K** [Editor de Texto]| Edit.ToggleBookmark |
|Alternar modo de conclusão|**Ctrl+Alt+Space** [Editor de Texto]| Edit.ToggleCompletionMode |
|Alternar a expansão da estrutura de tópicos|**Ctrl+M, Ctrl+M** [Editor de Texto]| Edit.ToggleOutliningExpansion |
|Remover comentário da seleção|**Ctrl+K, Ctrl+U** [Editor de Texto]| Edit.UncommentSelection |
|Desfazer|**Ctrl+Z**<br /><br />ou **ALT + Backspace**| Edit.Undo |
|Excluir palavra até o fim|**Ctrl+Delete** [Editor de Texto]| Edit.WordDeleteToEnd |
|Excluir palavra para iniciar|**Ctrl+Backspace** [Editor de Texto]| Edit.WordDeleteToStart |

#### <a name="file-popular-shortcuts"></a>Arquivo: atalhos populares

|Comandos|Atalhos de teclado [contextos especiais]|ID do comando|
|-|-|-|
|Fechar|**ALT + F4**| File.Exit |
|Novo arquivo|**Ctrl + N**| File.NewFile |
|Novo Projeto|**Ctrl + Shift + N**| File.NewProject |
|Novo site|**Shift+Alt+N**| File.NewWebSite |
|Abrir arquivo|**Ctrl+O**| File.OpenFile |
|Abrir projeto|**Ctrl + Shift + O**| File.OpenProject |
|Abrir site|**Shift+Alt+O**| File.OpenWebSite |
|Renomear|**F2** [Team Explorer]| File.Rename |
|Salvar tudo|**Ctrl + Shift + S**| File.SaveAll |
|Salvar itens selecionados|**Ctrl+S**| File.SaveSelectedItems |
|Exibir no navegador|**CTRL + SHIFT + W**| File.ViewinBrowser |

#### <a name="project-popular-shortcuts"></a>Project: atalhos populares

|Comandos|Atalhos de teclado [contextos especiais]|ID do comando|
|-|-|-|
|Adicionar item existente|**Shift + Alt + A**| Project.AddExistingItem |
|Adicionar novo item|**Ctrl + Shift + A**| Project.AddNewItem |

#### <a name="refactor-popular-shortcuts"></a>Refatorar: atalhos populares

|Comando|Atalho de teclado [contextos especiais]|ID do comando|
|-|-|-|
|Extrair método|**Ctrl+R, Ctrl+M**| Refactor.ExtractMethod |

#### <a name="tools-popular-shortcuts"></a>Ferramentas: atalhos populares

|Comando|Atalho de teclado [contextos especiais]|ID do comando|
|-|-|-|
|Anexar ao processo|**CTRL + ALT + P**| Tools.AttachtoProcess |

#### <a name="view-popular-shortcuts"></a>Exibição: atalhos populares

|Comandos|Atalhos de teclado [Contextos especiais]|ID do comando|
|-|-|-|
|Exibição de classe|**Ctrl+Shift+C**| View.ClassView |
|Editar rótulo|**F2**| View.EditLabel |
|Lista de erros|**Ctrl+ \\ , Ctrl+E**<br /><br />ou **Ctrl+ \\ , E**| View.ErrorList |
|Navegar para trás|**Ctrl+-**| View.NavigateBackward |
|Navegar para frente|**Ctrl+Shift+-**| View.NavigateForward |
|Pesquisador de objetos|**Ctrl+Alt+J**| View.ObjectBrowser |
|Saída|**Ctrl+Alt+O**| View.Output |
|Janela de Propriedades|**F4**| View.PropertiesWindow |
|Atualizar|**F5** [Team Explorer]| View.Refresh |
|Explorador de servidores|**Ctrl + Alt + S**| View.ServerExplorer |
|Mostrar marca inteligente|**Ctrl+.**<br /><br />ou **Shift+Alt+F10** [Exibição de Design do Editor HTML]| View.ShowSmartTag |
|Gerenciador de soluções|**Ctrl+Alt+L**| View.SolutionExplorer |
|Team Explorer do TFS|**Ctrl+ \\ , Ctrl+M**| View.TfsTeamExplorer |
|Caixa de Ferramentas|**Ctrl+Alt+X**| View.Toolbox |
|Exibir código|**Enter** [Diagrama de Classe]<br /><br />ou **F7** [Designer de Configurações]| View.ViewCode |
|Designer de exibição|**Shift+F7** [Modo Código-fonte do Editor de HTML]| View.ViewDesigner |

#### <a name="window-popular-shortcuts"></a>Janela: atalhos populares

|Comandos|Atalhos de teclado [Contextos especiais]|ID do comando|
|-|-|-|
|Ativar janela do documento|**Esc**| Window.ActivateDocumentWindow |
|Fechar janela do documento|**Ctrl+F4**| Window.CloseDocumentWindow |
|Próxima janela do documento|**Ctrl+F6**| Window.NextDocumentWindow |
|Próximo nav da janela do documento|**Ctrl+Tab**| Window.NextDocumentWindowNav |
|Próximo painel de divisão|**F6**| Window.NextSplitPane |


## <a name="global-shortcuts"></a>Atalhos globais

Esses atalhos de teclado são *globais*, o que significa que você pode usá-los quando qualquer janela do Visual Studio estiver em foco.

- [Analise](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_analyze)
- [Editar](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_edit)
- [Projeto](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_project)
- [Teste](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_test)
- [Arquitetura](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_architecture)
- [Menus de contexto do editor](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_editorContext)
- [Menus de Contexto de Projeto e Solução](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_projectContext)
- [Gerenciador de Testes](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_testexplorerGLOBAL)
- [Compilar](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_build)
- [Arquivo](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_file)
- [Refatoração](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_refactor)
- [Ferramentas](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_tools)
- [Menus de Contexto do Modo de Exibição de Classe](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_classview)
- [Ajuda](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_help)
- [Gerenciador de Soluções](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_solutionexplorerGLOBAL)
- [Exibir](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_view)
- [Depurar](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_debug)
- [Teste de carga](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_loadtest)
- [Equipe](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_team)
- [Window](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_window)
- [Menus de Contexto do Depurador](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_debugger)
- [Outros Menus de Contexto](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_otherContext)
- [Menus de Contexto do Team Foundation](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TFcontext)
- [Azure](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_windowsazure)
- [Hub de diagnósticos](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_diagnostics)

### <a name="analyze"></a><a name="bkmk_analyze"></a> Analisar

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Navegar para trás|**Shift+Alt+3**| Analyze.NavigateBackward |
|Navegar para frente|**Shift+Alt+4**| Analyze.NavigateForward |

### <a name="architecture"></a><a name="bkmk_architecture"></a> Arquitetura

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Novo diagrama|**Ctrl+ \\ , Ctrl+N**| Architecture.NewDiagram |

### <a name="build"></a><a name="bkmk_build"></a> Construir

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Seleção de build|**Ctrl+B** (Visual Studio 2019)| Build.BuildSelection |
|Criar solução|**Ctrl+Shift+B**| Build.BuildSolution |
|Cancelar|**Ctrl+Break**| Build.Cancel |
|Compilar|**Ctrl+F7**| Build.Compile |
|Executar análise de código na solução|**Alt+F11**| Build.RunCodeAnalysisonSolution |

### <a name="class-view-context-menus"></a><a name="bkmk_classview"></a> Modo de Exibição de Classe menus de contexto

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Propriedades|**Alt+Enter**| ClassViewContextMenus.ClassViewMultiselectProjectreferencesItems.Properties |

### <a name="debug"></a><a name="bkmk_debug"></a> Depurar

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Aplicar alterações de código|**Alt+F10**| Debug.ApplyCodeChanges |
|Anexar ao processo|**Ctrl+Alt+P**| Debug.AttachtoProcess |
|Autos|**Ctrl+Alt+V, A**| Debug.Autos |
|Quebrar tudo|**Ctrl+Alt+Break**| Debug.BreakAll |
|Pontos de interrupção|**Ctrl+Alt+B**| Debug.Breakpoints |
|Pilha de chamadas|**Ctrl+Alt+C**| Debug.CallStack |
|Excluir todos os pontos de interrupção|**Ctrl+Shift+F9**| Debug.DeleteAllBreakpoints |
|Inicializar|**Alt+F2**| Debug.DiagnosticsHub.Launch |
|Desmontagem|**Ctrl+Alt+D**| Debug.Disassembly |
|Explorador dom|**Ctrl+Alt+V, D**| Debug.DOMExplorer |
|Habilitar ponto de interrupção|**Ctrl+F9**| Debug.EnableBreakpoint |
|Exceções|**Ctrl+Alt+E**| Debug.Exceptions |
|Ponto de interrupção de função|**Ctrl+K, B** (Visual Studio 2019)<br />**Ctrl** + **B** (Visual Studio 2017)| Debug.FunctionBreakpoint |
|Vá para a chamada anterior ou evento do IntelliTrace|**Ctrl+Shift+F11**| Debug.GoToPreviousCallorIntelliTraceEvent |
|Iniciar diagnóstico|**Alt+F5**| Debug.Graphics.StartDiagnostics |
|Imediata|**Ctrl+Alt+I**| Debug.Immediate |
|Chamadas do IntelliTrace|**Ctrl+Alt+Y, T**| Debug.IntelliTraceCalls |
|Eventos do IntelliTrace|**Ctrl+Alt+Y, F**| Debug.IntelliTraceEvents |
|Console do JavaScript|**Ctrl+Alt+V, C**| Debug.JavaScriptConsole |
|Locais|**CTRL + ALT + V, L**| Debug.Locals |
|Combinação de processo|**CTRL + 5**| Debug.LocationToolbar.ProcessCombo |
|Combinação de quadros de pilhas|**CTRL + 7**| Debug.LocationToolbar.StackFrameCombo |
|Combinação de threads|**CTRL + 6**| Debug.LocationToolbar.ThreadCombo |
|Alternar estado sinalizado do thread atual|**CTRL + 8**| Debug.LocationToolbar.ToggleCurrentThreadFlaggedState |
|Alternar threads sinalizados|**CTRL + 9**| Debug.LocationToolbar.ToggleFlaggedThreads |
|Memória 1|**Ctrl+Alt+M, 1**| Debug.Memory1 |
|Memória 2|**Ctrl+Alt+M, 2**| Debug.Memory2 |
|Memória 3|**Ctrl+Alt+M, 3**| Debug.Memory3 |
|Memória 4|**Ctrl+Alt+M, 4**| Debug.Memory4 |
|Módulos|**Ctrl+Alt+U**| Debug.Modules |
|Pilhas paralelas|**Ctrl + Shift + D, S**| Debug.ParallelStacks |
|Inspeção paralela 1|**Ctrl+Shift+D, 1**| Debug.ParallelWatch1 |
|Inspeção paralela 2|**Ctrl+Shift+D, 2**| Debug.ParallelWatch2 |
|Inspeção paralela 3|**Ctrl+Shift+D, 3**| Debug.ParallelWatch3 |
|Inspeção paralela 4|**Ctrl+Shift+D, 4**| Debug.ParallelWatch4 |
|Processos|**Ctrl + Alt + Z**| Debug.Processes |
|Inspeção rápida|**Shift+F9** ou **Ctrl+Alt+Q**| Debug.QuickWatch |
|Anexar novamente ao processo|**Shift+Alt+P**| Debug. ReattachtoProcess |
|Atualizar windowsapp|**CTRL + SHIFT + R**| Debug.RefreshWindowsapp |
|Registros|**CTRL + ALT + G**| Debug.Registers |
|Reiniciar|**Ctrl+Shift+F5**| Debug.Restart |
|Executar até o cursor|**Ctrl + F10**| Debug.RunToCursor |
|Definir próxima instrução|**Ctrl+Shift+F10**| Debug.SetNextStatement |
|Mostrar pilha de chamadas no mapa de códigos|**Ctrl + Shift + '**| Debug.ShowCallStackonCodeMap |
|Mostrar próxima instrução|**Alt + num** *| Debug.ShowNextStatement |
|Iniciar|**F5**| Debug.Start |
|Iniciar análise de aplicativos do Windows Phone|**Alt + F1**| Debug.StartWindowsPhoneApplicationAnalysis |
|Iniciar sem depuração|**CTRL + F5**| Debug.StartWithoutDebugging |
|Avançar|**F11**| Debug.StepInto |
|Entrar no processo atual|**Ctrl+Alt+F11**| Debug.StepIntoCurrentProcess |
|Entrar em específico|**SHIFT + ALT + F11**| Debug.StepIntoSpecific |
|Sair|**Shift + F11**| Debug.StepOut |
|Depurar o processo atual|**Ctrl+Shift+Alt+F11**| Debug.StepOutCurrentProcess |
|Passar por|**F10** (ao depurar: executa uma etapa sobre a ação)| Debug.StepOver |
|Passar por|**F10** (quando não estiver Depurando: inicia a depuração e pára na primeira linha do código do usuário)| Debug.StepOver |
|Depurar o processo atual|**Ctrl+Alt+F10**| Debug.StepOverCurrentProcess |
|Parar a depuração|**Shift + F5**| Debug.StopDebugging |
|Parar análise de desempenho|**Shift+Alt+F2**| Debug.StopPerformanceAnalysis |
|Tarefas|**Ctrl + Shift + D, K**| Debug.Tasks |
|Threads|**CTRL + ALT + H**| Debug.Threads |
|Alterna um ponto de interrupção|**F9**| Debug.ToggleBreakpoint |
|Ativar/desativar desmontagem|**Ctrl + F11**| Debug.ToggleDisassembly |
|Inspeção 1|**CTRL + ALT + W, 1**| Debug.Watch1 |
|Inspeção 2|**CTRL + ALT + W, 2**| Debug.Watch2 |
|Inspeção 3|**CTRL + ALT + W, 3**| Debug.Watch3 |
|Inspeção 4|**CTRL + ALT + W, 4**| Debug.Watch4 |

### <a name="debugger-context-menus"></a><a name="bkmk_debugger"></a> Menus de contexto do depurador

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Excluir|**Alt + F9, D**| DebuggerContextMenus.BreakpointsWindow.Delete |
|Ir para desmontagem|**Alt+F9, A**| DebuggerContextMenus.BreakpointsWindow.GoToDisassembly |
|Ir para código-fonte|**Alt+F9, S**| DebuggerContextMenus.BreakpointsWindow.GoToSourceCode |

### <a name="diagnostics-hub"></a><a name="bkmk_diagnostics"></a> Hub de diagnóstico

|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Parar coleta|**Ctrl + Alt + F2**| DiagnosticsHub.StopCollection |

### <a name="edit"></a><a name="bkmk_edit"></a> Editar

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Copiar|**CTRL + C**<br /><br /> ou<br /><br /> **CTRL + ins**| Edit.Copy |
|Recortar|**CTRL + X**<br /><br /> ou<br /><br /> **Shift + Delete**| Edit.Cut |
|Alternar anel da área de transferência|**Ctrl + Shift + V**<br /><br /> ou<br /><br /> **Ctrl+Shift+Ins**| Edit.CycleClipboardRing |
|Excluir|**Excluir**| Edit.Delete |
|Duplicar|**Ctrl+D**| Edit.Duplicate |
|Localizar|**Ctrl + F**| Edit.Find |
|Localizar todas as referências|**SHIFT + F12**| Edit.FindAllReferences |
|Localizar nos arquivos|**Ctrl + Shift + F**| Edit.FindinFiles |
|Localizar próximo|**F3**| Edit.FindNext |
|Localizar próximo selecionado|**Ctrl + F3**| Edit.FindNextSelected |
|Localizar anterior|**Shift + F3**| Edit.FindPrevious |
|Localizar anterior selecionado|**Ctrl + Shift + F3**| Edit.FindPreviousSelected |
|Gerar método|**Ctrl+K, Ctrl+M**| Edit.GenerateMethod |
|Ir para|**Ctrl+G**| Edit.GoTo |
|Ir para todos|**Ctrl+,** ou **Ctrl+T**| Edit.GoToAll |
|Ir para a declaração|**Ctrl+F12**| Edit.GoToDeclaration |
|Ir para definição|**F12**| Edit.GoToDefinition |
|Ir para membro|**Ctrl+1, Ctrl+M** ou **Ctrl+1, M** ou **Alt+\\**| Edit.GoToMember |
|Ir para o próximo local|**F8** (próximo erro na Lista de Erros ou na janela Saída)| Edit.GoToNextLocation |
|Ir para local anterior|**Shift+F8** (erro anterior na Lista de Erros ou na janela Saída)| Edit.GoToPrevLocation |
|Inserir trecho|**CTRL + K, CTRL + X**| Edit.InsertSnippet |
|Mover controle para baixo|**CTRL + seta para baixo**| Edit.MoveControlDown |
|Mover controle para baixo na grade|**Seta para baixo**| Edit.MoveControlDownGrid |
|Mover controle para a esquerda|**Ctrl+Seta para a Esquerda**| Edit.MoveControlLeft |
|Mover controle para a esquerda na grade|**Seta para a esquerda**| Edit.MoveControlLeftGrid |
|Mover controle para a direita|**Ctrl+Seta para a Direita**| Edit.MoveControlRight |
|Mover controle para a direita na grade|**Seta para a direita**| Edit.MoveControlRightGrid |
|Mover controle para cima|**CTRL + seta para cima**| Edit.MoveControlUp |
|Mover controle para cima na grade|**Seta para cima**| Edit.MoveControlUpGrid |
|Próximo indicador|**CTRL + K, Ctrl + N**| Edit.NextBookmark |
|Próximo indicador na pasta|**Ctrl + Shift + K, Ctrl + Shift + N**| Edit.NextBookmarkInFolder |
|Abrir arquivo|**Ctrl+Shift+G** (abre o nome do arquivo sob o cursor)| Edit.OpenFile |
|Colar|**Ctrl + V**<br /><br /> ou<br /><br /> **Shift + ins**| Edit.Paste |
|Indicador anterior|**CTRL + K, CTRL + P**| Edit.PreviousBookmark |
|Indicador anterior na pasta|**Ctrl + Shift + K, Ctrl + Shift + P**| Edit.PreviousBookmarkInFolder |
|Símbolo de localização rápida|**Shift+Alt+F12**| Edit.QuickFindSymbol |
|Refazer|**Ctrl + Y**<br /><br /> ou<br /><br /> **Ctrl + Shift + Z**<br /><br /> ou<br /><br /> **Shift+Alt+Backspace**| Edit.Redo |
|Atualizar referências remotas|**Ctrl + Shift + J**| Edit.RefreshRemoteReferences |
|Substitua|**CTRL + H**| Edit.Replace |
|Substituir em arquivos|**Ctrl+Shift+H**| Edit.ReplaceinFiles |
|Selecionar tudo|**Ctrl+A**| Edit.SelectAll |
|Selecione o próximo controle|**Tab**| Edit.SelectNextControl |
|Selecionar controle anterior|**Shift+Tab**| Edit.SelectPreviousControl |
|Mostrar grade deile|**Enter**| Edit.ShowTileGrid |
|Controle de tamanho reduzido|**Ctrl+Shift+Seta para Baixo**| Edit.SizeControlDown |
|Controle de tamanho para baixo da grade|**Shift+Seta para Baixo**| Edit.SizeControlDownGrid |
|Controle de tamanho à esquerda|**Ctrl+Shift+Seta para a Esquerda**| Edit.SizeControlLeft |
|Grade esquerda do controle de tamanho|**Shift+Seta para a Esquerda**| Edit.SizeControlLeftGrid |
|Controle de tamanho à direita|**Ctrl+Shift+Seta para a direita**| Edit.SizeControlRight |
|Grade direita do controle de tamanho|**Shift+Seta para a direita**| Edit.SizeControlRightGrid |
|Controle de tamanho para cima|**Ctrl+Shift+Seta para Cima**| Edit.SizeControlUp |
|Grade de controle de tamanho para cima|**Shift+Seta para Cima**| Edit.SizeControlUpGrid |
|Parar pesquisa|**Alt+F3, S**| Edit.StopSearch |
|Cercar com|**Ctrl+K, Ctrl+S**| Edit.SurroundWith |
|Desfazer|**Ctrl+Z**<br /><br /> ou<br /><br /> **Alt+Backspace**| Edit.Undo |

### <a name="editor-context-menus"></a><a name="bkmk_editorContext"></a> Menus de contexto do editor

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Condições de ponto de interrupção|**Alt+F9, C**| EditorContextMenus.CodeWindow.Breakpoint.BreakpointConditions |
|Rótulos de edição de ponto de interrupção|**Alt+F9, L**| EditorContextMenus.CodeWindow.Breakpoint.BreakpointEditlabels |
|Mostrar item|**Ctrl+'**| EditorContextMenus.CodeWindow.CodeMap.ShowItem |
|Execute (executar)|**Ctrl+Alt+F5**| EditorContextMenus.CodeWindow.Execute |
|Ir para a exibição|**Ctrl+M, Ctrl+G**| EditorContextMenus.CodeWindow.GoToView |
|Alternar o arquivo de código do header|**Crtl+K, Ctrl+O** (letra "O")| EditorContextMenus.CodeWindow.ToggleHeaderCodeFile |
|Exibir hierarquia de chamada|**Ctrl+K, Ctrl+T**<br /><br /> ou<br /><br /> **Ctrl+K, T**| EditorContextMenus.CodeWindow.ViewCallHierarchy |

### <a name="file"></a><a name="bkmk_file"></a> Arquivo

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Fechar|**Alt+F4**| File.Exit |
|Novo arquivo|**Ctrl+N**| File.NewFile |
|Novo Projeto|**Ctrl+Shift+N**| File.NewProject |
|Novo site|**Shift+Alt+N**| File.NewWebSite |
|Abrir arquivo|**Ctrl+O** (letra "O")| File.OpenFile |
|Abrir projeto|**Ctrl+Shift+O** (letra "O")| File.OpenProject |
|Abrir site|**Shift+Alt+O** (letra "O")| File.OpenWebSite |
|Impressão|**CTRL + P**| File.Print |
|Salvar tudo|**Ctrl + Shift + S**| File.SaveAll |
|Salvar itens selecionados|**Ctrl+S**| File.SaveSelectedItems |
|Exibir no navegador|**CTRL + SHIFT + W**| File.ViewinBrowser |

### <a name="help"></a><a name="bkmk_help"></a> Ajuda

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Adicionar e remover conteúdo da ajuda|**CTRL + ALT + F1**| Help.AddandRemoveHelpContent |
|ajuda F1|**F1**| Help.F1Help |
|Exibir ajuda|**CTRL + F1**| Help.ViewHelp |
|Ajuda da janela|**Shift + F1**| Help.WindowHelp |

### <a name="load-test"></a><a name="bkmk_loadtest"></a> Teste de carga

|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Ir para o painel do contador|**Ctrl+R, Q**| LoadTest.JumpToCounterPane |

### <a name="other-context-menus"></a><a name="bkmk_otherContext"></a> Outros menus de contexto

|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Adicionar novo diagrama|**Inserção**| OtherContextMenus.MicrosoftDataEntityDesignContext.AddNewDiagram |

### <a name="project"></a><a name="bkmk_project"></a> Projeto

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Adicionar item existente|**Shift + Alt + A**| Project.AddExistingItem |
|Adicionar novo item|**Ctrl + Shift + A**| Project.AddNewItem |
|Assistente de classe|**CTRL + SHIFT + X**| Project.ClassWizard |
|Substituições|**Ctrl+Alt+Ins**| Project.Override |
|Visualizar alterações|**Alt+;** e, em seguida, **Alt+C**| Project.Previewchanges |
|Publicar arquivos selecionados|**Alt+;** e, em seguida, **Alt+P**| Project.Publishselectedfiles |
|Substituir arquivos selecionados do servidor|**Alt+;** e, em seguida, **Alt+R**| Project.Replaceselectedfilesfromserver |

### <a name="project-and-solution-context-menus"></a><a name="bkmk_projectContext"></a>menus de contexto de Project e solução

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Mover para baixo|**Alt + seta para baixo**| ProjectandSolutionContextMenus.Item.MoveDown |
|Mover para cima|**Alt+Up Arrow**| ProjectandSolutionContextMenus.Item.MoveUp |

### <a name="refactor"></a><a name="bkmk_refactor"></a> Refatorar

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Encapsular campo|**Ctrl+R, Ctrl+E**| Refactor.EncapsulateField |
|Extrair interface|**Ctrl+R, Ctrl+I**| Refactor.ExtractInterface |
|Extrair método|**Ctrl+R, Ctrl+M**| Refactor.ExtractMethod |
|Remover parâmetros|**Ctrl+R, Ctrl+V**| Refactor.RemoveParameters |
|Renomear|**Ctrl+R, Ctrl+R**| Refactor.Rename |
|Reordenar parâmetros|**Crtl+R, Ctrl+O** (letra "O")| Refactor.ReorderParameters |

### <a name="solution-explorer"></a><a name="bkmk_solutionexplorerGLOBAL"></a> Gerenciador de Soluções

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Abrir filtro de arquivos|**Ctrl+[**, **O** (letra "O")<br /><br /> ou<br /><br /> **Ctrl+[**, **Ctrl+O** (letra "O")| SolutionExplorer.OpenFilesFilter |
|Filtro de alterações pendentes|**Ctrl+[**, **P**<br /><br /> ou<br /><br /> **Ctrl+[**, **Ctrl+P**| SolutionExplorer.PendingChangesFilter |
|Sincronizar com documento ativo|**Ctrl+[**, **S**<br /><br /> ou<br /><br /> **Ctrl+[**, **Ctrl+S**| SolutionExplorer.SyncWithActiveDocument |

### <a name="team"></a><a name="bkmk_team"></a> Equipe

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Vá para branches git|**Ctrl+0** (zero), **Ctrl+N**<br /><br /> ou<br /><br /> **Ctrl+0, N**| Team.Git.GoToGitBranches |
|Ir para alterações do git|**Ctrl+0** (zero), **Ctrl+G**<br /><br /> ou<br /><br /> **Ctrl+0, G**| Team.Git.GoToGitChanges |
|Ir para confirmações do git|**Ctrl+0** (zero), **Ctrl+O** (letra "O")<br /><br /> ou<br /><br /> **Ctrl+0, O**| Team.Git.GoToGitCommits |
|Pesquisa do Team Explorer|**Ctrl+'**| Team.TeamExplorerSearch |

### <a name="team-foundation-context-menus"></a><a name="bkmk_TFcontext"></a> Menus de contexto do Team Foundation

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Ir para builds|**Ctrl+0** (zero), **Ctrl+B**<br /><br /> ou<br /><br /> **Ctrl+0, B**| TeamFoundationContextMenus.Commands.GoToBuilds |
|Ir para se conectar|**Ctrl+0** (zero), **Ctrl+C**<br /><br /> ou<br /><br /> **Ctrl+0, C**| TeamFoundationContextMenus.Commands.GoToConnect |
|Ir para documentos|**Ctrl+0** (zero), **Ctrl+D**<br /><br /> ou<br /><br /> **Ctrl+0, D**| TeamFoundationContextMenus.Commands.GoToDocuments |
|Ir para casa|**Ctrl+0** (zero), **Ctrl+H**<br /><br /> ou<br /><br /> **Ctrl+0, H**| TeamFoundationContextMenus.Commands.GoToHome |
|Vá para meu trabalho|**Ctrl+0** (zero), **Ctrl+M**<br /><br /> ou<br /><br /> **Ctrl+0, M**| TeamFoundationContextMenus.Commands.GoToMyWork |
|Ir para alterações pendentes|**Ctrl+0** (zero), **Ctrl+P**<br /><br /> ou<br /><br /> **Ctrl+0, P**| TeamFoundationContextMenus.Commands.GoToPendingChanges |
|Ir para relatórios|**Ctrl+0** (zero), **Ctrl+R**<br /><br /> ou<br /><br /> **Ctrl+0, R**| TeamFoundationContextMenus.Commands.GoToReports |
|Ir para as configurações|**Ctrl+0** (zero), **Ctrl+S**<br /><br /> ou<br /><br /> **Ctrl+0, S**| TeamFoundationContextMenus.Commands.GoToSettings |
|Acessar a Web|**Ctrl+0** (zero), **Ctrl+A**<br /><br /> ou<br /><br /> **Ctrl+0, A**| TeamFoundationContextMenus.Commands.GoToWebAccess |
|Ir para itens de trabalho|**Ctrl+0** (zero), **Ctrl+W**<br /><br /> ou<br /><br /> **Ctrl+0, W**| TeamFoundationContextMenus.Commands.GoToWorkItems |

### <a name="test"></a><a name="bkmk_test"></a> Teste

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Usar o construtor de teste de IU codificado|**Ctrl+ \\ , Ctrl+C**| Test.UseCodedUITestBuilder |
|Usar a gravação de ação existente|**Ctrl+ \\ , Ctrl+A**| Test.UseExistingActionRecording |

### <a name="test-explorer"></a><a name="bkmk_testexplorerGLOBAL"></a> Gerenciador de Testes

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Depurar todos os testes|**Ctrl+R, Ctrl+A**| TestExplorer.DebugAllTests |
|Depurar todos os testes no contexto|**Ctrl+R, Ctrl+T**| TestExplorer.DebugAllTestsInContext |
|Depurar última executado|**Ctrl+R, D**| TestExplorer.DebugLastRun |
|Repetir a última executar|**Ctrl+R, L**| TestExplorer.RepeatLastRun |
|Executar todos os testes|**Ctrl+R, A**| TestExplorer.RunAllTests |
|Executar todos os testes no contexto|**Ctrl+R, T**| TestExplorer.RunAllTestsInContext |
|Mostrar o explorador de testes|**Ctrl+E, T**| TestExplorer.ShowTestExplorer |
|Abrir guia|**Ctrl+E, L**| LiveUnitTesting.OpenTab |
|Resultados da cobertura de código|**Ctrl+E, C**| Test.CodeCoverageResults |

### <a name="tools"></a><a name="bkmk_tools"></a> Ferramentas

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Anexar ao processo|**Ctrl+Alt+P**| Tools.AttachtoProcess |
|Gerenciador de snippets de código|**Ctrl+K, Ctrl+B**| Tools.CodeSnippetsManager |
|Forçar gc|**Ctrl+Shift+Alt+F12, Ctrl+Shift+Alt+F12**| Tools.ForceGC |

### <a name="view"></a><a name="bkmk_view"></a> Ver

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Todas as janelas|**Shift+Alt+M**| View.AllWindows |
|Gerenciador de arquitetura|**Ctrl+ \\ , Ctrl+R**| View.ArchitectureExplorer |
|Para Trás|**Alt+Seta para a esquerda** (funciona de maneira diferente do View.NavigateBackward no editor de texto)| View.Backward |
|Janela indicador|**Ctrl+K, Ctrl+W**| View.BookmarkWindow |
|Navegue em seguida|**Ctrl+Shift+1**| View.BrowseNext |
|Procurar anteriormente|**Ctrl+Shift+2**| View.BrowsePrevious |
|Hierarquia de chamadas|**Ctrl+Alt+K**| View.CallHierarchy |
|Exibição de classe|**Ctrl+Shift+C**| View.ClassView |
|A exibição de classe vai para a combinação de pesquisa|**Ctrl+K, Ctrl+V**| View.ClassViewGoToSearchCombo |
|Janela de definição de código|**Ctrl+ \\ , D**<br /><br /> ou<br /><br /> **Ctrl+ \\ , Ctrl+D**| View.CodeDefinitionWindow |
|Janela Comando|**Ctrl+Alt+A**| View.CommandWindow |
|Fontes de dados|**Shift+Alt+D**| View.DataSources |
|Contorno do documento|**Ctrl+Alt+T**| View.DocumentOutline |
|Editar rótulo|**F2**| View.EditLabel |
|Lista de erros|**Ctrl+ \\ , E**<br /><br /> ou<br /><br /> **CTRL + \\ , CTRL + e**| View.ErrorList |
|F# interativo|**CTRL + ALT + F**| View.F#Interactive |
|Localizar resultados de símbolo|**Ctrl+Alt+F12**| View.FindSymbolResults |
|Encaminhar|**Alt+Seta para a direita** (funciona de maneira diferente do View.NavigateForward no editor de texto)| View.Forward |
|Contexto de navegação progressiva|**Ctrl + Shift + 7**| View.ForwardBrowseContext |
|Tela inteira|**Shift + Alt + Enter**| View.FullScreen |
|Navegar para trás|**CTRL +-**| View.NavigateBackward |
|Navegar para frente|**Ctrl + Shift +-**| View.NavigateForward |
|Próximo erro|**CTRL + SHIFT + F12**| View.NextError |
|Notificações|**Ctrl+W, N**<br /><br /> ou<br /><br /> **Ctrl+W, Ctrl+N**| View.Notifications |
|Pesquisador de objetos|**CTRL + ALT + J**| View.ObjectBrowser |
|Pesquisador de objetos ir para a combinação Pesquisar|**Ctrl+K, Ctrl+R**| View.ObjectBrowserGoToSearchCombo |
|Saída|**Ctrl+Alt+O** (letra "O")| View.Output |
|Contexto de navegação pop|**Ctrl+Shift+8** (somente C++)| View.PopBrowseContext |
|Janela de Propriedades|**F4**| View.PropertiesWindow |
|Páginas de propriedades|**Shift+F4**| View.PropertyPages |
|Exibição de recurso|**Ctrl + Shift + E**| View.ResourceView |
|Gerenciador de servidores|**Ctrl + Alt + S**| View.ServerExplorer |
|Mostrar marca inteligente|**Shift + Alt + F10**<br /><br /> ou<br /><br /> **CTRL +.**| View.ShowSmartTag |
|Gerenciador de soluções|**CTRL + ALT + L**| View.SolutionExplorer |
|pesquisador de objetos do SQL server|**CTRL + \\ , CTRL + S**| View.SQLServerObjectExplorer |
|Lista de tarefas|**CTRL + \\ , T**<br /><br /> ou<br /><br /> **CTRL + \\ , CTRL + T**| View.TaskList |
|Gerenciador de equipe do TFS|**CTRL + \\ , CTRL + M**| View.TfsTeamExplorer |
|Caixa de Ferramentas|**CTRL + ALT + X**| View.Toolbox |
|Gerenciador de modelos UML|**CTRL + \\ , Ctrl + U**| View.UMLModelExplorer |
|Exibir código|**F7**| View.ViewCode |
|Designer de exibição|**Shift+F7**| View.ViewDesigner |
|Navegador da Web|**CTRL + ALT + R**| View.WebBrowser |
|Ampliar|**Ctrl + Shift +.**| View.ZoomIn |
|Reduzir|**Ctrl + Shift +,**| View.ZoomOut |
|Mostrar Gerenciador de testes|**CTRL + E, T**| TestExplorer.ShowTestExplorer |

### <a name="window"></a><a name="bkmk_window"></a> Window

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Ativar janela do documento|**Esc**| Window.ActivateDocumentWindow |
|Adicionar guia à seleção|**Ctrl+Shift+Alt+Space**| Window.AddTabtoSelection |
|Fechar janela do documento|**CTRL + F4**| Window.CloseDocumentWindow |
|Fechar janela de ferramentas|**SHIFT + ESC**| Window.CloseToolWindow |
|Manter guia aberta|**Ctrl+Alt+Home**| Window.KeepTabOpen |
|Mover para a barra de navegação|**Ctrl+F2**| Window.MovetoNavigationBar |
|Próxima janela do documento|**Ctrl + F6**| Window.NextDocumentWindow |
|Navegar na próxima janela do documento|**Ctrl + Tab**| Window.NextDocumentWindowNav |
|Próximo painel|**Alt + F6**| Window.NextPane |
|Próximo painel de divisão|**F6**| Window.NextSplitPane |
|Próxima guia|**Ctrl+Alt+PgDn**<br /><br /> ou<br /><br /> **Ctrl+PgDn**| Window.NextTab |
|Próxima guia e adicionar à seleção|**Ctrl+Shift+Alt+PgDn**| Window.NextTabandAddtoSelection |
|Navegar na próxima janela de ferramentas|**ALT + F7**| Window.NextToolWindowNav |
|Janela anterior do documento|**Ctrl + Shift + F6**| Window.PreviousDocumentWindow |
|Navegar na janela anterior do documento|**Ctrl + Shift + Tab**| Window.PreviousDocumentWindowNav |
|Painel anterior|**Shift + Alt + F6**| Window.PreviousPane |
|Painel de divisão anterior|**Shift+F6**| Window.PreviousSplitPane |
|Guia Anterior|**Ctrl+Alt+PgUp**<br /><br /> ou<br /><br /> **Ctrl+PgUp**| Window.PreviousTab |
|Guia anterior e adicionar à seleção|**Ctrl+Shift+Alt+PgUp**| Window.PreviousTabandAddtoSelection |
|Navegação na janela de ferramentas anterior|**SHIFT + ALT + F7**| Window.PreviousToolWindowNav |
|Início rápido|**Ctrl+Q**| Window.QuickLaunch |
|Categoria anterior de início rápido|**CTRL + SHIFT + Q**| Window.QuickLaunchPreviousCategory |
|Mostrar menu de encaixe|**Alt +-**| Window.ShowDockMenu |
|Mostrar lista de arquivos MDI ex|**Ctrl + Alt + seta para baixo**| Window.ShowEzMDIFileList |
|Pesquisa do Gerenciador de soluções|**CTRL +;**| Window.SolutionExplorerSearch |
|Pesquisa de janela|**ALT + '**| Window.WindowSearch |

### <a name="azure"></a><a name="bkmk_windowsazure"></a> Azure

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Repetir operação de script do serviço móvel|**CTRL + num \* , CTRL + R**| WindowsAzure.RetryMobileServiceScriptOperation |
|Mostrar detalhes do erro de script do serviço móvel|**CTRL + num \* , CTRL + D**| WindowsAzure.ShowMobileServiceScriptErrorDetails |

## <a name="context-specific-shortcuts"></a>Atalhos específicos de contexto


### <a name="adonet-entity-data-model-designer"></a>Designer de Modelo de Dados de Entidade ADO.NET

Os atalhos específicos para esse contexto são:

|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Down|**Alt+Seta para Baixo**| OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.Down |
|5 inomoss|**Alt+PgDn**| OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.Down5 |
|Para baixo|**Alt+End**| OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.ToBottom |
|Para cima|**Alt+Home**| OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.ToTop |
|Up|**Alt+Up Arrow**| OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.Up |
|Até 5|**Alt+PgUp**| OtherContextMenus.MicrosoftDataEntityDesignContext.MoveProperties.Up5 |
|Renomear|**Ctrl+R, R**| OtherContextMenus.MicrosoftDataEntityDesignContext.Refactor.Rename |
|Remover do diagrama|**Shift+Del**| OtherContextMenus.MicrosoftDataEntityDesignContext.RemovefromDiagram |
|Navegador de modelo de dados de entidade|**Ctrl+1**| View.EntityDataModelBrowser |
|Detalhes de mapeamento do modelo de dados de entidade|**Ctrl+2**| View.EntityDataModelMappingDetails |

### <a name="class-diagram"></a>Diagrama de classe

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Recolher|**Num –**| ClassDiagram.Collapse |
|Expanda|**Num +**| ClassDiagram.Expand |
|Excluir|**Ctrl+Del**| Edit.Delete |
|Expandir lista de tipos base de ressupsução|**Shift+Alt+B**| Edit.ExpandCollapseBaseTypeList |
|Navegue até lollipop|**Shift+Alt+L**| Edit.NavigateToLollipop |
|Remover do diagrama|**Excluir**| Edit.RemovefromDiagram |
|Exibir código|**Enter**| View.ViewCode |

### <a name="coded-ui-test-editor"></a>Editor de Testes de Interface de Usuário Codificada

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Copiar referência para área de transferência|**Ctrl+C**| OtherContextMenus.UITestEditorContextMenu.CopyReferencetoClipboard |
|Inserir atraso antes|**Ctrl+Alt+D**| OtherContextMenus.UITestEditorContextMenu.InsertDelayBefore |
|Localizar todos|**Shift+Alt+L**| OtherContextMenus.UITestEditorContextMenu.LocateAll |
|Localizar o controle de interface do usuário|**Ctrl+Shift+L**| OtherContextMenus.UITestEditorContextMenu.LocatetheUIControl |
|Mover o código|**Ctrl+Alt+C**| OtherContextMenus.UITestEditorContextMenu.Movecode |
|Dividir em um novo método|**Ctrl+Shift+T**| OtherContextMenus.UITestEditorContextMenu.Splitintoanewmethod |

### <a name="dataset-editor"></a>Editor de Conjunto de Dados

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Inserir coluna|**Inserção**| OtherContextMenus.ColumnContext.InsertColumn |
|Coluna|**Ctrl+L**| OtherContextMenus.DbTableContext.Add.Column |

### <a name="difference-viewer"></a>Visualizador de Diferenças

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Ignorar espaço em branco de corte|**Ctrl+ \\ , Ctrl+Barra de Espaços**| Diff.IgnoreTrimWhitespace |
|Exibição em linha|**Ctrl+ \\ , Ctrl+1**| Diff.InlineView |
|Exibição somente à esquerda|**Ctrl+ \\ , Ctrl+3**| Diff.LeftOnlyView |
|Próxima diferença|**F8**| Diff.NextDifference |
|Diferença anterior|**Shift+F8**| Diff.PreviousDifference |
|Exibição somente à direita|**Ctrl+ \\ , Ctrl+4**| Diff.RightOnlyView |
|Exibição lado a lado|**Ctrl+ \\ , Ctrl+2**| Diff.SideBySideView |
|Alternar entre a esquerda e a direita|**Ctrl+ \\ , Ctrl+Tab**| Diff.SwitchBetweenLeftAndRight |
|Sincronizar alternância de exibição|**Ctrl+ \\ , Ctrl+Seta para Baixo**| Diff.SynchronizeViewToggle |
|Adicionar comentário|**Ctrl+Shift+K**| EditorContextMenus.CodeWindow.AddComment |
|Editar arquivo local|**Ctrl+Shift+P**| EditorContextMenus.CodeWindow.EditLocalFile |

### <a name="dom-explorer"></a>Explorador do DOM

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Atualizar|**F5**| DOMExplorer.Refresh |
|Selecionar elemento|**Ctrl+B**| DOMExplorer.SelectElement |
|Mostrar layout|**Ctrl+Shift+I**| DOMExplorer.ShowLayout |

### <a name="f-interactive"></a>F# interativo

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Cancelar avaliação interativa|**Ctrl+Break**| OtherContextMenus.FSIConsoleContext.CancelInteractiveEvaluation |

### <a name="graph-document-editor"></a>Editor de Documento Gráfico

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Adicionar nó|**Inserção**| ArchitectureContextMenus.DirectedGraphContextMenu.Advanced.Add.AddNode |
|Ambas as dependências|**B**| ArchitectureContextMenus.DirectedGraphContextMenu.Advanced.Select.BothDependencies |
|Dependências de entrada|**Eu**| ArchitectureContextMenus.DirectedGraphContextMenu.Advanced.Select.IncomingDependencies |
|Dependências de saída|**O**| ArchitectureContextMenus.DirectedGraphContextMenu.Advanced.Select.OutgoingDependencies |
|Novo comentário|**Ctrl+Shift+K**<br /><br /> ou<br /><br /> **Ctrl+E, C**| ArchitectureContextMenus.DirectedGraphContextMenu.NewComment |
|Remover|**Excluir**| ArchitectureContextMenus.DirectedGraphContextMenu.Remove |
|Renomear|**F2**| ArchitectureContextMenus.DirectedGraphContextMenu.Rename |

### <a name="graphics-diagnostics"></a>Diagnóstico de gráfico

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Quadro de captura|Nenhum| Debug.Graphics.CaptureFrame |
|Mover a seleção de pixel para baixo|**Shift+Alt+Seta para baixo**| Gráficos.MoverSeleçãoDePixelParaBaixo |
|Mover a seleção de pixel para a esquerda|**Shift+Alt+Seta para a Esquerda**| Gráficos.MoverSeleçãoDePixelParaEsquerda |
|Mover a seleção de pixel para a direita|**Shift+Alt+Seta para a Direita**| Gráficos.MoverSeleçãoDePixelParaDireita |
|Mover a seleção de pixel para cima|**Shift+Alt+Seta para Cima**| Gráficos.MoverSeleçãodePixelParaCima |
|Aplicar zoom para o tamanho real|**Shift+Alt+0** (zero)| Gráficos.AplicarZoomParaTamanhoReal |
|Aplicar zoom para ajustar à janela|**Shift+Alt+9**| Gráficos.AplicarParaAjustarJanela |
|Ampliar|**Shift + Alt + =**| Gráficos.Ampliar |
|Reduzir|**Shift + Alt +-**| Gráficos.Reduzir |

### <a name="html-editor"></a>Editor de HTML

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Ir para o controlador|**Ctrl+M, Ctrl+G**| OtherContextMenus.HTMLContext.GoToController |

### <a name="html-editor-design-view"></a>Exibição de Design do Editor HTML

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Mover controle para baixo|**CTRL + seta para baixo**| Edit.MoveControlDown |
|Mover controle para cima|**CTRL + seta para cima**| Edit.MoveControlUp |
|Negrito|**CTRL + B**| Format.Bold |
|Converter em hiperlink|**CTRL + L**| Format.ConverttoHyperlink |
|Inserir indicador|**Ctrl+Shift+L**| Format.InsertBookmark |
|Itálico|**Ctrl+I**| Format.Italic |
|Underline|**Ctrl+U**| Format.Underline |
|Adicionar página de conteúdo|**Ctrl+M, Ctrl+C**| Project.AddContentPage |
|Coluna à esquerda|**Ctrl + Alt + seta para a esquerda**| Table.ColumntotheLeft |
|Coluna à direita|**Ctrl+Alt+Seta para a Direita**| Table.ColumntotheRight |
|Linha acima|**Ctrl + Alt + seta para cima**| Table.RowAbove |
|Linha abaixo|**Ctrl + Alt + seta para baixo**| Table.RowBelow |
|Controles net não visuais|**Ctrl + Shift + N**| View.ASP.NETNonvisualControls |
|Editar mestre|**CTRL + M, CTRL + M**| View.EditMaster |
|Próxima exibição|**Ctrl+PgDn**| View.NextView |
|Mostrar marca inteligente|**Shift + Alt + F10**| View.ShowSmartTag |
|Exibir marcação|**Shift+F7**| View.ViewMarkup |
|Guia Anterior|**Ctrl+PgUp**| Window.PreviousTab |

### <a name="html-editor-source-view"></a>Modo Código-Fonte do Editor de HTML

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Ir para o controlador|**Ctrl+M, Ctrl+G**| OtherContextMenus.HTMLContext.GoToController |
|Próxima exibição|**Ctrl+PgDn**| View.NextView |
|Sincronizar exibições|**Ctrl+Shift+Y**| View.SynchronizeViews |
|Designer de exibição|**Shift+F7**| View.ViewDesigner |
|Guia Anterior|**Ctrl+PgUp**| Window.PreviousTab |

### <a name="layer-diagram"></a>Diagrama de camada

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Excluir|**Shift + Delete**| Edit.Delete |

### <a name="managed-resources-editor"></a>Editor de Recursos Gerenciados

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Editar célula|**F2**| Edit.EditCell |
|Remover|**Excluir**| Edit.Remove |
|Remover linha|**Ctrl + Delete**| Edit.RemoveRow |
|Cancelar seleção|**Escape**| Edit.SelectionCancel |
|Áudio|**CTRL + 4**| Resources.Audio |
|Arquivos|**CTRL + 5**| Resources.Files |
|Ícones|**CTRL + 3**| Resources.Icons |
|Imagens|**Ctrl + 2**| Resources.Images |
|Outro|**CTRL + 6**| Resources.Other |
|Cadeias de caracteres|**Ctrl + 1**| Resources.Strings |

### <a name="merge-editor-window"></a>Janela do Editor de Mesclagem

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Definir foco na janela esquerda|**Alt+1**| TeamFoundationContextMenus.MergeContextMenu.SetFocusonLeftWindow |
|Definir foco na janela de resultados|**Alt+2**| TeamFoundationContextMenus.MergeContextMenu.SetFocusonResultWindow |
|Definir foco na janela direita|**Alt+3**| TeamFoundationContextMenus.MergeContextMenu.SetFocusonRightWindow |

### <a name="microsoft-sql-server-data-tools-schema-compare"></a>Microsoft SQL Server Data Tools, Comparação de Esquemas

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Comparação de comparação entre esquemas SSDT|**Shift+Alt+C**| SQL.SSDTSchemaCompareCompare |
|Script de geração de comparação de esquema SSDT|**Shift+Alt+G**| SQL.SSDTSchemaCompareGenerateScript |
|Próxima alteração de comparação do esquema SSDT|**Shift + Alt +.**| SQL.SSDTSchemaCompareNextChange |
|SSDT esquema comparar alteração anterior|**Shift + Alt +,**| SQL.SSDTSchemaComparePreviousChange |
|Parada de comparação do esquema SSDT|**Alt + Break**| SQL.SSDTSchemaCompareStop |
|SSDT o esquema de comparação de atualizações de gravação|**Shift+Alt+U**| SQL.SSDTSchemaCompareWriteUpdates |

### <a name="microsoft-sql-server-data-tools-table-designer"></a>Microsoft SQL Server Data Tools, Designer de Tabela

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|CommitAllEdits|**Shift+Alt+U**|
|Expandir caracteres curinga|**Ctrl+R, E**<br /><br /> ou<br /><br /> **Ctrl+R, Ctrl+E**| SQL.ExpandWildcards |
|Qualificar nomes totalmente|**Ctrl+R, Q**<br /><br /> ou<br /><br /> **Ctrl+R, Ctrl+Q**| SQL.FullyqualifyNames |
|Mover para o esquema|**Ctrl+R, M**<br /><br /> ou<br /><br /> **Ctrl+R, Ctrl+M**| SQL.MovetoSchema |
|Renomear|**F2**<br /><br /> ou<br /><br /> **Ctrl+R, R**<br /><br /> ou<br /><br /> **Ctrl+R, Ctrl+R**| SQL.Rename |
|ViewFileInScriptPanel|**Shift+Alt+PgDn**| |

### <a name="microsoft-sql-server-data-tools-t-sql-editor"></a>Microsoft SQL Server Data Tools, Editor T-SQL

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|CommitAllEdits|**Shift+Alt+U**|
|Executar com depurador|**Alt + F5**| SQL.ExecuteWithDebugger |
|Expandir caracteres curinga|**Ctrl+R, E**<br /><br /> ou<br /><br /> **Ctrl+R, Ctrl+E**| SQL.ExpandWildcards |
|Qualificar nomes totalmente|**Ctrl+R, Q**<br /><br /> ou<br /><br /> **Ctrl+R, Ctrl+Q**| SQL.FullyqualifyNames |
|Mover para o esquema|**Ctrl+R, M**<br /><br /> ou<br /><br /> **Ctrl+R, Ctrl+M**| SQL.MovetoSchema |
|Renomear|**F2**<br /><br /> ou<br /><br /> **Ctrl+R, R**<br /><br /> ou<br /><br /> **Ctrl+R, Ctrl+R**| SQL.Rename |
|T SQL editor cancela a consulta|**Alt + Break**| SQL.TSqlEditorCancelQuery |
|T SQL editor executa a consulta|**Ctrl + Shift + E**| SQL.TSqlEditorExecuteQuery |
|T SQL o editor de resultados como arquivo|**Ctrl+D, F**| SQL.TSqlEditorResultsAsFile |
|T SQL o editor de resultados como grade|**Ctrl+D, G**| SQL.TSqlEditorResultsAsGrid |
|T SQL o editor de resultados como texto|**Ctrl+D, T**| SQL.TSqlEditorResultsAsText |
|T SQL editor mostrar plano estimado|**Ctrl+D, E**| SQL.TSqlEditorShowEstimatedPlan |
|T SQL editor alternar plano de execução|**Ctrl+D, A**| SQL.TSqlEditorToggleExecutionPlan |
|T SQL editor alternar o painel de resultados|**Ctrl+D, R**| SQL.TSqlEditorToggleResultsPane |
|T SQL o clone do editor de consulta|**Ctrl + Alt + N**|SQL. TSqlEditorCloneQuery |
|combinação de banco de dados do editor de SQL T|**Shift+Alt+PgDn**|SQL. TSqlEditorDatabaseCombo |

### <a name="microsoft-sql-server-data-tools-t-sql-pdw-editor"></a>Microsoft SQL Server Data Tools, Editor T-SQL PDW

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|T SQL editor cancela a consulta|**Alt + Break**| SQL.TSqlEditorCancelQuery |
|T SQL editor executa a consulta|**Ctrl + Shift + E**| SQL.TSqlEditorExecuteQuery |
|T SQL o editor de resultados como arquivo|**Ctrl+D, F**| SQL.TSqlEditorResultsAsFile |
|T SQL o editor de resultados como grade|**Ctrl+D, G**| SQL.TSqlEditorResultsAsGrid |
|T SQL o editor de resultados como texto|**Ctrl+D, T**| SQL.TSqlEditorResultsAsText |
|T SQL editor mostrar plano estimado|**Ctrl+D, E**| SQL.TSqlEditorShowEstimatedPlan |
|T SQL editor alternar plano de execução|**Ctrl+D, A**| SQL.TSqlEditorToggleExecutionPlan |
|T SQL editor alternar o painel de resultados|**Ctrl+D, R**| SQL.TSqlEditorToggleResultsPane |
|Consulta de clonagem SQL editor T|**Ctrl+Alt+N**|SQL. TSqlEditorCloneQuery |
|Consulta de clonagem SQL editor T|**Shift+Alt+PgDn**|SQL. TSqlEditorCloneQuery |

### <a name="page-inspector"></a>Inspetor de Página

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Minimizar|**F12**| PageInspector.Minimize |

### <a name="query-designer"></a>Designer de Consulta

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Cancelar a recuperação de dados|**Ctrl+T**| QueryDesigner.CancelRetrievingData |
|Critérios|**Ctrl+2**| QueryDesigner.Criteria |
|Diagrama|**Ctrl+1**| QueryDesigner.Diagram |
|Executar SQL|**Ctrl+R**| QueryDesigner.ExecuteSQL |
|Linha Goto|**Ctrl+G**| QueryDesigner.GotoRow |
|Modo de junção|**Ctrl+Shift+J**| QueryDesigner.JoinMode |
|Resultados|**Ctrl+4**| QueryDesigner.Results |
|Sql|**Ctrl+3**| QueryDesigner.SQL |

### <a name="query-results"></a>Resultados da consulta

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Nova linha de resultados da consulta|**Alt+End**| SQL.QueryResultsNewRow |
|Atualização de resultados da consulta|**Shift+Alt+R**| SQL.QueryResultsRefresh |
|Parar resultados da consulta|**Alt+Break**| SQL.QueryResultsStop |

### <a name="report-designer"></a>Designer de Relatórios

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Linha de quebra|**Enter**| Edit.BreakLine |
|Char left|**Seta para a esquerda**| Edit.CharLeft |
|Extensão à esquerda do caractere|**Shift+Seta para a Esquerda**| Edit.CharLeftExtend |
|Char right|**Seta para a direita**| Edit.CharRight |
|Estender à direita do caractere|**Shift+Seta para a direita**| Edit.CharRightExtend |
|Guia Inserir|**Tab**| Edit.InsertTab |
|Uma linha abaixo|**Seta para baixo**| Edit.LineDown |
|Extensão de linha para baixo|**Shift+Seta para Baixo**| Edit.LineDownExtend |
|Uma linha acima|**Seta para cima**| Edit.LineUp |
|Extensão de linha|**Shift+Seta para Cima**| Edit.LineUpExtend |
|Mover o controle para baixo|**Ctrl+Seta para Baixo**| Edit.MoveControlDown |
|Mover o controle para a esquerda|**Ctrl+Seta para a Esquerda**| Edit.MoveControlLeft |
|Mover o controle para a direita|**Ctrl+Seta para a Direita**| Edit.MoveControlRight |
|Mover o controle para cima|**Ctrl+Seta para Cima**| Edit.MoveControlUp |
|Cancelamento da seleção|**Esc**| Edit.SelectionCancel |
|Controle de tamanho reduzido|**Ctrl+Shift+Seta para Baixo**| Edit.SizeControlDown |
|Controle de tamanho à esquerda|**Ctrl+Shift+Seta para a Esquerda**| Edit.SizeControlLeft |
|Controle de tamanho à direita|**Ctrl+Shift+Seta para a direita**| Edit.SizeControlRight |
|Controle de tamanho para cima|**Ctrl+Shift+Seta para Cima**| Edit.SizeControlUp |
|Guia à esquerda|**Shift+Tab**| Edit.TabLeft |
|dados de relatório|**Ctrl+Alt+D**| View.ReportData |

### <a name="sequence-diagram"></a>Diagrama de sequência

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Navegar até o código|**F12**| ArchitectureDesigner.Sequence.NavigateToCode |
|Excluir|**Shift+Del**| Edit.Delete |

### <a name="settings-designer"></a>Designer de Configurações

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Editar célula|**F2**| Edit.EditCell |
|Remover linha|**Ctrl+Excluir**| Edit.RemoveRow |
|Cancelamento da seleção|**Esc**| Edit.SelectionCancel |
|Exibir código|**F7**| View.ViewCode |

### <a name="solution-explorer"></a>Gerenciador de Soluções

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Exibir no inspetor de página|**Ctrl+K, Ctrl+G**| ClassViewContextMenus.ClassViewProject.View.ViewinPageInspector |

### <a name="team-explorer"></a>Team Explorer

Os atalhos específicos para esse contexto são:


|Comando|Atalho do Teclado|ID do comando|
|-|-|-|
|Excluir|**Excluir**| Edit.Delete |
|Renomear|**F2**| File.Rename |
|Ir para a navegação do Team Explorer|**Alt+Home**| TeamFoundationContextMenus.Commands.GoToTeamExplorerNavigation |
|Acesse o conteúdo da próxima seção do Team Explorer|**Alt+Seta para Baixo**| TeamFoundationContextMenus.Commands.GoToTeamExplorerNextSectionContent |
|Ir para o conteúdo da página do Team Explorer|**Alt+0** (zero)| TeamFoundationContextMenus.Commands.GoToTeamExplorerPageContent |
|Acesse o conteúdo da seção anterior do Team Explorer|**Alt+Up Arrow**| TeamFoundationContextMenus.Commands.GoToTeamExplorerPreviousSectionContent |
|Acesse o conteúdo da seção 1 do Team Explorer|**Alt+1**| TeamFoundationContextMenus.Commands.GoToTeamExplorerSection1Content |
|Acesse o conteúdo da seção 2 do Team Explorer|**Alt+2**| TeamFoundationContextMenus.Commands.GoToTeamExplorerSection2Content |
|Acesse o conteúdo da seção 3 do Team Explorer|**Alt+3**| TeamFoundationContextMenus.Commands.GoToTeamExplorerSection3Content |
|Acesse o conteúdo da seção 4 do Team Explorer|**Alt+4**| TeamFoundationContextMenus.Commands.GoToTeamExplorerSection4Content |
|Acesse o conteúdo da seção 5 do Team Explorer|**Alt+5**| TeamFoundationContextMenus.Commands.GoToTeamExplorerSection5Content |
|Acesse o conteúdo da seção 6 do Team Explorer|**Alt+6**| TeamFoundationContextMenus.Commands.GoToTeamExplorerSection6Content |
|Ir para conteúdo da seção 7 do Team Explorer|**Alt+7**| TeamFoundationContextMenus.Commands.GoToTeamExplorerSection7Content |
|Ir para conteúdo da seção 8 do Team Explorer|**Alt+8**| TeamFoundationContextMenus.Commands.GoToTeamExplorerSection8Content |
|Ir para conteúdo da seção 9 do Team Explorer|**Alt+9**| TeamFoundationContextMenus.Commands.GoToTeamExplorerSection9Content |
|Navegar para trás do Team Explorer|**Alt+Left Arrow**| TeamFoundationContextMenus.Commands.TeamExplorerNavigateBackward |
|Navegação para frente do Team Explorer|**Alt+Right Arrow**| TeamFoundationContextMenus.Commands.TeamExplorerNavigateForward |
|Contexto do TFS minha página de trabalho criar cópia Wi|**Shift+Alt+C**| TeamFoundationContextMenus.MyWorkPageInProgress.TfsContextMyWorkPageCreateCopyWI |
|Contexto do TFS minha página de trabalho novo Wi vinculado|**Shift+Alt+L**| TeamFoundationContextMenus.MyWorkPageInProgress.TfsContextMyWorkPageNewLinkedWI |
|Atualizar|**F5**| View.Refresh |

### <a name="test-explorer"></a>Gerenciador de Testes

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Abrir teste|**F12**| TestExplorer.OpenTest |

### <a name="text-editor"></a>Editor de Texto

Os atalhos específicos para esse contexto são:


| Comandos | Atalhos de teclado |ID do comando|
|-|-|-|
|Linha de quebra| **Enter**<br /><br /> ou<br /><br /> **Shift+Enter** | Edit.BreakLine |
|Caractere à esquerda| **Seta para a esquerda** | Edit.CharLeft |
|Estender caractere à esquerda| **Shift + seta para a esquerda** | Edit.CharLeftExtend |
|Estender coluna para a esquerda do caractere| **Shift + Alt + seta para a esquerda** | Edit.CharLeftExtendColumn |
|Caractere à direita| **Seta para a direita** | Edit.CharRight |
|Estender caractere à direita| **Shift + seta para a direita** | Edit.CharRightExtend |
|Estender coluna para direita do caractere| **Shift + Alt + seta para a direita** | Edit.CharRightExtendColumn |
|Limpar indicadores| **CTRL + K, CTRL + L** | Edit.ClearBookmarks |
|Recolher toda a estrutura de tópicos| **CTRL + M, CTRL + A** | Edit.CollapseAllOutlining |
|Recolher região atual| **CTRL + M, CTRL + S** | Edit.CollapseCurrentRegion |
|Recolher marca| **Ctrl+M, Ctrl+T** | Edit.CollapseTag |
|Recolher para definições| **Ctrl+M, Ctrl+O** (letra "O") | Edit.CollapseToDefinitions |
|Seleção de contrato| **Shift + Alt +-** | Edit.ContractSelection |
|Seleção de comentário| **CTRL + K, CTRL + C** | Edit.CommentSelection |
|Completar a palavra| **CTRL + espaço**<br /><br /> ou<br /><br /> **Alt+Right Arrow** | Edit.CompleteWord |
|Copiar dica de parâmetro| **Ctrl + Shift + Alt + C** | Edit.CopyParameterTip |
|Diminuir nível de filtro| **ALT +,** | Edit.DecreaseFilterLevel |
|Excluir versões anteriores| **Backspace**<br /><br /> ou<br /><br /> **Shift+Bkspce** | Edit.DeleteBackwards |
|Excluir espaço em branco horizontal| **Ctrl+K, Ctrl+\\** | Edit.DeleteHorizontalWhiteSpace |
|Fim do documento| **Ctrl+End** | Edit.DocumentEnd |
|Extensão de fim do documento| **Ctrl+Shift+End** | Edit.DocumentEndExtend |
|Início do documento| **Ctrl+Home** | Edit.DocumentStart |
|Extensão de início do documento| **Ctrl+Shift+Home** | Edit.DocumentStartExtend |
|Expandir toda a delineamento| **Ctrl+M, Ctrl+X** | Edit.ExpandAllOutlining |
|Expandir região atual| **Ctrl+M, Ctrl+E** | Edit.ExpandCurrentRegion |
|Expandir seleção| **Shift+Alt+=** | Edit.ExpandSelection |
|Expandir a seleção para o bloco de contenção| **Shift+Alt+]** | Edit.ExpandSelectiontoContainingBlock |
|Formatar documento| **Ctrl+K, Ctrl+D** | Edit.FormatDocument |
|Formatar seleção| **Ctrl+K, Ctrl+F** | Edit.FormatSelection |
|Goto all| **Ctrl+T**<br /><br /> ou<br /><br /> **Ctrl+,** | Edit.GotoAll |
|Chave de goto| **Ctrl+]** | Edit.GotoBrace |
|Extensão de chave goto| **Ctrl+Shift+]** | Edit.GotoBraceExtend |
|Goto recente| **Ctrl+T, R** | Edit.GotoRecent |
|Próximo problema no arquivo Goto| **Alt+PgDn** | Edit.GotoNextIssueinFile |
|Problema anterior do Goto no arquivo| **Alt+PgUp** | Edit.GotoPreviousIssueinFile |
|Ocultar seleção| **Ctrl+M, Ctrl+H** | Edit.HideSelection |
|Aumentar o nível de filtro| **Alt+.** | Edit.IncreaseFilterLevel |
|Pesquisa incremental| **Ctrl+I** | Edit.IncrementalSearch |
|Inserir a caretas em todas as correspondências| **Shift+Alt+;** | Edit.InsertCaretsatAllMatching |
|Inserir o próximo a caret correspondente| **Shift+Alt+.** | Edit.InsertNextMatchingCaret |
|Guia Inserir| **Tab** | Edit.InsertTab |
|Corte de linha| **Ctrl+L** | Edit.LineCut |
|Exclusão de linha| **Ctrl+Shift+L** | Edit.LineDelete |
|Uma linha abaixo| **Seta para baixo** | Edit.LineDown |
|Extensão de linha para baixo| **Shift+Seta para Baixo** | Edit.LineDownExtend |
|Coluna de extensão de linha para baixo| **Shift+Alt+Seta para baixo** | Edit.LineDownExtendColumn |
|Fim da linha| **Final** | Edit.LineEnd |
|Extensão de extremidade de linha| **Shift+End** | Edit.LineEndExtend |
|Coluna de extensão de extremidade de linha| **Shift+Alt+End** | Edit.LineEndExtendColumn |
|Linha aberta acima| **Ctrl+Enter** | Edit.LineOpenAbove |
|Linha aberta abaixo| **Ctrl+Shift+Enter** | Edit.LineOpenBelow |
|Início da linha| **Início** | Edit.LineStart |
|Estender início da linha| **Shift + página inicial** | Edit.LineStartExtend |
|Estender coluna de início de linha| **Shift + Alt + Home** | Edit.LineStartExtendColumn |
|Transpor linha| **Shift + Alt + T** | Edit.LineTranspose |
|Uma linha acima| **Seta para cima** | Edit.LineUp |
|Estender linha acima| **Shift + seta para cima** | Edit.LineUpExtend |
|Estender coluna para cima na linha| **Shift+Alt+Seta para Cima** | Edit.LineUpExtendColumn |
|Listar os membros| **CTRL + J** | Edit.ListMembers |
|Tornar minúsculas| **Ctrl+U** | Edit.MakeLowercase |
|Colocar em maiúsculas| **Ctrl + Shift + U** | Edit.MakeUppercase |
|Mover linhas selecionadas para baixo| **Alt + seta para baixo** | Edit.MoveSelectedLinesDown |
|Mover linhas selecionadas para cima| **Alt+Up Arrow** | Edit.MoveSelectedLinesUp |
|Próxima referência realçada| **Ctrl+Shift+Seta para Baixo** | Edit.NextHighlightedReference |
|Modo sobrescrever| **Inserção** | Edit.OvertypeMode |
|Page Down| **PgDn** | Edit.PageDown |
|Estender página abaixo| **Shift+PgDn** | Edit.PageDownExtend |
|Uma página acima| **PgUp** | Edit.PageUp |
|Estender até a página acima| **Shift+PgUp** | Edit.PageUpExtend |
|Informações do parâmetro| **Ctrl+Shift+Barra de espaços** | Edit.ParameterInfo |
|Colar dica de parâmetro| **CTRL + SHIFT + ALT + P** | Edit.PasteParameterTip |
|Retroceder inspeção| **CTRL + ALT +-** | Edit.PeekBackward |
|Inspecionar definição| **Alt+F12** | Edit.PeekDefinition |
|Avançar inspeção| **CTRL + ALT + =** | Edit.PeekForward |
|Referência realçada anterior| **Ctrl+Shift+Seta para Cima** | Edit.PreviousHighlightedReference |
|Informações rápidas| **CTRL + K, Ctrl + I** | Edit.QuickInfo |
|Pesquisa incremental reversa| **Ctrl + Shift + I** | Edit.ReverseIncrementalSearch |
|Rolar linha para baixo| **CTRL + seta para baixo** | Edit.ScrollLineDown |
|Rolar linha para cima| **CTRL + seta para cima** | Edit.ScrollLineUp |
|Selecionar palavra atual| **CTRL + W** | Edit.SelectCurrentWord |
|Cancelar seleção| **Escape** | Edit.SelectionCancel |
|Selecionar até o último voltar| **CTRL + =** | Edit.SelectToLastGoBack |
|Mostrar menu de lentes de código| **CTRL + K, CTRL +\`** | Edit.ShowCodeLensMenu |
|Mostrar menu de navegação| **Alt +\`** | Edit.ShowNavigateMenu |
|Parar de ocultar atual| **Ctrl+M, Ctrl+U** | Edit.StopHidingCurrent |
|Interromper o delineamento| **Ctrl+M, Ctrl+P** | Edit.StopOutlining |
|Trocar âncora| **Ctrl+K, Ctrl+A** | Edit.SwapAnchor |
|Guia à esquerda| **Shift+Tab** | Edit.TabLeft |
|Alternar toda a delineamento| **Ctrl+M, Ctrl+L** | Edit.ToggleAllOutlining |
|Ativar/desativar indicador| **Ctrl+K, Ctrl+K** | Edit.ToggleBookmark |
|Alternar o modo de conclusão| **Ctrl+Alt+Space** | Edit.ToggleCompletionMode |
|Alternar a expansão de delineamento| **Ctrl+M, Ctrl+M** | Edit.ToggleOutliningExpansion |
|Atalho de lista de tarefas de alternância| **Ctrl+K, Ctrl+H** | Edit.ToggleTaskListShortcut |
|Alternar quebra de palavra| **Ctrl+E, Ctrl+W** | Edit.ToggleWordWrap |
|Seleção de não comentários| **Ctrl+K, Ctrl+U** | Edit.UncommentSelection |
|Exibir inferior| **Ctrl+PgDn** | Edit.ViewBottom |
|Exibir extensão inferior| **Ctrl+Shift+PgDn** | Edit.ViewBottomExtend |
|Exibir superior| **Ctrl+PgUp** | Edit.ViewTop |
|Exibir extensão superior| **Ctrl+Shift+PgUp** | Edit.ViewTopExtend |
|Exibir espaço em branco| **Ctrl+R, Ctrl+W** | Edit.ViewWhiteSpace |
|Exclusão de palavras até o fim| **Ctrl+Excluir** | Edit.WordDeleteToEnd |
|Exclusão de palavras para iniciar| **Ctrl+Backspace** | Edit.WordDeleteToStart |
|Word next| **Ctrl+Seta para a Direita** | Edit.WordNext |
|Extensão da próxima palavra| **Ctrl+Shift+Seta para a direita** | Edit.WordNextExtend |
|Coluna de extensão seguinte do Word| **Ctrl+Shift+Alt+Seta para a Direita** | Edit.WordNextExtendColumn |
|Palavra anterior| **Ctrl+Seta para a Esquerda** | Edit.WordPrevious |
|Extensão anterior da palavra| **Ctrl+Shift+Seta para a Esquerda** | Edit.WordPreviousExtend |
|Coluna de extensão anterior do Word| **Ctrl+Shift+Alt+Seta para a Esquerda** | Edit.WordPreviousExtendColumn |
|Transposição de palavras| **Ctrl+Shift+T** | Edit.WordTranspose |
|Executar em interativo| **Alt+Enter** | EditorContextMenus.CodeWindow.ExecuteInInteractive |
|Executar linha em interativo| **Alt+'** | EditorContextMenus.CodeWindow.ExecuteLineInInteractive |
|Exibir no inspetor de página| **Ctrl+K, Ctrl+G** | OtherContextMenus.HTMLContext.ViewinPageInspector |
|Anotar movimentação na próxima região do TFS| **Alt+PgDn** | TeamFoundationContextMenus.Annotate.TfsAnnotateMoveNextRegion |
|Anotar a movimentação da região anterior do TFS| **Alt+PgUp** | TeamFoundationContextMenus.Annotate.TfsAnnotateMovePreviousRegion |

### <a name="uml-activity-diagram"></a>Diagrama de atividade UML

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Excluir|**Shift+Del**| Edit.Delete |

### <a name="uml-class-diagram"></a>Diagrama de classe UML

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Excluir do modelo|**Shift+Del**| Edit.DeleteFromModel |

### <a name="uml-component-diagram"></a>Diagrama de componente UML

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Excluir do modelo|**Shift+Del**| Edit.DeleteFromModel |

### <a name="uml-use-case-diagram"></a>Diagrama de casos de uso UML

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Excluir do modelo|**Shift+Del**| Edit.DeleteFromModel |

### <a name="vc-accelerator-editor"></a>Editor de Tecla Aceleradora do VC

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Novo acelerador|**Inserção**| Edit.NewAccelerator |
|Próxima chave digitada|**Ctrl+W**| Edit.NextKeyTyped |

### <a name="vc-dialog-editor"></a>Editor de Caixa de Diálogo do VC

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Mover o controle para baixo|**Seta para baixo**| Edit.MoveControlDown |
|Mover o controle para a esquerda|**Seta para a esquerda**| Edit.MoveControlLeft |
|Mover o controle para a direita|**Seta para a direita**| Edit.MoveControlRight |
|Mover o controle para cima|**Seta para cima**| Edit.MoveControlUp |
|Role a coluna para a esquerda|**Ctrl+Seta para a Esquerda**| Edit.ScrollColumnLeft |
|Role a coluna para a direita|**Ctrl+Seta para a Direita**| Edit.ScrollColumnRight |
|Role a linha para baixo|**Ctrl+Seta para Baixo**| Edit.ScrollLineDown |
|Rolar linha para cima|**Ctrl+Seta para Cima**| Edit.ScrollLineUp |
|Controle de tamanho reduzido|**Shift+Seta para Baixo**| Edit.SizeControlDown |
|Controle de tamanho à esquerda|**Shift+Seta para a Esquerda**| Edit.SizeControlLeft |
|Controle de tamanho à direita|**Shift+Seta para a direita**| Edit.SizeControlRight |
|Controle de tamanho para cima|**Shift+Seta para Cima**| Edit.SizeControlUp |
|Alinhar as inferioridades|**Ctrl+Shift+Seta para Baixo**| Format.AlignBottoms |
|Alinhar centros|**Shift+F9**| Format.AlignCenters |
|Alinhar à esquerda|**Ctrl+Shift+Seta para a Esquerda**| Format.AlignLefts |
|Alinhar intermediários|**F9**| Format.AlignMiddles |
|Alinhar direitos|**Ctrl+Shift+Seta para a direita**| Format.AlignRights |
|Alinhar tops|**Ctrl+Shift+Seta para Cima**| Format.AlignTops |
|Botão inferior|**Ctrl+B**| Format.ButtonBottom |
|Botão direito|**Ctrl+R**| Format.ButtonRight |
|Central horizontal|**Ctrl+Shift+F9**| Format.CenterHorizontal |
|Centro vertical|**Ctrl+F9**| Format.CenterVertical |
|Verificar mnemônicos|**Ctrl+M**| Format.CheckMnemonics |
|Tamanho do conteúdo|**Shift+F7**| Format.SizetoContent |
|Espaço entre|**Alt+Right Arrow**<br /><br /> ou<br /><br /> **Alt+Left Arrow**| Format.SpaceAcross |
|Espaço ino mesmo|**Alt+Up Arrow**<br /><br /> ou<br /><br /> **Alt+Seta para Baixo**| Format.SpaceDown |
|Ordem de tabulação|**Ctrl+D**| Format.TabOrder |
|Caixa de diálogo Teste|**Ctrl+T**| Format.TestDialog |
|Guias de alternância|**Ctrl+G**| Format.ToggleGuides |

### <a name="vc-image-editor"></a>Editor de Imagem do VC

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Ferramenta Airbrush|**Ctrl+A**| Image.AirbrushTool |
|Ferramenta Brush|**Ctrl+B**| Image.BrushTool |
|Copiar e delinear seleção|**Ctrl+Shift+U**| Image.CopyandOutlineSelection |
|Desenhar opaco|**Ctrl+J**| Image.DrawOpaque |
|Ferramenta Elipse|**Alt+P**| Image.EllipseTool |
|Ferramenta Apagar|**Ctrl+Shift+I**| Image.EraseTool |
|Ferramenta de elipse preenchida|**Ctrl+Shift+Alt+P**| Image.FilledEllipseTool |
|Ferramenta de retângulo preenchida|**Ctrl+Shift+Alt+R**| Image.FilledRectangleTool |
|Ferramenta de retângulo arredondado preenchida|**Ctrl+Shift+Alt+W**| Image.FilledRoundedRectangleTool |
|Ferramenta Preencher|**Ctrl+F**| Image.FillTool |
|Inverter horizontalmente|**Ctrl+H**| Image.FlipHorizontal |
|Inverter vertical|**Shift+Alt+H**| Image.FlipVertical |
|Pincel maior|**Ctrl+=**| Image.LargerBrush |
|Ferramenta de linha|**Ctrl+L**| Image.LineTool |
|Ferramenta de ampliação|**Ctrl+M**| Image.MagnificationTool |
|Ampliar|**Ctrl+Shift+M**| Image.Magnify |
|Novo tipo de imagem|**Inserção**| Image.NewImageType |
|Próxima cor|**Ctrl+]**<br /><br /> ou<br /><br /> **Ctrl+Seta para a Direita**| Image.NextColor |
|Próxima cor à direita|**Ctrl+Shift+]**<br /><br /> ou<br /><br /> **Ctrl+Shift+Seta para a direita**| Image.NextRightColor |
|Ferramenta de elipse descrita|**Shift+Alt+P**| Image.OutlinedEllipseTool |
|Ferramenta de retângulo contorçada|**Shift+Alt+R**| Image.OutlinedRectangleTool |
|Ferramenta retângulo arredondado com contorno|**Shift+Alt+W**| Image.OutlinedRoundedRectangleTool |
|Ferramenta de lápis|**Ctrl+I**| Image.PencilTool |
|Cor anterior|**CTRL + [**<br /><br /> ou<br /><br /> **Ctrl+Seta para a Esquerda**| Image.PreviousColor |
|Cor anterior direita|**Ctrl + Shift + [**<br /><br /> ou<br /><br /> **Ctrl+Shift+Seta para a Esquerda**| Image.PreviousRightColor |
|Ferramenta de seleção de retângulo|**Shift+Alt+S**| Image.RectangleSelectionTool |
|Ferramenta retângulo|**Alt + R**| Image.RectangleTool |
|Girar 90 graus|**Ctrl + Shift + H**| Image.Rotate90Degrees |
|Ferramenta retângulo arredondado|**ALT + W**| Image.RoundedRectangleTool |
|Mostrar grade|**Ctrl + Alt + S**| Image.ShowGrid |
|Mostrar grade de blocos|**Ctrl+Shift+Alt+S**| Image.ShowTileGrid |
|Pincel pequeno|**CTRL +.**| Image.SmallBrush |
|Pincel menor|**CTRL +-**| Image.SmallerBrush |
|Ferramenta de texto|**CTRL + T**| Image.TextTool |
|Usar seleção como pincel|**Ctrl+U**| Image.UseSelectionasBrush |
|Ampliar|**Ctrl + Shift +.**<br /><br /> ou<br /><br /> **CTRL + seta para cima**| Image.ZoomIn |
|Reduzir|**Ctrl + Shift +,**<br /><br /> ou<br /><br /> **CTRL + seta para baixo**| Image.ZoomOut |

### <a name="vc-string-editor"></a>Editor de Cadeia de Caracteres do VC

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Nova cadeia de caracteres|**Inserção**| Edit.NewString |

### <a name="view-designer"></a>Designer de Exibição

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Cancelar recuperação de dados|**CTRL + T**| QueryDesigner.CancelRetrievingData |
|Critérios|**Ctrl + 2**| QueryDesigner.Criteria |
|Diagrama|**Ctrl + 1**| QueryDesigner.Diagram |
|Executar SQL|**CTRL + R**| QueryDesigner.ExecuteSQL |
|Ir para linha|**Ctrl+G**| QueryDesigner.GotoRow |
|Modo de junção|**Ctrl + Shift + J**| QueryDesigner.JoinMode |
|Resultados|**CTRL + 4**| QueryDesigner.Results |
|Sql|**CTRL + 3**| QueryDesigner.SQL |

### <a name="visual-studio"></a>Visual Studio

Os atalhos específicos para esse contexto são:


|Comando|Atalho de teclado|ID do comando|
|-|-|-|
|Ocultar Painel de métodos|**Ctrl + 1**| OtherContextMenus.ORDesignerContext.HideMethodsPane |

### <a name="windows-forms-designer"></a>Designer de Formulários do Windows

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Linha de quebra|**Enter**| Edit.BreakLine |
|Char left|**Seta para a esquerda**| Edit.CharLeft |
|Extensão à esquerda do caractere|**Shift+Seta para a Esquerda**| Edit.CharLeftExtend |
|Char right|**Seta para a direita**| Edit.CharRight |
|Estender à direita do caractere|**Shift+Seta para a direita**| Edit.CharRightExtend |
|Fim do documento|**Final**| Edit.DocumentEnd |
|Extensão de fim do documento|**Shift+End**| Edit.DocumentEndExtend |
|Início do documento|**Início**| Edit.DocumentStart |
|Extensão de início do documento|**Shift+Home**| Edit.DocumentStartExtend |
|Guia Inserir|**Tab**| Edit.InsertTab |
|Uma linha abaixo|**Seta para baixo**| Edit.LineDown |
|Extensão de linha para baixo|**Shift+Seta para Cima**| Edit.LineDownExtend |
|Uma linha acima|**Seta para cima**| Edit.LineUp |
|Extensão de linha|**Shift+Seta para Baixo**| Edit.LineUpExtend |
|Mover o controle para baixo|**Ctrl+Seta para Baixo**| Edit.MoveControlDown |
|Mover o controle para a esquerda|**Ctrl+Seta para a Esquerda**| Edit.MoveControlLeft |
|Mover o controle para a direita|**Ctrl+Seta para a Direita**| Edit.MoveControlRight |
|Mover o controle para cima|**Ctrl+Seta para Cima**| Edit.MoveControlUp |
|Cancelamento da seleção|**Escape**| Edit.SelectionCancel |
|Controle de tamanho reduzido|**Ctrl+Shift+Seta para Baixo**| Edit.SizeControlDown |
|Controle de tamanho à esquerda|**Ctrl+Shift+Seta para a Esquerda**| Edit.SizeControlLeft |
|Controle de tamanho à direita|**Ctrl+Shift+Seta para a direita**| Edit.SizeControlRight |
|Controle de tamanho para cima|**Ctrl+Shift+Seta para Cima**| Edit.SizeControlUp |
|Guia à esquerda|**Shift+Tab**| Edit.TabLeft |

### <a name="work-item-editor"></a>Editor de Itens de Trabalho

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Criar cópia do item de trabalho|**Shift+Alt+C**| Edit.CreateCopyofWorkItem |
|Atualizar item de trabalho|**F5**| Edit.RefreshWorkItem |
|Novo item de trabalho vinculado|**Shift+Alt+L**| Team.NewLinkedWorkItem |

### <a name="work-item-query-view"></a>Exibição de Consulta de Item de Trabalho

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Criar cópia do item de trabalho|**Shift+Alt+C**| Edit.CreateCopyofWorkItem |
|Recuar|**Shift+Alt+Seta para a Direita**| Edit.Indent |
|Recuo|**Shift+Alt+Seta para a Esquerda**| Edit.Outdent |
|Novo item de trabalho vinculado|**Shift+Alt+L**| Team.NewLinkedWorkItem |
|Atualizar|**F5**| Team.Refresh |
|Alternar|**Shift+Alt+V**| Window.Toggle |

### <a name="work-item-results-view"></a>Exibição de Resultados de Item de Trabalho

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Criar cópia do item de trabalho|**Shift+Alt+C**| Edit.CreateCopyofWorkItem |
|Recuar|**Shift+Alt+Seta para a Direita**| Edit.Indent |
|Recuo|**Shift+Alt+Seta para a Esquerda**| Edit.Outdent |
|Próximo item de trabalho do Goto|**Shift+Alt+N**| Team.GotoNextWorkItem |
|Item de trabalho anterior do Goto|**Shift+Alt+P**| Team.GotoPreviousWorkItem |
|Novo item de trabalho vinculado|**Shift+Alt+L**| Team.NewLinkedWorkItem |
|Atualizar|**F5**| Team.Refresh |
|Alternar|**Shift+Alt+V**| Window.Toggle |

### <a name="workflow-designer"></a>Designer de Fluxo de Trabalho

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Completar a palavra|**Ctrl+K, W**<br /><br /> ou<br /><br /> **Ctrl+K, Ctrl+W**<br /><br /> ou<br /><br /> **Ctrl+Barra de Espaços**<br /><br /> ou<br /><br /> **Alt+Right Arrow**| Edit.CompleteWord |
|Diminuir o nível de filtro|**Alt+,**| Edit.DecreaseFilterLevel |
|Aumentar o nível de filtro|**Alt+.**| Edit.IncreaseFilterLevel |
|Listar os membros|**Ctrl+K, L**<br /><br /> ou<br /><br /> **Ctrl+K, Ctrl+L**<br /><br /> ou<br /><br /> **Ctrl+J**| Edit.ListMembers |
|Informações de parâmetro|**Ctrl+K, P**<br /><br /> ou<br /><br /> **Ctrl+K, Ctrl+P**<br /><br /> ou<br /><br /> **Ctrl+Shift+Barra de espaços**| Edit.ParameterInfo |
|Informações rápidas|**Ctrl+K, I**<br /><br /> ou<br /><br /> **Ctrl+K, Ctrl+I**| Edit.QuickInfo |
|Recolher|**Ctrl+E, Ctrl+C**<br /><br /> ou<br /><br /> **Ctrl+E, C**| WorkflowDesigner.Collapse |
|Recolher tudo|ou| WorkflowDesigner.CollapseAll |
|Conexão nós|**Ctrl+E, Ctrl+F**<br /><br /> ou<br /><br /> **Ctrl+E, F**| WorkflowDesigner.ConnectNodes |
|Criar variável|**Ctrl+E, Ctrl+N**<br /><br /> ou<br /><br /> **Ctrl+E, N**| WorkflowDesigner.CreateVariable |
|Expandir tudo|**Ctrl+E, Ctrl+X**<br /><br /> ou<br /><br /> **Ctrl+E, X**| WorkflowDesigner.ExpandAll |
|Expandir no local|**Ctrl+E, Ctrl+E**<br /><br /> ou<br /><br /> **Ctrl+E, E**| WorkflowDesigner.ExpandInPlace |
|Ir para o pai|**Ctrl+E, Ctrl+P**<br /><br /> ou<br /><br /> **Ctrl+E, P**| WorkflowDesigner.GoToParent |
|Mover foco|**Ctrl+E, Ctrl+M**<br /><br /> ou<br /><br /> **CTRL + E, M**| WorkflowDesigner.MoveFocus |
|Navegar pelo designer|**Ctrl+Alt+F6**| WorkflowDesigner.NavigateThroughDesigner |
|Restaurar|**Ctrl+E, Ctrl+R**<br /><br /> ou<br /><br /> **Ctrl+E, R**| WorkflowDesigner.Restore |
|Mostrar designer de argumento de ocultar|**Ctrl+E, Ctrl+A**<br /><br /> ou<br /><br /> **Ctrl+E, A**| WorkflowDesigner.ShowHideArgumentDesigner |
|Mostrar ocultar designer de importações|**Ctrl+E, Ctrl+I**<br /><br /> ou<br /><br /> **Ctrl+E, I**| WorkflowDesigner.ShowHideImportsDesigner |
|Mostrar mapa de visão geral ocultar|**Ctrl+E, Ctrl+O** (letra "O")<br /><br /> ou<br /><br /> **Ctrl+E, O**| WorkflowDesigner.ShowHideOverviewMap |
|Mostrar designer de variável de ocultar|**Ctrl+E, Ctrl+V**<br /><br /> ou<br /><br /> **Ctrl+E, V**| WorkflowDesigner.ShowHideVariableDesigner |
|Alternar seleção|**Ctrl+E, Ctrl+S**<br /><br /> ou<br /><br /> **Ctrl+E, S**| WorkflowDesigner.ToggleSelection |
|Ampliar|**Ctrl+Num +**| WorkflowDesigner.ZoomIn |
|Reduzir|**CTRL + num-**| WorkflowDesigner.ZoomOut |

### <a name="xaml-ui-designer"></a>XAML Designer

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Ajustar tudo|**Ctrl + 0** (zero)| Design.FitAll |
|Mostrar identificadores|**F9**| Design.ShowHandles |
|Ampliar|**CTRL + ALT + =**| Design.ZoomIn |
|Reduzir|**CTRL + ALT +-**| Design.ZoomOut |
|Opções do designer|**Ctrl + Shift +;**|
|Editar texto|**F2**| Format.EditText |
|Tudo|**CTRL + SHIFT + R**| Format.ResetLayout.All |
|Executar código do projeto|**CTRL + F9**|
|Ocultar (somente Blend)|**CTRL + H**| Timeline.Hide (apenas Blend) |
|Bloqueio (somente Blend)|**CTRL + L**| Timeline.Lock (apenas Blend) |
|Mostrar (somente Blend)|**Ctrl + Shift + H**| Timeline.Show (apenas Blend) |
|Desbloquear (somente Blend)|**Ctrl+Shift+L**| Timeline.Unlock (apenas Blend) |
|Mover borda para a esquerda esquerda|**Ctrl+Shift+,**| View.EdgeLeftMoveLeft |
|Mover para a esquerda da borda para a direita|**Ctrl+Shift+.**| View.EdgeLeftMoveRight |
|Mover para a direita da borda para a esquerda|**Ctrl+Shift+Alt+,**| View.EdgeRightMoveLeft |
|Mover para a direita da borda para a direita|**Ctrl+Shift+Alt+.**| View.EdgeRightMoveRight |
|Menu Mostrar marcador de propriedade|**Ctrl+Barra de Espaços**| View.ShowPropertyMarkerMenu |

### <a name="xml-text-editor"></a>Editor XML (Texto)

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|Iniciar a depuração de XSLT|**Alt+F5**| XML.StartXSLTDebugging |
|Iniciar XSLT sem depuração|**Ctrl+Alt+F5**| XML.StartXSLTWithoutDebugging |

### <a name="xml-schema-designer"></a>Designer de Esquema XML

Os atalhos específicos para esse contexto são:


|Comandos|Atalhos de teclado|ID do comando|
|-|-|-|
|De baixo para cima|**Alt+Up Arrow**| GraphView.BottomtoTop |
|Da esquerda para a direita|**Alt+Right Arrow**| GraphView.LefttoRight |
|Da direita para a esquerda|**Alt+Left Arrow**| GraphView.RighttoLeft |
|De cima para baixo|**Alt+Seta para Baixo**| GraphView.ToptoBottom |
|Remover do workspace|**Excluir**| OtherContextMenus.GraphView.RemovefromWorkspace |
|Mostrar exibição do modelo de conteúdo|**Ctrl+2**| XsdDesigner.ShowContentModelView |
|Mostrar exibição de grafo|**Ctrl+3**| XsdDesigner.ShowGraphView |
|Mostrar exibição inicial|**Ctrl+1**| XsdDesigner.ShowStartView |

## <a name="see-also"></a>Consulte também

- [Comandos do Visual Studio](reference/visual-studio-commands.md)
