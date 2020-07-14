---
title: Caixa de diálogo geral, depuração, opções | Microsoft Docs
ms.date: 06/04/2020
ms.topic: reference
f1_keywords:
- vs.debug.options.General
- VS.ToolsOptionsPages.Debugger.General
- VS.ToolsOptionsPages.Debugger.ENC
- vs.debug.options.ENC
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Options dialog box, debugging
ms.assetid: b33aee0b-43c3-4c26-8ed4-bc673f491503
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c5b03d7b45e488d7e8026a7d6835bbfba1efa210
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286551"
---
# <a name="general-debugging-options"></a>Opções gerais de depuração

Para definir opções do depurador do Visual Studio, selecione opções de **ferramentas**  >  **Options**e, em **depuração** , marque ou desmarque as caixas ao lado das opções **gerais** . Você pode restaurar todas as configurações padrão com **ferramentas**  >  **importar e exportar configurações**  >  **redefinir todas as configurações**. Para redefinir um subconjunto de configurações, salve suas configurações com o **Assistente de importação e exportação de configurações** antes de fazer as alterações que você deseja testar e, em seguida, importe as configurações salvas posteriormente.

Você pode definir as seguintes opções **gerais** :

**Perguntar antes de excluir todos os pontos de interrupção**: requer confirmação antes de concluir o comando **excluir todos os pontos de interrupção** .

**Interromper todos os processos quando um processo for interrompido**: interrompe simultaneamente todos os processos aos quais o depurador está anexado, quando ocorre uma interrupção.

**Quebra quando as exceções cruzam os limites de AppDomain ou gerenciado/nativo**: em depuração de modo misto ou gerenciado, o Common Language Runtime pode capturar exceções que cruzam limites de domínio de aplicativo ou limites nativos/gerenciados quando as seguintes condições são verdadeiras:

1. Quando o código nativo chama o código gerenciado usando a interoperabilidade COM e o código gerenciado aciona uma exceção. Consulte [introdução à interoperabilidade com](/dotnet/articles/visual-basic/programming-guide/com-interop/introduction-to-com-interop).

2. Quando o código gerenciado executado no domínio do aplicativo 1 chama o código gerenciado no domínio 2 do aplicativo, e o código no aplicativo domínio 2 gera uma exceção. Consulte [programação com domínios de aplicativo](/dotnet/articles/framework/app-domains/index).

3. Quando o código chama uma função usando reflexão, e essa função gera uma exceção. Consulte [reflexão](/dotnet/framework/reflection-and-codedom/reflection).

Nas condições 2 e 3, às vezes, a exceção é capturada pelo código gerenciado em `mscorlib` vez de pelo Common Language Runtime. Esta opção não afeta a quebra em exceções capturadas por `mscorlib`.

**Habilitar depuração no nível de endereço**: habilita recursos avançados para depuração no nível de endereço (a janela de **desmontagem** , a janela de **registros** e pontos de interrupção de endereço).

- **Mostrar desmontagem se a origem não estiver disponível**: mostra automaticamente a janela de **desmontagem** quando você depura o código para o qual a origem está indisponível.

**Habilitar filtros de ponto de interrupção**: permite que você defina filtros em pontos de interrupção para que afetem apenas processos, threads ou computadores específicos.

**Usar o novo auxiliar de exceção**: habilita o auxiliar de exceção que substitui o assistente de exceção. (O auxiliar de exceção tem suporte a partir do Visual Studio 2017)

> [!NOTE]
> Para código gerenciado, essa opção anteriormente era chamada **habilitar o assistente de exceção** .

**Habilitar apenas meu código**: o depurador exibe e percorre as etapas do código do usuário ("meu código") apenas, ignorando o código do sistema e outro código que é otimizado ou que não tem símbolos de depuração.

- **Avisar se não houver código de usuário na inicialização (somente gerenciado)**: quando a depuração começar com apenas meu código habilitado, essa opção avisará se não houver código de usuário ("meu código").

**Habilitar .NET Framework a depuração de origem**: permite que o depurador entre .NET Framework fonte. Habilitar essa opção desabilita automaticamente Apenas Meu Código. .NET Framework símbolos serão baixados em um local de cache. Altere o local do cache com a caixa de diálogo **Opções** , categoria **depuração** , página **símbolos** .

**Percorrer Propriedades e operadores (somente gerenciado)**: impede que o depurador percorra em Propriedades e operadores em código gerenciado.

**Habilitar a avaliação de propriedade e outras chamadas de função implícitas**: ativa a avaliação automática de propriedades e chamadas de função implícitas em janelas de variáveis e na caixa de diálogo **QuickWatch** .

