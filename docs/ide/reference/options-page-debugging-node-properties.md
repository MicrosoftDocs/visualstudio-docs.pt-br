---
title: Página de Opções, Depuração, Propriedades do Nó
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 564cc8b2-0084-420e-b560-200cc5621a7e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 70a06548dd25ade1bf64bad6a99261e043f6ac65
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670826"
---
# <a name="options-page-debugging-node-properties"></a>Página de Opções, Depuração, Propriedades do Nó
As tabelas a seguir descrevem as páginas (ou as coleções de propriedades) associadas à categoria **Depuração**, `DTE.Properties("Debugging", <Property Page>)` da caixa de diálogo **Opções**.

## <a name="general"></a>Geral
 `DTE.Properties("Debugging", "General")`

|Nome do item de propriedade|Valor|Descrição|
| - |-----------|-----------------|
|PromptOnBreakpointDelete|Get/Set (Booliano)|Determina se o depurador solicitará permissão antes de excluir todos os pontos de interrupção de um projeto.|
|BreakAllProcesses|Get/Set (Booliano)|Determina se o depurador interromperá todos os processos sempre que um único processo for interrompido.|
|BreakAtBoundaries|Get/Set (Booliano)|Determina se o depurador interromperá a execução quando uma exceção exceder um limite entre AppDomains ou entre o código nativo e gerenciado.|
|EnableAddressLevelDebugging|Get/Set (Booliano)|Determina se os recursos de depuração do nível do endereço são habilitados.|
|ShowDisassemblyIfNoSource|Get/Set (Booliano)|Determina se o depurador exibe o código de desmontagem quando o código-fonte não está disponível.|
|EnableBreakpointFilters|Get/Set (Booliano)|Determina se a filtragem do ponto de interrupção é habilitada.|
|EnableExceptionAssistant|Get/Set (Booliano)|Determina se o Assistente de Exceção é usado para exceções gerenciadas.|
|UnwindCallstack|Get/Set (Booliano)|Determina se o depurador desenrola a pilha de chamadas de uma exceção sem tratamento.|
|EnableJustMyCode|Get/Set (Booliano)|Determina se o Apenas Meu Código está habilitado para o código C# e Visual Basic.|
|ShowAllMembers|Get/Set (Booliano)|Para objetos que não são de usuário, determina se o depurador exibe todos os membros de objeto nas janelas de variáveis. Essa opção só terá efeito se Apenas Meu Código estiver habilitado.|
|WarnIfNoUserCode|Get/Set (Booliano)|Determina se o depurador emite um aviso quando o usuário tenta se anexar a um processo que não tem nenhum código de usuário. Essa opção só terá efeito se Apenas Meu Código estiver habilitado.|
|EnablePropertyEvaluation|Get/Set (Booliano)|Determina se o depurador avalia automaticamente as propriedades e as chamadas de função implícitas no código gerenciado.|
|CallStringConversion|Get/Set (Booliano)|Determina se o depurador chama implicitamente uma função de conversão de cadeia de caracteres em objetos nas janelas de variáveis.|
|EnableSourceServer|Get/Set (Booliano)|Determina se o depurador pode acessar o código em um servidor de origem.|
|PrintSourceServerDiagnostics|Get/Set (Booliano)|Determina se a Janela de Saída mostra mensagens de diagnóstico relacionadas ao servidor de origem. Essa opção só terá efeito se o acesso ao servidor de origem estiver habilitado.|
|HighlightEntireLine|Get/Set (Booliano)|Determina se o depurador realça uma linha inteira de pontos de interrupção e a instrução atual.|
|RequireSourceToMatch|Get/Set (Booliano)|Determina se o depurador exige que os arquivos de origem correspondam exatamente à versão original ao abrir arquivos para depuração.|
|RedirectOutputToImmediate|Get/Set (Booliano)|Determina se a saída da Janela de Saída é redirecionada para a Janela Imediata.|
|ShowRawVariableStructure|Get/Set (Booliano)|Determina se os objetos nas janelas de variáveis são mostrados no formato bruto.|
|SuppressJitOptimization|Get/Set (Booliano)|Para o código gerenciado, determina se a otimização Just-In-Time é suprimida pelo depurador.|
|WarnIfNoSymbols|Get/Set (Booliano)|Determina se o depurador exibirá um aviso se não houver símbolos de depuração disponíveis quando um processo é iniciado.|
|WarnIfScriptDisabled|Get/Set (Booliano)|Determina se o depurador exibirá um aviso se a depuração de script não estiver habilitada quando um processo é iniciado.|
|ShowMarkersForAllThreads|Get/Set (Booliano)|Determina se o depurador exibe marcadores de thread.|
|StepOverPropertiesAndOperators|Get/Set (Booliano)|Especifica se as propriedades e os operadores são depurados parcialmente somente no código gerenciado.|

