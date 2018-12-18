---
title: Exibir o estado anterior do aplicativo usando o IntelliTrace
ms.description: Learn how to take snapshots, and view snapshots with IntelliTrace step-back
ms.custom: mvc
ms.date: 09/19/2018
ms.technology: vs-ide-debug
ms.topic: tutorial
ms.assetid: 7c60d929-d993-49dc-9db3-43b30be9912b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6d43e1a04570d68ce69f283cde264280fc24865a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49846857"
---
# <a name="inspect-previous-app-states-using-intellitrace-step-back-in-visual-studio"></a>Inspecionar estados anteriores do aplicativo usando o retrocesso do IntelliTrace no Visual Studio

O retrocesso do IntelliTrace tira automaticamente um instantâneo do seu aplicativo em cada evento de etapa do depurador e do ponto de interrupção. Os instantâneos registrados permitem retornar aos pontos de interrupção ou às etapas anteriores e exibir o estado do aplicativo como ele era no passado. O retrocesso do IntelliTrace poderá poupar seu tempo quando você desejar ver o estado do aplicativo anterior, mas não desejar reiniciar a depuração nem recriar o estado do aplicativo desejado.

O retrocesso do IntelliTrace passar a estar disponível do Visual Studio Enterprise 2017 versão 15.5 e posterior e ele requer a Atualização de Aniversário do Windows 10 ou superior. Atualmente, o recurso é compatível com depuração de ASP.NET, WinForms, WPF, aplicativos de console gerenciados e bibliotecas de classes gerenciadas. Começando com o Visual Studio 2017 Enterprise versão 15.7, o recurso também dá suporte ao ASP.NET Core e ao .NET Core. Começando com o Visual Studio 2017 Enterprise versão 15.9 Versão prévia 2, o recurso também dá suporte aos aplicativos nativos destinados ao Windows. Atualmente, não há suporte para a depuração de aplicativos UWP.

Neste tutorial, você irá:

> [!div class="checklist"]
> * Habilitar instantâneos e eventos do IntelliTrace
> * Navegar pelos eventos usando os comandos de retrocesso e de avanço
> * Exibir instantâneos de evento
  
## <a name="enable-intellitrace-events-and-snapshots-mode"></a>Habilitar o modo de eventos e instantâneos do IntelliTrace 

1. Abra seu projeto no Visual Studio Enterprise.

1. Abra as configurações **Ferramentas** > **Opções** > **IntelliTrace** e selecione a opção **Eventos e instantâneos do IntelliTrace**. 

    Começando no Visual Studio 2017 Enterprise versão 15.9 Versão prévia 2, essa opção passou a ser **Instantâneos do IntelliTrace (gerenciados e nativos)**. 

    ![Habilitar o modo de Eventos e Instantâneos do IntelliTrace](../debugger/media/intellitrace-enable-snapshots.png "Habilitar o modo de Eventos e Instantâneos do IntelliTrace")

1. Se você deseja configurar as opções para exibição de instantâneos em exceções, escolha **IntelliTrace** > **Avançado** na caixa de diálogo **Opções**.

    Essas opções estão disponíveis no Visual Studio 2017 Enterprise versão 15.7 em diante.

    ![Configurar o comportamento de instantâneos em exceções](../debugger/media/intellitrace-enable-snapshots-on-exceptions.png)

    Quando você habilita eventos e instantâneos, tirar instantâneos em exceções também é habilitado por padrão. Você pode desabilitar os instantâneos em exceções, desmarcando **Coletar instantâneos em eventos de exceção**. Quando esse recurso está habilitado, os instantâneos são obtidos nas exceções sem tratamento. Para exceções tratadas, os instantâneos serão obtidos somente se a exceção for lançada e se não for um relançamento de uma exceção gerada anteriormente. Você pode definir um número máximo de instantâneos em exceções selecionando um valor na lista suspensa. O máximo se aplica a cada vez que o aplicativo entra em modo de interrupção (por exemplo, quando o aplicativo atinge um ponto de interrupção).

    > [!NOTE]
    > Os instantâneos são obtidos somente para eventos de exceção que o IntelliTrace registra. No código gerenciado, você pode especificar quais eventos o IntelliTrace registra, selecionando **Ferramentas** > **Opções** > **Eventos do IntelliTrace**.

