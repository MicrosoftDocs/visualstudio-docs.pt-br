---
title: 'Passo a passo: Identificando problemas de desempenho | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- profiling tools, walkthroughs
- performance tools, walkthroughs
- performance, analyzing
- profiling applications, walkthroughs
ms.assetid: 36f6f123-0c14-4763-99c3-bd60ecb95b87
caps.latest.revision: 58
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9d26e6ccabcdff12b8f4d9839888e17dc1ab3ce4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745362"
---
# <a name="walkthrough-identifying-performance-problems"></a>Passo a passo: Identificando problemas de desempenho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo demonstra como criar um perfil de um aplicativo para identificar problemas de desempenho.  
  
 Neste passo a passo, você passará pelo processo de criação de perfil de um aplicativo gerenciado, usando amostragem e instrumentação para isolar e identificar problemas de desempenho no aplicativo.  
  
 Neste passo a passo, você seguirá estas etapas:  
  
-   Crie o perfil de um aplicativo usando o método de amostragem.  
  
-   Analise os resultados da criação de perfil amostrada para localizar e corrigir um problema de desempenho.  
  
-   Crie o perfil de um aplicativo usando o método de instrumentação.  
  
-   Analise os resultados da criação de perfil instrumentada para localizar e corrigir um problema de desempenho.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
- Compreensão intermediária de C#.  
  
- Uma cópia de [Amostra do PeopleTrax](../profiling/peopletrax-sample-profiling-tools.md).  
  
  Para trabalhar com as informações fornecidas pela criação de perfil, é bom ter as informações de símbolo de depuração disponíveis.  
  
## <a name="profiling-by-using-the-sampling-method"></a>Criação de perfil usando o método de amostragem  
 A amostragem é um método de criação de perfil pelo qual o processo em questão é monitorado periodicamente para determinar a função ativa. Os dados resultantes fornecem uma contagem da frequência da função na parte superior da pilha de chamadas, quando o processo foi amostrado.  
  
#### <a name="to-profile-an-application-by-using-the-sampling-method"></a>Para criar o perfil de um aplicativo usando o método de amostragem  
  
1.  Abra [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] com privilégios de administrador. Para a criação de perfil, é necessário executar como administrador.  
  
2.  Abra a solução PeopleTrax.  
  
     A solução PeopleTrax agora preenche o Gerenciador de Soluções.  
  
3.  Defina a configuração do projeto como **Versão**.  
  
     Você deve usar um build de versão para detectar problemas de desempenho no aplicativo. Um build de versão é recomendado para criação de perfil porque um build de depuração contém informações adicionais compiladas que podem afetar negativamente o desempenho e não ilustrar os problemas de desempenho com precisão.  
  
4.  No menu **Analisar**, clique em **Iniciar o Assistente de Desempenho**.  
  
     O Assistente de Desempenho é exibido.  
  
5.  Certifique-se de que a **Amostragem de CPU (recomendada)** está selecionada e clique em **Avançar**.  
  
6.  Em **Para qual aplicativo o perfil deve ser criado?**, selecione PeopleTrax e clique em **Avançar**.  
  
     [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] compila o projeto e inicia a criação de perfil do aplicativo. A janela do aplicativo **PeopleTrax** é exibida.  
  
7.  Clique em **Get People**.  
  
8.  Clique em **ExportData**.  
  
     O bloco de notas é aberto e exibe um novo arquivo que contém os dados exportados do **PeopleTrax**.  
  
9. Feche o bloco de notas e, em seguida, feche o aplicativo **PeopleTrax**.  
  
     O criador de perfil gera um arquivo de dados de criação de perfil (\*. vsp), lista o nome de arquivo na seção de relatórios da janela Gerenciador de Desempenho e carrega automaticamente a exibição **Resumo** do arquivo de dados na janela principal do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  
  
#### <a name="to-analyze-sampled-profiling-results"></a>Para analisar os resultados de criação de perfil amostrada  
  
1.  A exibição Resumo exibe uma linha do tempo de utilização da CPU ao longo da execução de criação de perfil, a lista **Afunilamento**, que representa a ramificação da árvore de chamada do aplicativo que estava mais ativo e uma lista das **Funções Que Realizam a Maioria do Trabalho Individual**, que mostra as funções mais intensamente amostradas durante a execução de código no próprio corpo da função.  
  
     Examine a lista **Afunilamento** e observe que o método PeopleNS.People.GetNames é a função do PeopleTrax mais próxima ao final da lista. Sua posição a torna um bom candidato para análise. Clique no nome da função para exibir detalhes dos GetNames na exibição **Detalhes da Função**.  
  
