---
title: Solução de problemas e problemas conhecidos (Ferramentas do VS para Unity)
description: Leia sobre solução de problemas no Ferramentas do Visual Studio para Unity. Consulte as descrições de problemas conhecidos e saiba mais sobre as soluções para esses problemas.
ms.custom: ''
ms.date: 04/15/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: troubleshooting
ms.assetid: 8f5db192-8d78-4627-bd07-dbbc803ac554
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: 37ee35fa66d37f9b85af01f5012e8ede76e877de
ms.sourcegitcommit: 3e1ff87fba290f9e60fb4049d011bb8661255d58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107879363"
---
# <a name="troubleshooting-and-known-issues-visual-studio-tools-for-unity"></a>Solução de problemas e problemas conhecidos (Ferramentas do Visual Studio para Unity)

Nesta seção, você encontrará soluções para problemas comuns das Ferramentas do Visual Studio para Unity, as descrições de problemas conhecidos e aprenderá como ajudar a melhorar as Ferramentas do Visual Studio para Unity por meio de relatórios de erro.

## <a name="troubleshooting-the-connection-between-unity-and-visual-studio"></a>Solução de problemas com a conexão entre o Unity e o Visual Studio

### <a name="confirm-editor-attaching-is-enabled-or-code-optimization-on-startup-is-set-to-debug"></a>Confirmar `Editor Attaching` está habilitado ou `Code Optimization On Startup` definido como `Debug`

No menu do Unity, selecione `Edit / Preferences` .

Dependendo da versão do Unity usada:
- Confirme se `Code Optimization On Startup` está definido como `Debug` .
- Ou selecione a `External Tools` guia. Confirme se a `Editor Attaching` caixa de seleção está habilitada. 