1. Em seu projeto, defina um ou mais pontos de interrupção e inicie a depuração (pressione **F5**) ou inicie a depuração percorrendo seu código (**F10** ou **F11**).

    O IntelliTrace obtém um instantâneo do processo do aplicativo em cada etapa do depurador, em cada evento de ponto de interrupção e em cada evento de exceção sem tratamento. Esses eventos são registrados na guia **Eventos** na janela **Ferramentas de Diagnóstico** junto com outros eventos do IntelliTrace. Para abrir essa janela, escolha **Depurar** > **Janelas** > **Mostrar Ferramentas de Diagnóstico**.

    Um ícone de câmera aparece próximo aos eventos para os quais os instantâneos estão disponíveis. 

    ![Guia Eventos com instantâneos](../debugger/media/intellitrace-events-tab-with-snapshots.png "Guia Eventos com instantâneos de pontos de interrupção e etapas")

    Por questões de desempenho, os instantâneos não são executados quando você percorre as etapas muito rapidamente. Se nenhum ícone de câmera aparecer próximo da etapa, tente depurar mais lentamente.

## <a name="navigate-and-view-snapshots"></a>Navegar e exibir instantâneos

1. Navegue entre os eventos usando os botões **Voltar Etapa (Alt + [)** e **Avançar Etapa (Alt +])** na barra de ferramentas Depurar.

    Esses botões navegam pelos eventos exibidos na guia **Eventos** na janela **Ferramentas de Diagnóstico**. Voltar ou avançar para um evento ativa automaticamente a [depuração histórica](../debugger/historical-debugging.md) no evento selecionado.

    ![Botões Voltar e Avançar Etapa](../debugger/media/intellitrace-step-back-icons-description.png "Botões Voltar e Avançar Etapa")

    Quando você volta ou avança uma etapa, o Visual Studio entra em modo de depuração histórica. Nesse modo, o contexto do depurador alterna para a hora em que o evento selecionado foi registrado. O Visual Studio também move o ponteiro para a linha de código correspondente na janela de origem. 

    Nessa exibição, você pode inspecionar os valores nas janelas **Pilha de Chamadas**, **Locais**, **Autos** e **Inspeção**. Você também pode passar o mouse sobre variáveis para exibir DataTips e executar a avaliação da expressão na janela **Imediato**. Os dados que você vê são do instantâneo do processo do aplicativo executado naquele momento.

    Portanto, por exemplo, se você alcançou um ponto de interrupção e realizou uma Etapa (**F10**), o botão **Voltar Etapa** coloca o Visual Studio no modo histórico na linha de código correspondente ao ponto de interrupção. 

    ![Ativando o modo histórico em um evento com um instantâneo](../debugger/media/intellitrace-historical-mode-with-snapshot.png "Ativando o modo histórico em um evento com um instantâneo")

2. Para retornar à execução ao vivo, escolha **Continuar (F5)** ou clique no link **Retornar à depuração ao vivo** na barra de informações. 

3. Você também pode exibir um instantâneo na guia **Eventos**. Para fazer isso, selecione um evento com um instantâneo e clique em **Ativar Depuração Histórica**.

    ![Ativar Depuração Histórica em um evento](../debugger/media/intellitrace-activate-historical-debugging.png "Ativar Depuração Histórica em um evento")

    Ao contrário do comando **Definir Próxima Instrução**, a exibição de um instantâneo não executa novamente seu código; ela fornece uma exibição estática do estado do aplicativo em um ponto no tempo ocorrido no passado.

    ![Visão geral do retrocesso do IntelliTrace](../debugger/media/intellitrace-step-back-overview.png "Visão geral do retrocesso do IntelliTrace")

    Para saber mais sobre como inspecionar variáveis no Visual Studio, confira [Tour pelas funcionalidades do depurador](../debugger/debugger-feature-tour.md)  

## <a name="frequently-asked-questions"></a>Perguntas frequentes

#### <a name="how-is-intellitrace-step-back-different-from-intellitrace-events-only-mode"></a>Qual a diferença entre o retrocesso do IntelliTrace e o modo somente eventos do IntelliTrace?

O IntelliTrace no modo somente eventos permite que você ative a depuração histórica em pontos de interrupção e etapas do depurador. No entanto, o IntelliTrace somente capturará dados nas janelas **Locais** e **Autos** se elas estiverem abertas e somente capturará dados que estejam expandidos e na exibição. No modo somente eventos, você geralmente não tem uma exibição completa das variáveis e de objetos complexos. Além disso, não há suporte para a avaliação de expressão e para a exibição de dados na janela **Inspeção**. 