2.  A exibição **Detalhes da Função** contém duas janelas. A janela de distribuição de custo fornece uma exibição gráfica do trabalho feito pela função, o trabalho realizado pelas funções chamadas e a contribuição de funções que chamaram a função para o número de instâncias amostradas. Você pode alterar a função que é o foco do modo de exibição, clicando em um nome de função. Por exemplo, você pode clicar em PeopleNS.People.GetPeople para fazer de GetPeople a função selecionada.  
  
     A janela **Exibição de Código da Função** mostrará o código-fonte da função se ela estiver disponível e realça as linhas mais caras na função selecionada. Quando GetNames é selecionada, você pode ver que essa função lê uma cadeia de caracteres nos recursos do aplicativo e, em seguida, usa um <xref:System.IO.StringReader> para adicionar cada linha da cadeia de caracteres a uma <xref:System.Collections.ArrayList>. Não há maneira óbvia de otimizar essa função.  
  
3.  Como PeopleNS.People.GetPeople é o único chamador de GetNames, clique em GetPeople na janela de distribuição de custos para examinar seu código. Esse método retorna uma <xref:System.Collections.ArrayList> de objetos PersonInformationNS.PersonInformation dos nomes de pessoas e empresas produzidos por GetNames. No entanto, GetNames é chamado duas vezes toda vez que um objeto PersonInformation é criado. Você pode ver que o método pode ser facilmente otimizado criando as listas apenas uma vez no início do método e indexando a essas listas durante o loop de criação de PersonInformation.  
  
4.  Uma versão alternativa de GetPeople é fornecida com o código do aplicativo de exemplo e você poderá chamar a função otimizada adicionando um símbolo de build condicional às propriedades de build. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Propriedades**. Clique em **Compilar** no menu de página de propriedades e digite **OPTIMIZED_GETPEOPLE** na caixa de texto do símbolo de build condicional. A versão otimizada de GetPeople substitui o método original na próximo build.  
  
