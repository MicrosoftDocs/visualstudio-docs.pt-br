---
title: Geral, depuração, caixa de diálogo de opções | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2018
ms.technology: vs-ide-debug
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4b5711b90e2b160f48c05835ae833bfbe7cd29fe
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730672"
---
# <a name="general-debugging-options"></a>Opções gerais de depuração

Para definir opções de depurador do Visual Studio, selecione **ferramentas** > **opções**e, em **depuração** marque ou desmarque as caixas ao lado de  **Geral** opções. Você pode restaurar todas as configurações padrão com **ferramentas** > **importar e exportar configurações** > **redefinir todas as configurações**. Para redefinir um subconjunto de configurações, salvar suas configurações com o **Import and Export Settings Wizard** antes de fazer as alterações que você deseja testar, em seguida, importar as configurações salvas posteriormente.

Você pode definir o seguinte **geral** opções:

**Perguntar antes de excluir todos os pontos de interrupção**:  
Requer a confirmação antes de concluir a **excluir todos os pontos de interrupção** comando.

**Interromper todos os processos quando um processo for interrompido**:  
Interrompe simultaneamente todos os processos ao qual o depurador é anexado, quando ocorre uma interrupção.

**Interromper quando exceções cruzarem AppDomain ou limites gerenciados/nativos**:  
Na depuração gerenciada ou de modo misto, o common language runtime pode capturar exceções que cruzem limites de domínio de aplicativo ou domínios gerenciados/nativos quando as seguintes condições forem verdadeiras:

1. Quando o código nativo chama código gerenciado usando a interoperabilidade COM e o código gerenciado gera uma exceção. Ver [Introdução à interoperabilidade COM](/dotnet/articles/visual-basic/programming-guide/com-interop/introduction-to-com-interop).

2. Quando o código gerenciado em execução no domínio do aplicativo 1 chama o código gerenciado no domínio do aplicativo 2, e o código no domínio do aplicativo 2 gera uma exceção. Ver [programação com domínios do aplicativo](/dotnet/articles/framework/app-domains/index).

3. Quando o código chama uma função por meio de reflexão, e a função gera uma exceção. Ver [reflexão](/dotnet/framework/reflection-and-codedom/reflection).

Em condições de 2 e 3, a exceção é às vezes detectada pelo código gerenciado em `mscorlib` em vez do common language runtime. Esta opção não afeta a quebra em exceções capturadas por `mscorlib`.

**Habilitar depuração no nível do endereço**:  
Habilita recursos avançados para depuração no nível do endereço (a **desmontagem** janela, o **registra** janela e pontos de interrupção de endereço).

- **Mostrar desmontagem se a fonte não está disponível**:  
    Mostra automaticamente a **desmontagem** janela ao depurar o código para o qual a fonte está indisponível.

**Habilitar filtros de ponto de interrupção**:  
Permite que você defina filtros em pontos de interrupção de modo que eles afetem somente processos, threads ou computadores específicos.

**Use o novo auxiliar de exceção**:  
Permite que o auxiliar de exceção (Visual Studio 2017) que substitui o Assistente de exceção.

> [!NOTE]
> Para código gerenciado, essa opção foi chamada anteriormente **habilitar o Assistente de exceção** .

**Habilitar apenas meu código**:  
O depurador exibe e as etapas no código do usuário ("meu código"), ignorando o código de sistema e outro código que é otimizado ou que não tem símbolos de depuração.

- **Avisar se não houver código de usuário na inicialização (somente gerenciado)**:  
    Quando a depuração começa com o Just My Code ativado, esta opção advertirá você se não houver nenhum código de usuário ("My Code").

**Habilitar o .NET Framework depuração da origem**:  
Permite que o depurador entre na fonte do .NET Framework. Habilitar esta opção desabilita automaticamente apenas meu código. Símbolos do .NET framework serão baixados para um local de cache. Alterar o local do cache com o **opções** caixa de diálogo **depuração** categoria, **símbolos** página.

**Depurar parcialmente propriedades e operadores (somente gerenciado)**:  
Impede que o depurador entre em propriedades e operadores no código gerenciado.