- **Chamar função de conversão de cadeia de caracteres em objetos em janelas de variáveis (somente C# e JavaScript)**: executa uma chamada de conversão de cadeia de caracteres implícita ao avaliar objetos em janelas de variáveis. O resultado é exibido como uma cadeia de caracteres em vez do nome do tipo. Aplica-se somente à depuração no código em C. Essa configuração pode ser substituída pelo atributo DebuggerDisplay (consulte [usando o atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md)).

**Habilitar o suporte ao servidor de origem**: informa ao depurador do Visual Studio para obter arquivos de origem de servidores de origem que implementam o protocolo SrcSrv ( `srcsrv.dll` ). O Team Foundation Server e as Ferramentas de Depuração para o Windows são dois servidores de origem que implementam o protocolo. Para obter mais informações sobre a configuração do SrcSrv, consulte a documentação do [srcsrv](/windows-hardware/drivers/debugger/srcsrv) . Além disso, consulte [especificar símbolo (. pdb) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

> [!IMPORTANT]
> Como a leitura de arquivos *. pdb* pode executar código arbitrário nos arquivos, certifique-se de confiar no servidor.

- **Imprimir mensagens de diagnóstico do servidor de origem na janela de saída**: quando o suporte ao servidor de origem está habilitado, essa configuração ativa a exibição de diagnóstico.

- **Permitir servidor de origem para assemblies de confiança parcial (somente gerenciado)**: quando o suporte ao servidor de origem está habilitado, essa configuração substitui o comportamento padrão de não recuperar fontes para assemblies de confiança parcial.

- **Sempre executar comandos de servidor de origem não confiáveis sem avisar**: quando o suporte ao servidor de origem está habilitado, essa configuração substitui o comportamento padrão de solicitação ao executar um comando não confiável.

**Habilitar suporte ao link de origem**: informa o depurador do Visual Studio para baixar arquivos de origem para arquivos *. pdb* que contêm informações de link de origem. Para obter mais informações sobre o link de origem, consulte a [especificação do link de origem](/dotnet/standard/library-guidance/sourcelink).

> [!IMPORTANT]
> Como o link de origem baixará arquivos usando http ou HTTPS, certifique-se de confiar no arquivo *. pdb* .

- **Volte para a autenticação do git Credential Manager para todas as solicitações de link de origem**: quando o suporte ao link de origem está habilitado e uma solicitação de link de origem falha na autenticação, o Visual Studio chama o Git Credential Manager.

**Realçar toda a linha de origem para pontos de interrupção e a instrução atual (somente C++)**: quando o depurador realça um ponto de interrupção ou uma instrução atual, ele realça a linha inteira.

**Exigir que os arquivos de origem correspondam exatamente à versão original**: diz ao depurador para verificar se um arquivo de origem corresponde à versão do código-fonte usado para criar o executável que você está depurando. Quando a versão não corresponder, você será solicitado a localizar uma fonte correspondente. Se uma fonte compatível não for encontrada, o código-fonte não será exibido durante a depuração.

**Redirecionar todo o texto da janela de saída para a janela imediata**: envia todas as mensagens do depurador que normalmente apareceriam na janela de **saída** para a janela **imediata** .

**Mostrar estrutura bruta de objetos em janelas de variáveis**: desativa todas as personalizações de exibição de estrutura de objeto. Para obter mais informações sobre as personalizações de exibição, consulte [criar exibições personalizadas de objetos gerenciados](../debugger/create-custom-views-of-managed-objects.md).

**Suprimir a otimização JIT na carga do módulo (somente gerenciado)**: desabilita a otimização JIT do código gerenciado quando um módulo é carregado e JIT é compilado enquanto o depurador é anexado. Desativar a otimização pode facilitar a depuração de alguns problemas, embora às custas de desempenho. Se você estiver usando Apenas Meu Código, a supressão da otimização de JIT poderá fazer com que código que não seja do usuário apareça como código do usuário ("Meu Código"). Para obter mais informações, consulte [otimização e depuração JIT](../debugger/jit-optimization-and-debugging.md).

**Habilitar depuração de JavaScript para ASP.net (Chrome, Microsoft Edge e IE)**: habilita o depurador de script para aplicativos ASP.net. Na primeira utilização no Chrome, talvez seja necessário entrar no navegador para habilitar as extensões do Chrome que você instalou. Desabilite esta opção para reverter para o comportamento herdado.

::: moniker range=">= vs-2019"
**Habilitar o uso do depurador de JavaScript multidirecional para Depurar JavaScript em destinos aplicáveis (requer depuração de reinicialização)** Habilita a conexão ao navegador e ao back-end simultaneamente, permitindo que você depure seu código em execução no cliente e no servidor diretamente do editor.
::: moniker-end

**Carregar exportações de dll (somente nativo)**: carrega tabelas de exportação de dll. Informações de símbolos das tabelas de exportação de dll podem ser úteis se você estiver trabalhando com mensagens do Windows, procedimentos do Windows (WindowProcs), objetos COM, ou marshaling, ou qualquer dll para a qual você não tem símbolos. A leitura das informações de exportação de dll gera certa sobrecarga. Desse modo, esse recurso é desativado por padrão.

Para ver quais símbolos estão disponíveis na tabela de exportação de uma dll, use `dumpbin /exports`. Os símbolos estão disponíveis para qualquer dll de 32 bits do sistema. Ao ler a saída `dumpbin /exports`, você pode ver o nome exato da função, incluindo caracteres não alfanuméricos. Isso é útil para definir um ponto de interrupção em uma função. Os nomes de função de tabelas de exportação de dll podem aparecer truncados em qualquer outro lugar no depurador. As chamadas são listadas na ordem de chamada, com a função atual (a mais profundamente aninhada) na parte superior. Para obter mais informações, confira [dumpbin /exports](/cpp/build/reference/dash-exports).

**Mostrar diagrama de pilhas paralelas de baixo para cima**: controla a direção em que as pilhas são exibidas na janela **pilhas paralelas** .

**Ignorar exceções de acesso à memória GPU se os dados gravados não alteraram o valor**: ignora as condições de corrida detectadas durante a depuração se os dados não foram alterados. Para obter mais informações, consulte [depuração de código de GPU](../debugger/debugging-gpu-code.md).

**Usar modo de compatibilidade gerenciado**: substitui o mecanismo de depuração padrão por uma versão herdada para habilitar estes cenários:

- Você está usando uma linguagem .NET diferente de C#, Visual Basic ou F # que fornece seu próprio avaliador de expressão (isso inclui C++/CLI).

- Você deseja habilitar editar e continuar para projetos C++ durante a depuração de modo misto.

> [!NOTE]
> A escolha do modo de compatibilidade gerenciado desabilita alguns recursos que são implementados somente no mecanismo de depuração padrão. O mecanismo de depuração herdado foi substituído no Visual Studio 2012.

::: moniker range="vs-2017"
**Use os avaliadores de expressão c# e VB herdados**: o depurador usará o Visual Studio 2013 os avaliadores de expressão c# ou Visual Basic em vez dos avaliadores de expressão baseados em Roslyn do Visual Studio 2015.
::: moniker-end

**Avisar ao usar visualizadores de depurador personalizados contra processos potencialmente não seguros (somente gerenciados)**: o Visual Studio avisa quando você está usando um visualizador de depurador personalizado que está executando código no processo depurado, pois ele poderia estar executando código não seguro.

**Habilitar o alocador de heap de depuração do Windows (somente nativo)**: habilita o heap de depuração do Windows para melhorar o diagnóstico de heap. Habilitar essa opção afetará o desempenho da depuração.

**Habilitar ferramentas de depuração de interface do usuário para XAML**: a árvore visual ao vivo e a propriedade ao vivo explorando o Windows aparecerão quando você iniciar a depuração (**F5**) de um tipo de projeto com suporte. Para obter mais informações, consulte [inspecionar propriedades XAML durante a depuração](../xaml-tools/inspect-xaml-properties-while-debugging.md).

- **Visualizar elementos selecionados na árvore visual dinâmica**: o elemento XAML cujo contexto está selecionado também é selecionado na janela da **árvore visual ao vivo** .

- **Mostrar ferramentas de tempo de execução no aplicativo**: mostra os comandos de **árvore visual ao vivo** em uma barra de ferramentas na janela principal do aplicativo XAML que está sendo depurado. Essa opção foi introduzida no Visual Studio 2015 atualização 2.

- **Habilitar o recarregamento de XAML**: permite que você use o recurso de recarregamento ativo em XAML com código XAML quando seu aplicativo está em execução. (Anteriormente, esse recurso era chamado de "edição XAML e continuação")

::: moniker range=">= vs-2019" 
- **Habilitar apenas meu XAML**: a partir do Visual Studio 2019 versão 16,4, a **árvore visual ativa** , por padrão, mostra apenas o XAML que é classificado como código de usuário. Se você desabilitar essa opção, todo o código XAML gerado será mostrado na ferramenta.

- Desligar **o modo de seleção quando um elemento é selecionado** A partir do Visual Studio 2019 versão 16,4, o botão seletor do elemento da barra de ferramentas no aplicativo (**habilitar seleção**) é desativado quando um elemento é selecionado. Se você desabilitar essa opção, a seleção de elementos permanecerá ativada até você clicar no botão da barra de ferramentas no aplicativo novamente.

- **Aplicar o Hot recarregamento de XAML ao salvar documento** A partir do Visual Studio 2019 versão 16,6, o aplica o Hot recarregamento de XAML quando você salva o documento.

::: moniker-end

**Habilitar ferramentas de diagnóstico durante a depuração**: a janela **ferramentas de diagnóstico** aparece enquanto você está depurando.

**Mostrar tempo decorrido dica durante a depuração**: a janela de código exibe o tempo decorrido de uma determinada chamada de método quando você está depurando.

**Habilitar editar e continuar**: habilita a funcionalidade Editar e continuar durante a depuração.

- **Habilitar editar e continuar nativo**: você pode usar a funcionalidade Editar e continuar ao depurar código C++ nativo. Para obter mais informações, consulte [Editar e continuar (C++)](../debugger/edit-and-continue-visual-cpp.md).

- **Aplicar alterações ao continuar (somente nativo)**: o Visual Studio compila automaticamente e aplica todas as alterações de código pendentes feitas ao continuar o processo a partir de um estado de interrupção. Se não estiver selecionado, você poderá optar por aplicar as alterações usando o item **aplicar alterações de código** no menu **depurar** .

- **Avisar sobre código obsoleto (somente nativo)**: obter avisos sobre código obsoleto.

**Mostrar executar para clicar no botão no editor durante a depuração**: quando esta opção for selecionada, o botão [Executar para clicar](../debugger/debugger-feature-tour.md#run-to-a-point-in-your-code-quickly-using-the-mouse) será exibido durante a depuração.

**Fechar automaticamente o console quando a depuração for interrompida**: informa ao Visual Studio para fechar o console no final de uma sessão de depuração.

::: moniker range=">= vs-2019"
**Habilitar a avaliação rápida de expressão (somente gerenciado)**: permite que o depurador tente uma avaliação mais rápida simulando a execução de propriedades e métodos simples.

**Carregar símbolos de depuração no processo externo (somente nativo)** Habilita essa [otimização de memória](https://devblogs.microsoft.com/cppblog/out-of-process-debugger-for-c-in-visual-studio-2019/) durante a depuração.

**Traga o Visual Studio para o primeiro plano ao interromper o depurador** Alterna o Visual Studio para o primeiro plano quando você pausa no depurador.
::: moniker-end

## <a name="options-available-in-older-versions-of-visual-studio"></a>Opções disponíveis em versões mais antigas do Visual Studio

Se você estiver usando uma versão mais antiga do Visual Studio, algumas opções adicionais poderão estar presentes.

**Habilitar ferramentas para desenvolvedores de borda para aplicativos de JavaScript UWP (experimental)**: habilita as ferramentas de desenvolvedor para aplicativos de JavaScript UWP no Microsoft Edge.

**Habilitar depurador de JavaScript do Chrome herdado para ASP.net**: habilita o depurador de script do JavaScript Chrome herdado para aplicativos ASP.net. Na primeira utilização no Chrome, talvez seja necessário entrar no navegador para habilitar as extensões do Chrome que você instalou.

**Habilitar o assistente de exceção**: para código gerenciado, habilita o assistente de exceção. A partir do Visual Studio 2017, o auxiliar de exceção substituiu o assistente de exceção.

**Desenrolar a pilha de chamadas em exceções sem tratamento**: faz com que a janela **pilha de chamadas** reverta a pilha de chamadas até o ponto antes que a exceção sem tratamento ocorra.

**Use uma maneira experimental de iniciar a depuração de JavaScript do Chrome ao executar o Visual Studio como administrador**: diz ao Visual Studio para experimentar uma nova maneira de iniciar o Chrome durante a depuração do JavaScript.

**Avisar se nenhum símbolo for iniciado (somente nativo)**: exibe uma caixa de diálogo de aviso quando você depura um programa para o qual o depurador não tem informações de símbolo.

**Avisar se a depuração de script estiver desabilitada na inicialização**: exibe uma caixa de diálogo de aviso quando o depurador é iniciado com a depuração de script desabilitada.

**Usar o modo de compatibilidade nativa**: quando essa opção é selecionada, o depurador usa o depurador nativo do Visual Studio 2010 em vez do novo depurador nativo.

- Use esta opção quando estiver depurando o código .NET C++, pois o novo mecanismo de depuração não oferece suporte à avaliação de expressões .NET C++. No entanto, habilitar o modo de compatibilidade nativa desabilita muitos recursos que dependem da implementação do depurador atual para operar. Por exemplo, o mecanismo herdado não tem muitos visualizadores para tipos internos, como `std::string` nos projetos do Visual Studio 2015.   Use Visual Studio 2013 projetos para a experiência de depuração ideal nesses casos.

## <a name="see-also"></a>Veja também

- [Depurando no Visual Studio](../debugger/index.yml)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)