Para saber mais, confira a [Documentação de preferências do Unity](https://docs.unity3d.com/Manual/Preferences.html).

### <a name="unable-to-attach"></a>Não é possível anexar

- Tente desabilitar o antivírus temporariamente ou criar regras de exclusão para o VS e o Unity.
- Tente desabilitar o firewall temporariamente ou criar regras para permitir a rede TCP/UDP entre o Unity e o VS.
- Alguns programas, como o Team Viewer, podem interferir com a detecção do processo. Você pode tentar interromper temporariamente algum software adicional para ver se algo muda.
- Não renomeie o executável principal do Unity, uma vez que o VSTU está monitorando apenas os processos de “Unity.exe”.

## <a name="visual-studio-crashes"></a>O Visual Studio falha

O problema pode ser causado pela corrupção do cache do MEF do Visual Studio.

Tente remover a pasta a seguir para redefinir o cache do MEF (feche o Visual Studio antes de fazer isso):

```batch
%localappdata%\Microsoft\VisualStudio\<version>\ComponentModelCache
```

Isso deve corrigir o problema. Caso o problema persista, execute um prompt de comando do desenvolvedor do Visual Studio como administrador e use o seguinte comando:

```batch
 devenv /setup
```

## <a name="visual-studio-stops-responding"></a>O Visual Studio para de responder

Vários plug-ins do Unity como Parse, FMOD, UMP (Player de Mídia Universal), ZFBrowser ou Embedded Browser usam threads nativos. Isso é um problema quando um plug-in acaba anexando um thread nativo ao runtime, fazendo chamadas de bloqueio para o sistema operacional. Isso significa que o Unity não pode interromper esse thread para o depurador (ou recarregamento de domínio) e parar de responder.

Para o FMOD, há uma solução alternativa. Você pode passar o [sinalizador](https://www.fmod.com/resources/documentation-studio?version=2.0&page=https://fmod.com/resources/documentation-api?version=2.0&page=studio-api-system.html#fmod_studio_initflags) de inicialização `FMOD_STUDIO_INIT_SYNCHRONOUS_UPDATE` para desabilitar o processamento assíncrono e executar todo o processamento no thread principal.

## <a name="incompatible-project-in-visual-studio"></a>Projeto incompatível no Visual Studio

A coisa muito importante a saber é que o Visual Studio está salvando o estado "incompatível" nas configurações do projeto e não tentará recarregar um projeto até que você o use explicitamente `Reload Project` . Assim, após cada etapa de solução de problemas, certifique-se de tentar reabrir a solução e tente clicar com o botão direito do mouse em todos os projetos incompatíveis e escolher `Reload Project` .

1. Verifique se o Visual Studio está definido como seu editor de script externo no Unity usando `Edit / Preferences / External Tools` .
2. Dependendo da sua versão do Unity:
   - Verifique se o plug-in do Visual Studio está instalado no Unity. `Help / About` deve exibir uma mensagem como Microsoft Visual Studio ferramentas para o Unity está habilitada na parte inferior.
   - Unity 2020. x +: Verifique se você está usando o pacote mais recente do editor do Visual Studio no `Window / Package Manager` .
3. Tente excluir todos os projetos/arquivos de solução e a `.vs` pasta em seu projeto.
4. Tente recriar projetos/solução usando o `Open C# Project` ou o `Edit / Preferences / External tools / Regenerate Project files` .
5. Verifique se você instalou a carga de trabalho Game/Unity no Visual Studio.
6. Tente limpar o cache do MEF conforme explicado [aqui](#visual-studio-crashes).
7. Tente reinstalar o Visual Studio (usando a carga de trabalho Game/Unity somente para iniciar).
8. Tente desabilitar extensões de terceiros caso elas possam interferir na extensão do Unity no `Tools / Extensions` .

## <a name="extra-reloads-or-visual-studio-losing-all-open-windows"></a>Recargas extras, ou o Visual Studio perde todas as janelas abertas

Certifique-se de nunca tocar nos arquivos de projeto diretamente de um processador de ativos ou de qualquer outra ferramenta. Se você realmente precisar manipular o arquivo de projeto, expomos uma API para isso. Consulte a seção de [Problemas com referências de assembly](#assembly-reference-or-project-property-issues).

Se você tiver recargas extras ou se o Visual Studio estiver perdendo todas as janelas abertas ao recarregar, verifique se você tem os pacotes corretos de direcionamento do .NET instalados. Verifique a seção a seguir sobre estruturas para obter mais informações.

## <a name="the-debugger-does-not-break-on-exceptions"></a>O depurador não é interrompido quando há exceções

Ao usar o runtime do Unity herdado (equivalente ao .NET 3.5), o depurador sempre será interrompido quando uma exceção ficar sem tratamento (= fora de um bloco try/catch). Se a exceção for manipulada, o depurador usará a janela Configurações de Exceção para determinar se uma interrupção é necessária ou não.

Com o novo runtime (equivalente ao .NET 4.6), o Unity introduziu uma nova forma de gerenciar exceções de usuário e, como resultado, todas as exceções são vistas como "tratados pelo usuário", mesmo se estiverem fora de um bloco try/catch. Por isso, agora é necessário verificá-los explicitamente na janela Configurações de Exceção se você quiser que o depurador seja interrompido.

Na janela Configurações de Exceção (Depurar > Windows > Configurações de Exceção), expanda o nó de uma categoria de exceções (por exemplo, Exceções de Common Language Runtime, ou seja, exceções de .NET) e marque a caixa de seleção referente à exceção específica que você deseja capturar nessa categoria (por exemplo, System.NullReferenceException). Você também pode selecionar uma categoria inteira de exceções.

## <a name="on-windows-visual-studio-asks-to-download-the-unity-target-framework"></a>No Windows, o Visual Studio pede para baixar a estrutura de destino do Unity

Ao usar o tempo de execução do Unity herdado (equivalente do .NET 3,5), Ferramentas do Visual Studio para Unity requer o .NET Framework 3,5, que não está instalado por padrão no Windows 8 ou 10. Para corrigir esse problema, siga as instruções para baixar e instalar o .NET Framework 3.5.

Ao usar o novo tempo de execução do Unity, os pacotes de direcionamento do .NET versão 4,6 ou 4.7.1 também são necessários, dependendo da versão do Unity. É possível usar o instalador do Visual Studio para instalá-los rapidamente (modificar sua instalação, componentes individuais, categoria do .NET, selecionar todos os 4. x pacotes de direcionamento).

## <a name="assembly-reference-or-project-property-issues"></a>Referência de assembly ou problemas de Propriedade do projeto

Se seu projeto consegue lidar com referências complexas ou se você quiser controlar melhor essa etapa de geração, use nossa [API](../extensibility/customize-project-files-created-by-vstu.md) para manipular o conteúdo da solução ou do projeto gerado. Você também pode usar [arquivos de resposta](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html) no seu projeto Unity, que serão processados para você.

Com as versões recentes do Visual Studio e do Unity, a melhor abordagem parece usar um `Directory.Build.props` arquivo personalizado junto com seus projetos gerados. Você será capaz de contribuir para a estrutura do projeto sem interferir no processo de geração. Mais informações [aqui](https://docs.microsoft.com/visualstudio/msbuild/customize-your-build#directorybuildprops-and-directorybuildtargets).

## <a name="breakpoints-with-a-warning"></a>Pontos de interrupção com um aviso

Se o Visual Studio não conseguir encontrar um local de origem para um ponto de interrupção específico, você verá um aviso ao lado do ponto de interrupção. Verifique se o script que você está usando está carregado e está sendo usado corretamente na cena atual do Unity.

## <a name="breakpoints-not-hit"></a>Pontos de interrupção não atingidos

Verifique se o script que você está usando está carregado e está sendo usado corretamente na cena atual do Unity. Saia do Visual Studio e do Unity e exclua todos os arquivos gerados ( \* . csproj, \* . sln), a `.vs` pasta e a pasta de biblioteca inteira. Você pode encontrar mais informações sobre depuração em C# no [site](https://docs.unity3d.com/Manual/ManagedCodeDebugging.html)do Unity.

## <a name="unable-to-debug-android-players"></a>Não é possível depurar players Android

O multicast é usado para a detecção de player (que é o mecanismo padrão usado pelo Unity), mas depois disso, é usada uma conexão TCP regular para anexar o depurador. A fase de detecção é o principal problema para dispositivos Android.

O Wi-Fi é versátil, mas é muito lento em comparação com o USB devido à latência. Foi constatada uma falta de suporte adequado ao multicast para alguns roteadores ou dispositivos (a série Nexus é conhecida por isso).

O USB é bastante rápido para a depuração, e as Ferramentas do Visual Studio para Unity agora são capazes de detectar dispositivos USB e de se comunicar com o servidor adb para encaminhar corretamente as portas para depuração.

## <a name="issues-with-intellisense-or-code-coloration"></a>Problemas com o IntelliSense ou o Code coloração

Tente atualizar o Visual Studio para a versão mais recente. Experimente as mesmas etapas de solução de problemas para [projetos incompatíveis](#incompatible-project-in-visual-studio).

## <a name="known-issues"></a>Problemas conhecidos

Há problemas conhecidos nas Ferramentas do Visual Studio para Unity, decorrentes de como o depurador interage com a versão mais antiga do compilador C# do Unity. Estamos trabalhando para ajudar a corrigir esses problemas, mas, enquanto isso, você poderá enfrentar os seguintes problemas:

- O Unity pode falhar durante a depuração.

- O Unity pode congelar durante a depuração.

- A intervenção ou saída de métodos pode se comportar incorretamente, especialmente em iteradores ou em instruções switch.

## <a name="report-errors"></a>Relatar erros

Ajude-nos a melhorar a qualidade das Ferramentas do Visual Studio para Unity enviando relatórios de erro quando ocorrerem falhas, congelamentos ou outros erros. Isso nos ajuda a investigar e corrigir problemas nas Ferramentas do Visual Studio para Unity. Obrigado!

### <a name="how-to-report-an-error-when-visual-studio-freezes"></a>Como relatar um erro quando o Visual Studio congela

Há relatórios que indicam que, às vezes, o Visual Studio congela ao depurar com as Ferramentas do Visual Studio para Unity, mas precisamos de mais dados para entender esse problema. Ajude-nos a investigá-lo seguindo as etapas abaixo.

##### <a name="to-report-that-visual-studio-freezes-while-debugging-with-visual-studio-tools-for-unity"></a>Para relatar que o Visual Studio congela durante a depuração com as Ferramentas do Visual Studio para Unity

*No Windows:*

1. Abra uma nova instância do Visual Studio.

1. Abra o diálogo Anexar ao Processo. Na nova instância do Visual Studio, escolha **Depurar** e **Anexar ao Processo** no menu principal.

1. Anexe o depurador à instância congelada do Visual Studio. No diálogo **Anexar ao Processo**, selecione a instância congelada do Visual Studio na tabela **Processos Disponíveis** e, em seguida, escolha o botão **Anexar**.

1. Pause o Depurador. Na nova instância do Visual Studio, no menu principal, escolha **Depurar**, **Interromper Tudo** ou apenas pressione **Ctrl + Alt + Break**.

1. Crie um despejo de thread. Na janela Comando, insira o seguinte comando e pressione **Enter**:

    ```powershell
    Debug.ListCallStack /AllThreads /ShowExternalCode
    ```

    Talvez seja necessário tornar a janela **Comando** visível primeiro. No Visual Studio, escolha **Exibir**, **Outras Janelas**, **janela Comando** no menu principal.

*No Mac:*

1. Abra um terminal e obtenha o PID do Visual Studio para Mac:

    ```shell
    ps aux | grep "[V]isual Studio.app"
    ```

1. Inicie o depurador lldb:

    ```shell
    lldb
    ```

1. Anexe à instância do Visual Studio para Mac usando o PID:

    ```shell
    process attach --pid THE_PID_OF_THE_VSFM_PROCESS
    ```

1. Recupere o rastreamento de pilha de todos os threads:

    ```shell
    bt all
    ```

Por fim, envie o despejo de thread para [vstusp@microsoft.com](mailto:vstusp@microsoft.com) , juntamente com uma descrição do que você estava fazendo quando o Visual Studio ficou congelado.

## <a name="see-also"></a>Consulte também

- [Solução de problemas do Visual Studio](/troubleshoot/visualstudio/welcome-visual-studio/)