**Habilitar a avaliação de propriedade e outras chamadas de função implícitas**:  
Chama de ativar a avaliação automática de propriedades e de função implícitas nas janelas de variáveis e o **QuickWatch** caixa de diálogo.

- **Chamar a função de conversão de cadeia de caracteres em objetos nas janelas de variáveis (C# e o JavaScript apenas)**:  
    Executa uma chamada de conversão de cadeia de caracteres implícita ao avaliar objetos em janelas de variáveis. O resultado é exibido como uma cadeia de caracteres em vez do nome de tipo. Aplica-se somente à depuração no código em C. Essa configuração pode ser substituída pelo atributo DebuggerDisplay (consulte [usando o atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md)).

**Habilitar o suporte do servidor de origem**:  
Informe ao depurador do Visual Studio para obter os arquivos de origem dos servidores de origem que implementam o protocolo de SrcSrv (`srcsrv.dll`). Team Foundation Server e as ferramentas de depuração para Windows são dois servidores de origem que implementam o protocolo. Para obter mais informações sobre a configuração de SrcSrv, consulte o [SrcSrv](/windows-hardware/drivers/debugger/srcsrv) documentação. Além disso, consulte [especificar arquivos de símbolo (. PDB) e código-fonte](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

> [!IMPORTANT]
> Pois lendo *. PDB* arquivos pode executar código arbitrário em arquivos, certifique-se de que você confia no servidor.

- **Imprimir mensagens de diagnóstico de servidor de origem para a janela de saída**:  
    Quando o suporte do servidor de origem é ativado, esta configuração ativa ao diagnóstico.

- **Permitir que o servidor de origem para os assemblies de confiança parcial (somente gerenciado)**:  
    Quando o suporte do servidor de origem é ativado, esta configuração substitui o comportamento padrão de não recuperar as fontes dos assemblies de confiança parcial.

- **Sempre executar comandos do servidor de origem não confiável, sem avisar**:  
    Quando o suporte do servidor de origem está habilitado, essa configuração substitui o comportamento padrão de solicitação quando executar um comando não confiável.

**Habilitar o suporte a Link de origem**:  
    Informa o depurador do Visual Studio para baixar os arquivos de origem *. PDB* arquivos que contêm informações de Link de origem. Para obter mais informações sobre o Link de origem, consulte a [especificação de link de origem](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/source_link.md).

> [!IMPORTANT]
>  Porque vínculo da fonte será baixar arquivos usando http ou https, verifique se você confia as *. PDB* arquivo.

- **Fazer fallback para autenticação de Git Credential Manager para todas as solicitações de Link de origem**:  
    Quando o suporte de Link de origem está habilitado e uma solicitação de Link de origem falhar na autenticação, o Visual Studio, em seguida, chama o Gerenciador de credenciais do Git.

**Realçar a linha inteira para pontos de interrupção e a instrução atual (C++)**:  
Quando o depurador realça um ponto de interrupção ou uma declaração atual, realça a linha inteira.

**Exigir arquivos de origem correspondam exatamente à versão original**:  
Informe ao depurador para verificar se um arquivo fonte corresponde à versão do código-fonte usado para criar o arquivo executável que você está depurando. Quando a versão não corresponde, você será solicitado para encontrar uma origem correspondente. Se uma fonte compatível não for encontrada, o código-fonte não será exibido durante a depuração.

**Redirecionar todo o texto da janela Saída para a janela imediata**:  
Envia todas as mensagens do depurador que normalmente apareceriam na **saída** janela para o **imediato** janela em vez disso.

**Mostrar estrutura bruta de objetos nas janelas de variáveis**:  
Desative todas as personalizações de exibição da estrutura do objeto. Para obter mais informações sobre personalizações de exibição, consulte [criar exibições personalizadas de objetos gerenciados](../debugger/create-custom-views-of-dot-managed-objects.md).

**Suprimir Otimização JIT no carregamento do módulo (somente gerenciado)**:  
Desativa a otimização JIT de código gerenciado quando um módulo é carregado e JIT é compilado enquanto o depurador é anexado. Desativar a otimização pode facilitar a depuração de alguns problemas, embora às custas de desempenho. Se você estiver usando Apenas Meu Código, a supressão da otimização de JIT poderá fazer com que código que não seja do usuário apareça como código do usuário ("Meu Código"). Para obter mais informações, consulte [JIT otimização e depuração](../debugger/jit-optimization-and-debugging.md).

**Habilitar a depuração de JavaScript para ASP.NET (Chrome, Edge e IE)**:  
Permite que o depurador de script para aplicativos ASP.NET. No primeiro uso no Chrome, você precisa entrar no navegador para habilitar as extensões do Chrome que você instalou. Desabilite essa opção para reverter para o comportamento herdado.

**Habilitar ferramentas de desenvolvedor do Edge para aplicativos JavaScript da UWP (Experimental)**:  
Habilita as ferramentas de desenvolvedor para aplicativos UWP JavaScript no Edge.

**Habilitar depurador JavaScript Chrome herdado para ASP.NET**:  
Permite que o depurador de script JavaScript Chrome herdado para aplicativos ASP.NET. No primeiro uso no Chrome, você precisa entrar no navegador para habilitar as extensões do Chrome que você instalou.

**Usar modo experimental para iniciar a depuração de JavaScript do Chrome, ao executar o Visual Studio como administrador**:  
Informa ao Visual Studio para tentar uma nova maneira de iniciar o Chrome durante a depuração de JavaScript.

**Carregar exportações de dll (somente nativo)**:  
Carrega as tabelas de exportação de dll. Informações de símbolo de tabelas de exportação de dll podem ser útil se você estiver trabalhando com mensagens do Windows, procedimentos do Windows (WindowProcs), objetos COM, ou marshaling ou qualquer dll para o qual você não tem símbolos. Informações de exportação lendo dll envolve alguma sobrecarga. Desse modo, esse recurso é desativado por padrão.

Para ver quais símbolos estão disponíveis na tabela de exportação de uma dll, use `dumpbin /exports`. Símbolos estão disponíveis para qualquer dll do sistema de 32 bits. Ao ler a saída `dumpbin /exports`, você pode ver o nome exato da função, incluindo caracteres não alfanuméricos. Isso é útil para definir um ponto de interrupção em uma função. Nomes de função de tabelas de exportação de dll podem aparecer truncados em outro lugar no depurador. As chamadas são listadas na ordem de chamada, com a função atual (a mais profundamente aninhada) na parte superior. Para obter mais informações, consulte [dumpbin/exportações](/cpp/build/reference/dash-exports).

**Mostrar pilhas paralelas de baixo para cima do diagrama**:  
Controla a direção na qual as pilhas são exibidas na **pilhas paralelas** janela.

**Ignorar as exceções de acesso de memória GPU, se os dados gravados não tiver alterado o valor**:  
Ignora as condições de corrida que foram detectadas durante a depuração caso os dados não forem alterados. Para obter mais informações, consulte [depurando código de GPU](../debugger/debugging-gpu-code.md).

**Usar o modo de compatibilidade gerenciado**:  
Substitui o mecanismo de depuração padrão com uma versão herdada para habilitar estes cenários:

- Você estiver usando uma linguagem .NET Framework diferente de C#, Visual Basic, ou F# que fornece seu próprio avaliador de expressão (Isso inclui C + + c++ CLI).

- Você deseja habilitar editar e continuar para projetos do C++ durante a depuração de modo misto.

> [!NOTE]
> O modo escolhendo compatibilidade gerenciada desativa alguns recursos que são implementados somente no mecanismo de depuração padrão.

**Use o novas C# e os avaliadores de expressão de VB**:  
O depurador usará o Visual Studio 2013 C# ou Visual Basic avaliadores de expressão em vez dos avaliadores de expressão baseada em Roslyn de 2015 do Visual Studio.

**Avisar ao usar os visualizadores do depurador personalizados contra processos potencialmente inseguros (somente gerenciado)**:  
Visual Studio avisa você quando você estiver usando um visualizador de depurador personalizada que está executando código no processo depurado, porque ele pode estar executando o código não seguro.

**Habilitar alocador de heap de depuração do Windows (somente nativo)**:  
Permite que o heap de depuração do windows melhorar o diagnóstico de heap. Habilitar essa opção afetará o desempenho de depuração.

**Habilitar ferramentas de depuração para XAML**:  
A Live Visual Tree e os windows Live propriedade explorar aparecerá quando você iniciar a depuração (**F5**) um tipo de projeto com suporte. Para obter mais informações, consulte [propriedades de XAML de inspecionar durante a depuração](../debugger/inspect-xaml-properties-while-debugging.md).

- **Visualizar os elementos selecionados no Live Visual Tree**:  
    O elemento XAML cujo contexto é selecionado também está selecionado na **Live Visual Tree** janela.

- **Mostrar ferramentas de tempo de execução no aplicativo**:  
    Mostra a **Live Visual Tree** comandos em uma barra de ferramentas na janela principal do aplicativo XAML que está sendo depurado. Essa opção foi introduzida no Visual Studio 2015 atualização 2.

- **Habilitar o XAML Edit and Continue**:  
    Permite que você usar o editar e continuar o recurso com o código XAML.

**Habilitar ferramentas de diagnóstico durante a depuração**:  
O **ferramentas de diagnóstico** janela é exibida enquanto você está depurando.

**Mostrar tempo decorrido PerfTip durante a depuração**:  
A janela de código exibe o tempo decorrido de uma chamada de método fornecido quando você estiver depurando.

**Habilitar Editar e continuar**:  
Habilita a funcionalidade de editar e continuar durante a depuração.

- **Habilitar nativo editar e continuar**:  
    Você pode usar o editar e continuar a funcionalidade durante a depuração de código C++ nativo. Para obter mais informações, consulte [editar e continuar (Visual C++)](../debugger/edit-and-continue-visual-cpp.md).

- **Aplicar alterações ao continuar (somente nativo)**:  
    Visual Studio automaticamente compila e aplica as alterações de código pendentes feitas ao continuar o processo de um estado de interrupção. Se não estiver selecionada, você pode optar por aplicar as alterações usando o **aplicar alterações de código** item sob o **depurar** menu.

- **Avisar sobre código obsoleto (somente nativo)**:  
    Obter avisos sobre código obsoleto.

**Mostrar execução ao clique de botão no editor durante a depuração**:  
Quando essa opção é selecionada, o [executar com um clique](debugger-feature-tour.md#run-to-a-point-in-your-code-quickly-using-the-mouse) botão será mostrado durante a depuração.

**Fechar automaticamente o console ao parar a depuração**:  
Informa ao Visual Studio para fechar o console no final de uma sessão de depuração.

## <a name="options-available-in-older-versions-of-visual-studio"></a>Opções disponíveis em versões mais antigas do Visual Studio

Se você estiver usando uma versão mais antiga do Visual Studio, algumas opções adicionais podem estar presentes.

**Habilitar o Assistente de exceção**:  
Para código gerenciado, permite que o Assistente de exceção. No Visual Studio 2017, o auxiliar de exceção substituído o Assistente de exceção.

**Desenrolar a pilha de chamadas em exceções não tratadas**:  
Faz com que o **pilha de chamadas** janela para reverter a pilha de chamadas para o ponto antes da ocorrência de exceção sem tratamento.

**Avisar se não houver símbolos na inicialização (somente nativo)**:  
Exibe uma caixa de diálogo de aviso quando você depura um programa para o qual o depurador não tem nenhuma informação de símbolo.

**Avisar se a depuração de script estiver desabilitada na inicialização**:  
Exibe uma caixa de diálogo de aviso quando o depurador é iniciado com a depuração de script desabilitada.

**Usar o modo de compatibilidade nativa**:  
Quando essa opção é selecionada, o depurador usa o depurador nativo do Visual Studio 2010, em vez do novo depurador nativo.

- Use esta opção quando você estiver depurando o código C++ .NET, pois o novo mecanismo de depuração não dá suporte a expressões de avaliação C++ .NET. No entanto, a habilitação do modo de compatibilidade nativa desabilita muitos recursos que dependem da implementação atual do depurador para operar. Por exemplo, o mecanismo herdado não tem muitos visualizadores para tipos internos, como `std::string` em projetos do Visual Studio 2015.   Use os projetos do Visual Studio 2013 para a melhor experiência de depuração nesses casos.

## <a name="see-also"></a>Consulte também

- [Depurando no Visual Studio](../debugger/index.md)
- [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)