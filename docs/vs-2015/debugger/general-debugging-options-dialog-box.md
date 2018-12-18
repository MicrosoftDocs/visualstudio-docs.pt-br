---
title: Geral, depuração, caixa de diálogo de opções | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.options.General
- VS.ToolsOptionsPages.Debugger.General
- VS.ToolsOptionsPages.Debugger.ENC
- vs.debug.options.ENC
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- Options dialog box, debugging
ms.assetid: b33aee0b-43c3-4c26-8ed4-bc673f491503
caps.latest.revision: 50
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e3a9e0b8008da5b648ae156235a20964fc0952b1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51742774"
---
# <a name="general-debugging-options-dialog-box"></a>Caixa de diálogo Geral, Depuração, Opções
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O**Ferramentas / opções / depuração / geral** página permite que você defina as seguintes opções:  
  
 **Perguntar antes de excluir todos os pontos de interrupção**  
 Requer a confirmação antes de concluir a **excluir todos os pontos de interrupção** comando.  
  
 **Interromper todos os processos quando um processo for interrompido**  
 Interrompe simultaneamente todos os processos ao qual o depurador é anexado, quando ocorre uma interrupção.  
  
 **Interromper quando exceções cruzarem AppDomain ou limites gerenciados/nativos**  
 Na depuração gerenciada ou de modo misto, o common language runtime pode capturar exceções que cruzem limites de domínio de aplicativo ou domínios gerenciados/nativos quando as seguintes condições forem verdadeiras:  
  
 1\) quando o código nativo chama código gerenciado usando interoperabilidade COM e o código gerenciado gera uma exceção. Ver [Introdução à interoperabilidade COM](http://msdn.microsoft.com/library/8bd62e68-383d-407f-998b-29aa0ce0fd67).  
  
 2\) quando o código gerenciado em execução no domínio do aplicativo 1 chama o código gerenciado no domínio do aplicativo 2, e o código no domínio do aplicativo 2 gera uma exceção. Ver [programação com domínios do aplicativo](http://msdn.microsoft.com/en-us/bd36055b-56bd-43eb-b4d8-820c37172131).  
  
 3\) quando o código chama uma função por meio de reflexão e a função gerará uma exceção. Ver [reflexão](http://msdn.microsoft.com/library/d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775).  
  
 Em 2) e 3), a exceção é às vezes detectada pelo código gerenciado em `mscorlib` em vez do common language runtime. Esta opção não afeta a quebra em exceções capturadas por `mscorlib`.  
  
 **Habilitar depuração no nível do endereço**  
 Habilita recursos avançados para depuração no nível do endereço (a **desmontagem** janela, o **registra** janela e pontos de interrupção de endereço).  
  
 **Mostrar desmontagem se a fonte não está disponível**  
 Mostra automaticamente a **desmontagem** janela quando você tenta depurar o código para o qual fonte não está disponível.  
  
 **Habilitar filtros de ponto de interrupção**  
 Permite que você defina filtros em pontos de interrupção de modo que eles afetem somente processos, threads ou computadores específicos.  
  
 **Habilitar o Assistente de exceção**  
 Somente para código gerenciado. Gerenciado exceções abrir a caixa de diálogo do Assistente de exceção.  Ver [Assistente de exceção](http://msdn.microsoft.com/library/992892ac-9d52-44cc-bf09-b44bfc5befeb).  
  
 **Desenrolar a pilha de chamadas em exceções não tratadas**  
 Faz com que o **pilha de chamadas** janela para reverter a pilha de chamadas para o ponto antes da ocorrência de exceção sem tratamento.  
  
 **Habilitar Apenas Meu Código**  
 O depurador exibe e as etapas no código do usuário ("meu código"), ignorando o código de sistema e outro código que é otimizado ou que não tem símbolos de depuração.  
  
 **Mostrar todos os membros dos objetos não usuário nas janelas de variáveis (somente Visual Basic)**  
 Ativa a exibição de membros não-públicos em objetos que são de código não usuário (não "My Code").  
  
 **Avisar se não houver código de usuário na inicialização**  
 Quando a depuração começa com o Just My Code ativado, esta opção advertirá você se não houver nenhum código de usuário ("My Code").  
  
 **Habilitar o .NET Framework depuração da origem**  
 Permite que o depurador entre na fonte do .NET Framework. Habilitar esta opção desativa automaticamente Apenas Meus Código dos símbolos do .NET Framework que serão baixados em um local do cache. Você pode alterar o local do cache na **opções** caixa de diálogo **depuração** categoria, **símbolos** página.  
  
 **Depurar propriedades e operadores (somente gerenciados)**  
 Impede que o depurador entre em propriedades e operadores no código gerenciado.  
  
 **Habilitar a avaliação de propriedade e outras chamadas de função implícitas**  
 Chama de ativar a avaliação automática de propriedades e de função implícitas nas janelas de variáveis e o **QuickWatch** caixa de diálogo.  
  
 **Chamar a função de conversão de cadeia de caracteres em objetos nas janelas de variáveis (c# e JavaScript apenas)**  
 Executa uma chamada de conversão de cadeia de caracteres implícita ao avaliar objetos em janelas de variáveis. Portanto, o resultado é exibido como uma cadeia de caracteres em vez do nome do tipo. Aplica-se somente à depuração no código em C. Essa configuração pode ser substituída pelo atributo DebuggerDisplay (consulte [usando o atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md)).  
  
 **Habilitar o suporte do servidor de origem**  
 Informe ao depurador do Visual Studio para obter os arquivos de origem dos servidores de origem que implementam o protocolo de SrcSrv (`srcsrv.dll`). Team Foundation Server e as ferramentas de depuração para Windows são dois servidores de origem que implementam o protocolo. Para obter mais informações sobre a configuração de SrcSrv, consulte a documentação Ferramentas de depuração para o Windows. Além disso, consulte [especificar arquivos de símbolo (. PDB) e código-fonte](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).  
  
> [!IMPORTANT]
>  Como ler arquivos .pdb pode executar o código arbitrário em arquivos, certifique-se de que você confia no servidor.  
  
 **Imprimir mensagens de diagnóstico de servidor de origem para a janela de saída**  
 Quando o suporte do servidor de origem é ativado, esta configuração ativa ao diagnóstico.  
  
 **Permitir que o servidor de origem para os assemblies de confiança parcial (somente gerenciado)**  
 Quando o suporte do servidor de origem é ativado, esta configuração substitui o comportamento padrão de não recuperar as fontes dos assemblies de confiança parcial.  
  
 **Realçar a linha inteira para pontos de interrupção e a instrução atual**  
 Quando o depurador realça um ponto de interrupção ou uma declaração atual, realça a linha inteira.  
  
 **Exigir arquivos de origem correspondam exatamente à versão original**  
 Informe ao depurador para verificar se um arquivo fonte corresponde à versão do código-fonte usado para criar o arquivo executável que você está depurando. Se a versão não corresponde, será solicitado que você localize uma origem correspondente. Se uma fonte compatível não for encontrada, o código-fonte não será exibido durante a depuração.  
  
 **Redirecionar todo o texto da janela Saída para a janela imediata**  
 Envia todas as mensagens do depurador que normalmente apareceriam na **saída** janela para o **imediato** janela em vez disso.  
  
 **Mostrar estrutura bruta de objetos nas janelas de variáveis**  
 Desative todas as personalizações de exibição da estrutura do objeto. Para obter mais informações sobre personalizações de exibição, consulte [criar exibições personalizadas de objetos gerenciados](../debugger/create-custom-views-of-dot-managed-objects.md).  
  
 **Suprimir Otimização JIT no carregamento do módulo (somente gerenciado)**  
 Desativa a otimização JIT de código gerenciado quando um módulo é carregado e JIT é compilado enquanto o depurador é anexado. Desativar a otimização pode facilitar a depuração de alguns problemas, embora às custas de desempenho. Se você estiver usando Apenas Meu Código, a supressão da otimização de JIT poderá fazer com que código que não seja do usuário apareça como código do usuário ("Meu Código").  
  
 **Avisar se não houver símbolos na inicialização (somente nativo)**  
 Exibe uma caixa de diálogo de aviso quando você tenta depurar um programa para o qual o depurador não tem nenhuma informação de símbolo.  
  
 **Avisar se a depuração de script estiver desabilitada na inicialização**  
 Exibe uma caixa de diálogo de aviso quando o depurador é iniciado com a depuração de script desabilitada.  
  
 **Carregar exportações de dll**  
 Carrega as tabelas de exportação de dll. Informações de símbolo de tabelas de exportação de dll podem ser útil se você estiver trabalhando com mensagens do Windows, procedimentos do Windows (WindowProcs), objetos COM, ou marshaling ou qualquer dll para o qual você não tem símbolos. Informações de exportação lendo dll envolve alguma sobrecarga. Desse modo, esse recurso é desativado por padrão.  
  
 Para ver quais símbolos estão disponíveis na tabela de exportação de uma dll, use `dumpbin /exports`. Símbolos estão disponíveis para qualquer dll do sistema de 32 bits. Ao ler a saída `dumpbin /exports`, você pode ver o nome exato da função, incluindo caracteres não alfanuméricos. Isso é útil para definir um ponto de interrupção em uma função. Nomes de função de tabelas de exportação de dll podem aparecer truncados em outro lugar no depurador. As chamadas são listadas na ordem de chamada, com a função atual (a mais profundamente aninhada) na parte superior. Para obter mais informações, consulte [dumpbin/exportações](http://msdn.microsoft.com/library/2971ab7e-4ee6-478b-9c85-cda42a4ce1bf).  
  
 **Mostrar diagrama de pilhas paralelas baixo para cima**  
 Controla a direção na qual as pilhas são exibidas na **pilhas paralelas** janela.  
  
 **Ignorar as exceções de acesso de memória GPU, se os dados gravados não tiver alterado o valor**  
 Ignora as condições de corrida detectadas durante a depuração caso os dados não tenham sido alterados. Para obter mais informações, consulte [depurando código de GPU](../debugger/debugging-gpu-code.md).  
  
 **Use o modo de compatibilidade gerenciado**  
 Substitui o mecanismo de depuração padrão com uma versão herdada para habilitar estes cenários:  
  
- Você está usando uma linguagem .NET Framework diferente de C#, VB ou F#, que fornece seu próprio Avaliador de Expressão (incluindo C++/CLI).  
  
- Você deseja habilitar editar e continuar para projetos do C++ durante a depuração de modo misto.  
  
  Observe que escolher o modo Compatibilidade gerenciada desativa alguns recursos que são implementados somente no mecanismo de depuração padrão.  
  
  **Use o modo de compatibilidade nativa**  
  Quando essa opção é selecionada, o depurador usa o depurador nativo do Visual Studio 2010, em vez do novo depurador nativo.  
  
  Você deve usar essa opção quando você estiver depurando o código C++ .NET, pois o novo mecanismo de depuração não dá suporte a expressões de avaliação C++ .NET. No entanto, a habilitação do modo de compatibilidade nativa desabilita muitos recursos que dependem da implementação atual do depurador para operar. Por exemplo, o mecanismo herdado não tem muitos visualizadores para tipos internos, como `std::string` em projetos do Visual Studio 2015.   Use projetos do Visual Studio 2013 para a melhor experiência de depuração nesses casos.  
  
  **Use os avaliadores de expressão c# e VB herdados**  
  O depurador usará os avaliadores de expressão do Visual Studio 2013 C# /VB em vez dos avaliadores de expressão baseada em Roslyn de 2015 do Visual Studio.  
  
  **Avisar ao usar os visualizadores do depurador personalizados contra processos potencialmente inseguros (somente gerenciado)**  
  Visual Studio avisa você quando você estiver usando um visualizador de depurador personalizada que está executando o código do processo de depuração, porque ele pode estar executando o código não seguro.  
  
  **Habilitar alocador de heap de depuração do Windows (somente nativo)**  
  Permite que o heap de depuração do windows melhorar o diagnóstico de heap. Habilitar essa opção afetará o desempenho de depuração.  
  
  **Habilitar ferramentas de depuração para XAML**  
  A Live Visual Tree e os windows Live propriedade explorar aparecerá quando você iniciar a depuração (F5) um tipo de projeto com suporte. Para obter mais informações, consulte [propriedades de XAML de inspecionar durante a depuração](../debugger/inspect-xaml-properties-while-debugging.md).  
  
  **Visualizar os elementos selecionados na árvore Visual dinâmica**  
  O elemento XAML cujo contexto é selecionado também está selecionado na **Live Visual Tree** janela.  
  
  **Mostrar ferramentas de tempo de execução no aplicativo**  
  Mostra a **Live Visual Tree** comandos em uma barra de ferramentas na janela principal do aplicativo XAML que está sendo depurado. Essa opção foi introduzida no Visual Studio 2015 atualização 2.  
  
  **Habilitar ferramentas de diagnóstico durante a depuração**  
  O **ferramentas de diagnóstico** janela é exibida enquanto você está depurando. Para obter mais informações, consulte [integradas ao depurador de criação de perfil](http://msdn.microsoft.com/library/a1f40370-7b61-42c2-afc4-0e13eba98859).  
  
  **Mostrar tempo decorrido PerfTip durante a depuração**  
  A janela de código exibe o tempo decorrido de uma chamada de método fornecido quando você estiver depurando.  
  
  **Habilitar Editar e continuar**  
  Você pode usar o editar e continuar a funcionalidade durante a depuração.  
  
  **Habilitar nativo editar e continuar**  
  Você pode usar o editar e continuar a funcionalidade durante a depuração de código C++ nativo. Para obter mais informações, consulte [editar e continuar (Visual C++)](../debugger/edit-and-continue-visual-cpp.md).  
  
  **Aplicar alterações ao continuar (somente nativo)**  
  Visual Studio automaticamente compila e aplica as alterações de código pendentes feitas ao continuar o processo de um estado de interrupção. Se não estiver selecionada, você pode optar por aplicar alterações usando o item de "Aplicar alterações de código" no menu Depurar.  
  
  **Avisar sobre código obsoleto (somente nativo)**  
  Obter avisos sobre código obsoleto.  
  
  **Permitir pré-compilação (somente nativo)**  
  Pré-compilação é permitida.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md)