No modo de eventos e instantâneos, o IntelliTrace captura todo o instantâneo do processo do aplicativo, incluindo objetos complexos. Em uma linha de código, você pode ver as mesmas informações como se você tivesse parado em um ponto de interrupção (e não importa se você expandiu previamente as informações). A avaliação da expressão também é compatível ao exibir um instantâneo.  

#### <a name="what-is-the-performance-impact-of-this-feature"></a>Qual é o impacto de desempenho desse recurso? 

O impacto no desempenho geral das etapas depende de seu aplicativo. A sobrecarga de tirar um instantâneo é de cerca de 30 ms. Quando um instantâneo é obtido, o processo do aplicativo é bifurcado e a cópia bifurcada é suspensa. Quando você exibe um instantâneo, o Visual Studio está anexando a cópia bifurcada do processo. Para cada instantâneo, o Visual Studio copia apenas a tabela de página e define as páginas como gravação de cópia. Se os objetos no heap forem alterados entre as etapas do depurador associadas a instantâneos, a respectiva tabela de página será copiada, resultando em um custo mínimo de memória. Se o Visual Studio detectar que não há memória suficiente para criar um instantâneo, ele não o fará.
 
## <a name="known-issues"></a>Problemas Conhecidos  
* Se você estiver usando o modo de eventos e instantâneos do IntelliTrace em versões do Windows anteriores ao Windows 10 Fall Creators Update (RS3) e se a plataforma de depuração de destino do aplicativo for definida como x86, o IntelliTrace não obterá instantâneos.

    Soluções alternativas:
  * Se você estiver na Atualização de Aniversário do Windows 10 (RS1) e anterior à versão 10.0.14393.2273, [instale o KB4103720](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720). 
  * Se você estiver com o Windows 10 Creators Update (RS2) e anterior à versão 10.0.15063.1112, [instale o KB4103722](https://support.microsoft.com/help/4103722/windows-10-update-4103722).
  * Instale ou atualize para o Windows 10 Fall Creators Update (RS3). 
  * Como alternativa: 
    1. Instale o conjunto de ferramentas do VC++ 2015.3 v140 para o componente de área de trabalho (x86, x64) do Instalador do Visual Studio.
    2. Compile o aplicativo de destino.
    3. Na linha de comando, use a ferramenta editbin para definir o sinalizador `Largeaddressaware` para o executável de destino. Por exemplo, você pode usar esse comando (depois de atualizar o caminho): "C:\Arquivos de Programas (x86)\Microsoft Visual Studio\Preview\Enterprise\VC\Tools\MSVC\14.12.25718\bin\Hostx86\x86\editbin.exe" /Largeaddressaware "C:\Path\To\Application\app.exe".
    4. Para iniciar a depuração, pressione **F5**. Agora, os instantâneos são obtidos em pontos de interrupção e etapas do depurador.

       > [!Note]
       > O sinalizador `Largeaddressaware` deverá ser definido sempre que o executável for recompilado com as alterações.

* Quando um instantâneo do processo do aplicativo for criado em um aplicativo que usa um arquivo persistente mapeado na memória, o processo com o instantâneo manterá um bloqueio exclusivo no arquivo mapeado em memória (mesmo depois que o processo pai liberar o bloqueio). Outros processos ainda serão capazes de ler, mas não de gravar no arquivo mapeado em memória.

    Solução alternativa:
    * Elimine todos os instantâneos encerrando a sessão de depuração. 

* Ao depurar um aplicativo cujo processo tenha um grande número de regiões de memória exclusivas, como um aplicativo que carrega um grande número de DLLs, o desempenho das etapas com instantâneos habilitados poderá ser afetado. Esse problema será abordado em uma versão futura do Windows. Se você estiver enfrentando esse problema, contate-nos em stepback@microsoft.com. 

* Ao salvar um arquivo com **Depurar > IntelliTrace > Salvar sessão do IntelliTrace** no modo de eventos e instantâneos, os dados adicionais capturados de instantâneos não ficarão disponíveis no arquivo .itrace. No modo de eventos de ponto de interrupção e etapa, você vê as mesmas informações como se tivesse salvo o arquivo no modo somente eventos do IntelliTrace. 

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como usar o retrocesso do IntelliTrace. Pode ser interessante saber mais sobre outros recursos do IntelliTrace.

> [!div class="nextstepaction"]
> [Recursos do IntelliTrace](../debugger/intellitrace-features.md)