5.  Execute novamente a sessão de desempenho. Na barra de ferramentas do Gerenciador de Desempenho, clique em **Iniciar com Criação de Perfil**. Clique em **Get People** e, em seguida, clique em **Exportar Dados**. Feche a janela do bloco de notas que aparece e, em seguida, feche o aplicativo People Trax.  
  
     Um novo arquivo de dados de criação de perfil é gerado e uma exibição **Resumo** dos novos dados aparece na janela principal [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  
  
6.  Para comparar as duas execuções de criação de perfil, selecione os dois arquivos de dados no Gerenciador de Desempenho, clique com botão direito do mouse nos arquivos e, em seguida, clique em **Comparar Relatórios de Desempenho**. Uma janela de Relatório de Comparação é exibida na janela principal [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. A coluna **Delta** mostra a alteração no valor do desempenho das funções, desde o valor anterior da **Linha de Base** até o último valor de **Comparação**. Você pode selecionar os valores a serem comparados na lista suspensa **Coluna**. Selecione **% de Amostras Inclusivas**.  
  
     Observe que os métodos GetPeople e GetNames mostram ganhos de desempenho consideráveis.  
  
## <a name="profiling-by-using-the-instrumentation-method"></a>Criação de perfil usando o método de instrumentação  
 A instrumentação é um método de criação de perfil em que o criador de perfil insere funções de teste em versões especialmente criadas de binários com perfil. Os testes que coletam informações de tempo na entrada e saída das funções nos módulos instrumentados e em todos os sites de chamada nessas funções. O processo de instrumentação é útil para investigar problemas relacionados a operações de entrada/saída como, por exemplo, gravação em disco e a comunicação em uma rede. As instrumentação fornece informações mais detalhadas do que a amostragem, mas é mais invasiva na execução do processo e resulta em maior quantidade de sobrecarga. Binários instrumentados também são maiores do que os binários de depuração ou liberação e não são destinados a implantação.  
  
 Nesta seção do passo a passo, usaremos o método de instrumentação para descobrir mais códigos que podemos otimizar no aplicativo PeopleTrax para o qual criamos antes um perfil. Usando o filtro da linha do tempo da exibição Resumo, concentraremos nossa análise do cenário de dados de exportação no aplicativo com perfil, no qual a lista de pessoas é gravada em um arquivo do bloco de notas.  
  
#### <a name="to-profile-an-existing-application-by-using-the-instrumentation-method"></a>Para criar o perfil de um aplicativo existente usando o método de instrumentação  
  
1.  Se necessário, abra o aplicativo PeopleTrax no Visual Studio.  
  
     Verifique se você está executando como administrador e se a configuração de build da solução está definida como **Versão**.  
  
2.  No Gerenciador de Desempenho, clique em **Instrumentação**.  
  
3.  Na barra de ferramentas do Gerenciador de Desempenho, clique em **Iniciar com Criação de Perfil**.  
  
     O criador de perfil compila o projeto e inicia a criação de perfil do aplicativo. A janela do aplicativo PeopleTrax é exibida.  
  
4.  Clique em **Get People**.  
  
     A grade de dados do PeopleTrax é preenchida com os dados.  
  
5.  Aguarde cerca de 10 segundos e, em seguida, clique em **Exportar Dados**.  
  
     O **bloco de notas** é iniciado e exibe um novo arquivo que contém uma lista de pessoas do PeopleTrax. A espera permite que você identifique mais facilmente o procedimento de exportação de dados para filtragem.  
  
6.  Feche o **bloco de notas** e, em seguida, feche o aplicativo **PeopleTrax**.  
  
     [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] gera um relatório de sessão de desempenho (*.vsp).  
  
#### <a name="to-analyze-instrumented-profiling-results"></a>Para analisar resultados de criação de perfil instrumentado  
  
1. O gráfico de linha do tempo da exibição **Resumo** do relatório mostra a utilização de CPU do programa durante a execução da criação de perfil. A operação de exportação de dados deve ser o grande pico ou o limite no lado direito do gráfico. É possível filtrar a sessão de desempenho para exibir e analisar apenas os dados coletados na operação de exportação. Clique à esquerda do ponto no gráfico em que começa a operação de exportação de dados. Clique novamente à direita da operação. Em seguida, clique em **Filtrar por Seleção** na lista de links à direita da linha do tempo.  
  
    A árvore de **Afunilamento** mostra que o método <xref:System.String.Concat%2A> chamado pelo método PeopleTrax.Form1.ExportData consome um grande percentual do tempo. Como **System.String.Concat** também está na parte superior da lista **Funções com Mais Trabalho Individual**, reduzir o tempo gasto na função é um ponto provável de otimização.  
  
2. Clique duas vezes em **System.String.Concat** em qualquer uma das tabelas de resumo para obter mais informações na exibição Detalhes da Função.  
  
3. Você pode ver que o PeopleTrax.Form1.ExportData é o único método que chama Concat. Clique em **PeopleTrax.Form1.ExportData** na lista **Chamando Funções** para selecionar o método como o destino da exibição Detalhes da Função.  
  
4. Examine o método na janela Exibição de Código da Função. Observe que não há nenhuma chamada literal para **System.String.Concat**. Em vez disso, há vários usos do operando +=, que o compilador substitui por chamadas para **System.String.Concat**. Quaisquer modificações em uma cadeia de caracteres no .NET Framework faz com que uma nova cadeia de caracteres seja alocada. O .NET Framework inclui uma classe <xref:System.Text.StringBuilder> que é otimizada para concatenação de cadeia de caracteres  
  
5. Para substituir essa área de problema por código otimizado, adicione OPTIMIZED_EXPORTDATA como um símbolo de compilação condicional ao projeto PeopleTrax.  
  
6. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto PeopleTrax e clique em **Propriedades**.  
  
    O formulário de propriedades do projeto PeopleTrax aparece.  
  
7. Clique na guia **Build**.  
  
8. Na caixa de texto **Símbolos de compilação condicional**, digite **OPTIMIZED_EXPORTDATA**.  
  
9. Feche o formulário de propriedades do projeto e escolha **Salvar tudo** ao ser solicitado.  
  
   Quando você executar o aplicativo novamente, verá melhorias marcadas no desempenho. É recomendável que você execute a sessão de criação de perfil novamente, mesmo que haja melhorias visíveis no desempenho do usuário. É importante revisar os dados depois de corrigir um problema porque o primeiro problema pode obscurecer algum outro problema.  
  
## <a name="see-also"></a>Consulte também  
 [Visões gerais](../profiling/overviews-performance-tools.md)   
 [Introdução](../profiling/getting-started-with-performance-tools.md)   
 [/Z7, /Zi, /ZI (Formato de Informações de Depuração)](http://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8)