## <a name="edit-and-continue"></a>Editar e continuar
 `DTE.Properties("Debugging", "EditAndContinue")`

|Nome do item de propriedade|Valor|Descrição|
| - |-----------|-----------------|
|EnableEditAndContinue|Get/Set (Booliano)|Determina se a opção Editar e Continuar está habilitada. Essa opção se aplica a todas as linguagens que dão suporte à opção Editar e Continuar.|
|InvokedByCommands|Get/Set (Booliano)|Determina se a opção Editar e Continuar aplica as alterações de código automaticamente quando o usuário seleciona um comando de depuração como **Executar em Etapas** ou **Continuar**. Essa opção se aplica apenas ao código nativo.|
|InvokedByCommandsAskFirst|Get/Set (Booliano)|Determina se a opção Editar e Continuar solicita ao usuário permissão para aplicar alterações de código quando o usuário seleciona um comando de depuração como **Executar em Etapas** ou **Continuar**. Essa opção se aplica apenas ao código nativo.|
|WarnAboutStaleCode|Get/Set (Booliano)|Determina se o depurador emite uma mensagem de aviso quando a opção Editar e Continuar resulta na execução de um código desatualizado ou obsoleto. Essa opção se aplica apenas ao código nativo.|
|RelinkChangesOnStop|Get/Set (Curto)|Determina se o Visual Studio vincula novamente as alterações de código aplicadas pela opção Editar e Continuar quando a execução do aplicativo é interrompida. Essa opção se aplica apenas ao código nativo.|
|AllowPrecompiling|Get/Set (Curto)|Determina se a opção Editar e Continuar tem permissão para carregar cabeçalhos pré-compilados na tela de fundo. Essa opção se aplica apenas ao código nativo.|

## <a name="just-in-time"></a>Just-In-Time
 `DTE.Properties("Debugging", "JustInTime")`

|Nome do item de propriedade|Valor|Descrição|
| - |-----------|-----------------|
|JitManaged|Get/Set (Booliano)|Determina se a depuração Just-In-Time está habilitada para o código gerenciado.|
|JitNative|Get/Set (Booliano)|Determina se a depuração Just-In-Time está habilitada para o código nativo.|
|JitScript|Get/Set (Booliano)|Determina se a depuração Just-In-Time está habilitada para o código de script.|

## <a name="native"></a>Nativo
 `DTE.Properties("Debugging", "Native")`

|Nome do item de propriedade|Valor|Descrição|
| - |-----------|-----------------|
|LoadDllExports|Get/Set (Booliano)|Determina se o depurador carrega as tabelas de exportação de DLL.|
|EnableRPC|Get/Set (Booliano)|Determina se o depurador pode intervir em chamadas COM de procedimento remoto.|

## <a name="see-also"></a>Consulte também

- [Controlando as configurações de opções](https://msdn.microsoft.com/Library/a09ed242-7494-4cde-bbd1-7a8ec617965d)
- [Determinando os nomes dos itens de propriedade nas páginas de opções](https://msdn.microsoft.com/Library/d450422d-47c7-4eeb-9f9f-3286264bc5aa)
- [Página de Opções, Propriedades do Nó de Fontes e Cores](../../ide/reference/options-page-fonts-and-colors-node-properties.md)
- [Página de Opções, Propriedades do Nó de Editor de Texto](../../ide/reference/options-page-text-editor-node-properties.md)
- [Caixa de diálogo Geral, Depuração, Opções](../../debugger/general-debugging-options-dialog-box.md)
- [Caixa de diálogo Editar e Continuar, Depuração, Opções](/visualstudio/debugger/edit-and-continue?view=vs-2015)
- [Caixa de diálogo Just-In-Time, Depuração, Opções](../../debugger/just-in-time-debugging-options-dialog-box.md)