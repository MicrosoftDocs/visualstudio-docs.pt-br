---
title: Analisar o uso de memória do JavaScript em aplicativos UWP | Microsoft Docs
description: Saiba como o analisador de memória JavaScript está disponível para ajudá-lo a entender o uso de memória e encontrar vazamentos de memória em seus aplicativos UWP criados para Windows usando JavaScript.
ms.custom: ''
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- JavaScript
helpviewer_keywords:
- dominators, memory analyzer (JavaScript)
- memory leaks (JavaScript)
- heap memory, JavaScript
- leaks, memory (JavaScript)
- snapshots, memory analyzer (JavaScript)
- JavaScript Memory Analyzer
- analyzing memory, JavaScript
- memory analyzer, JavaScript
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f6fb446890c1485b6af249fd593cc9065bdba5aa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99918116"
---
# <a name="analyze-javascript-memory-usage-in-uwp-apps"></a>Analisar o uso de memória do JavaScript em aplicativos UWP
O analisador de memória do JavaScript está disponível no Visual Studio para ajudar você a entender o uso de memória e a localizar vazamentos de memória em seus aplicativos UWP compilados para o Windows usando JavaScript. Os aplicativos com suporte incluem aplicativos para Aplicativos Universais do Windows.

 O analisador de memória de JavaScript pode executar estas ações para você:

- Ajudá-lo a encontrar, com rapidez, problemas de uso de memória do seu aplicativo sublinhando os dados mais relevantes.

     Você obtém esses dados em resumos que mostram as diferenças entre dois instantâneos e fornecem links para modos de exibição mais detalhada.

- Fornecer exibições de dominators, tipos e raízes para ajudar a isolar problemas.

- Reduzir informações não acionáveis nos dados heap JavaScript.

     Os objetos que não são criados diretamente no seu código de aplicativo são filtrados automaticamente. Você também pode filtrar dados por nome de objeto.

## <a name="run-the-javascript-memory-analyzer"></a>Executar o analisador de memória de JavaScript
 Use o analisador de memória quando tiver um aplicativo de trabalho UWP aberto no Visual Studio.

#### <a name="to-run-the-memory-analyzer"></a>Para executar o Memory Analyzer

1. Abra o Visual Studio.

2. Se estiver executando o aplicativo pelo Visual Studio, na lista **Iniciar Depuração** na barra de ferramentas **Padrão**, escolha o destino de depuração do seu projeto: **Máquina Local** ou **Dispositivo**.

3. Na barra de menus, escolha **debug**  >  **Performance Profiler**.

     Por padrão, o projeto de inicialização atual é analisado. Se desejar alterar o destino da análise, escolha **Alterar Destino**.

     ![Destino da análise de alterações](../profiling/media/js_tools_target.png "JS_Tools_Target")

     As seguintes opções estão disponíveis para o destino de análise:

    - **Projeto de Inicialização**. Analisa o projeto de inicialização atual. Se você estiver executando o aplicativo em um computador remoto, escolha esta opção, que é o valor padrão.

    - **Aplicativo em Execução**. Permite selecionar um aplicativo UWP de uma lista de aplicativos em execução. Não é possível usar esta opção ao executar seu aplicativo em um computador remoto.

         Use esta opção para analisar o uso de memória de aplicativos em execução no seu computador quando você não tem acesso ao código-fonte.

    - **Aplicativo Instalado**. Permite selecionar um aplicativo UWP instalado que você deseja analisar. Não é possível usar esta opção ao executar seu aplicativo em um computador remoto.

         Use esta opção para analisar o uso de memória de aplicativos instalados no seu computador quando você não tem acesso ao código-fonte. Esta opção também pode ser útil quando você deseja apenas analisar o uso de memória de qualquer aplicativo fora do seu próprio desenvolvimento de aplicativo.

4. Em **Ferramentas Disponíveis**, marque a caixa de seleção **Memória JavaScript** e escolha **Iniciar**.

5. Quando você inicia o Memory Analyzer, a janela de Controle de Conta de Usuário pode solicitar sua permissão para executar o Visual Studio ETW Collector.exe. Escolha **Sim**.

     Interaja com o aplicativo para testar os cenários relevantes do uso de memória e exibir o gráfico de memória, conforme discutido nas seções a seguir.

6. Alterne para o Visual Studio pressionando a **tecla Alt** + .

7. Para exibir os dados reunidos pelo analisador de memória, escolha **Obter uma imagem instantânea do heap**. Consulte [Exibir um resumo de instantâneo](#view-a-snapshot-summary) posteriormente neste tópico.

## <a name="check-memory-usage"></a>Verifique o uso de memória
 Você pode tentar identificar vazamentos de memória usando diferentes exibições no analisador de memória de JavaScript. Se houver suspeita de perda de memória em seu aplicativo, consulte [Isolar perda de memória](#isolate-a-memory-leak) para obter uma sugestão de fluxo de trabalho.

 Use as seguintes exibições para ajudar a identificar vazamentos de memória em um aplicativo:

- [Exibir Resumo de uso de memória dinâmica](#view-live-memory-usage-summary). Use o gráfico de uso de memória para procurar aumento repentino do uso de memória ou uso de memória que aumenta de forma contínua, resultante de ações específicas. Use a exibição resumida do uso da memória ativa para tirar instantâneos do heap. Os instantâneos aparecem como uma coleção abaixo do gráfico de uso da memória.

    > [!TIP]
    > Você verá um aumento no uso de memória quando tirar um instantâneo. Use os resumos de instantâneo para ter uma indicação mais exata do crescimento.

- [Exiba um resumo de instantâneo](#view-a-snapshot-summary). Você pode exibir informações resumidas de instantâneo durante ou após uma sessão de criação de perfil de memória. Use os resumos de instantâneo para acessar detalhes de instantâneo e exibições diferenciais de instantâneo.

    > [!TIP]
    > Normalmente, as exibições diferenciais de instantâneo fornecem as informações mais úteis sobre vazamentos de memória.

- [Exibir detalhes do instantâneo](#view-snapshot-details). Mostra dados do uso de memória detalhados para um único instantâneo.

- [Exibir uma comparação de instantâneos](#view-a-snapshot-diff). Mostra valores diferenciais entre instantâneos. Essas exibições mostram diferenças de tamanho e número de objetos.

## <a name="isolate-a-memory-leak"></a>Isolar um vazamento de memória
 Estas etapas fornecem um fluxo de trabalho que pode ajudá-lo a usar o analisador de memória de JavaScript com mais eficiência. Estas etapas podem ser úteis se você suspeitar de vazamento de memória em seu aplicativo. Para ver um tutorial que percorre o processo de identificação de perda de memória em um aplicativo em funcionamento, consulte [Passo a passo: localizar uma perda de memória (JavaScript)](javascript-memory.md).

1. Abra o aplicativo no Visual Studio.

2. Executar o analisador de memória de JavaScript (veja as etapas anteriores).

3. Execute seu aplicativo com o cenário que deseja testar. Por exemplo, o cenário pode envolver uma grande mutação do DOM, quando uma determinada página estiver carregando ou quando o aplicativo for iniciado.

4. Repita o cenário mais algumas vezes (1 a 4 vezes).

   > [!TIP]
   > Ao repetir o cenário de teste várias vezes, você pode ajudar a garantir que o trabalho de inicialização seja descartado dos resultados.

5. Alterne para o Visual Studio (pressione a tecla **ALT** + ).

6. Obtenha um instantâneo do heap da linha de base escolhendo **Obter uma imagem instantânea do heap**.

    A ilustração a seguir mostra um exemplo de um instantâneo de linha de base.

    ![Instantâneo de linha de base](../profiling/media/js_mem_leak_workflow_baseline.png "JS_Mem_Leak_Workflow_Baseline")

   > [!TIP]
   > Para ter um controle mais preciso do intervalo entre os instantâneos, use o comando [Associar o código-fonte com os dados de uso de memória](#associate-source-code-with-memory-usage-data) no seu código.

7. Troque para o seu aplicativo e repita o cenário que você estava testando (repita apenas uma vez).

8. Alterne para o Visual Studio e obtenha um segundo instantâneo.

9. Troque para o seu aplicativo e repita o cenário que você estava testando (repita apenas uma vez).

10. Alterne para o Visual Studio e obtenha um terceiro instantâneo.

     A ilustração a seguir mostra um exemplo de um segundo e um terceiro instantâneos.

     ![Segundo e terceiro instantâneo](../profiling/media/js_mem_leak_workflow.png "JS_Mem_Leak_Workflow")

     Ao determinar uma linha de base, um segundo e um terceiro instantâneos neste fluxo de trabalho, você pode descartar com mais facilidade as alterações que não estiverem associadas aos vazamentos de memória. Por exemplo, pode haver alterações previstas, como a atualização de cabeçalhos e rodapés em uma página, que criarão algumas alterações no uso da memória, mas tais alterações podem não estar relacionadas aos vazamentos de memória.

11. No terceiro instantâneo, escolha um link para uma das exibições de comparação:

    - Tamanho de heap diferencial (link à esquerda, abaixo do tamanho do heap). Esse texto de link mostra a diferença entre o tamanho do heap do instantâneo atual e o tamanho do heap do instantâneo anterior.

    - Contagem de objetos diferencial (link à direita, abaixo da contagem de objetos). O texto do link mostra dois valores (por exemplo, +1858 / -1765). O primeiro valor representa o número de novos objetos adicionados desde o instantâneo anterior, ao passo que o segundo valor traz o número de objetos removidos desde o instantâneo anterior.

      Esses links abrem uma exibição de comparação dos detalhes do instantâneo dos tipos no heap, classificados pelo tamanho retido ou pela contagem de objetos, dependendo do link aberto.

12. Escolha uma das seguintes opções de filtro de **Escopo** para ajudar a identificar problemas de uso de memória:

    - **Objetos restantes do instantâneo nº 2**.

    - **Objetos adicionados entre os instantâneos nº 2 e nº 3**

    > [!TIP]
    > Use a exibição filtrada de objetos restantes desde o instantâneo anterior para investigar os vazamentos de memória. Por exemplo, se a contagem de objetos diferencial for de +205 / -195, essa exibição mostrará os 10 objetos restantes, os quais serão as prováveis explicações para os vazamentos de memória.

     A ilustração a seguir mostra uma exibição de comparação dos objetos restantes desde o instantâneo 2.

     ![Exibição de comparação de instantâneos mostrando tipos](../profiling/media/js_mem_snapshot_diff.png "JS_Mem_Snapshot_Diff")

     Na ilustração anterior, vemos que há dois objetos restantes desde o instantâneo anterior. Verifique se esse é o comportamento esperado para seu aplicativo. Caso não seja, isso pode indicar um vazamento de memória.

13. Para ver onde os objetos nas exibições de comparação estão vinculados ao objeto global, o que impede sua coleta como lixo, abra o menu de atalho de um objeto e escolha **Mostrar na exibição de raiz**. Um número maior de objetos pode ser retido na memória por serem referenciados por um único objeto (ou por poucos objetos) que seja vinculado ao objeto global.

14. Se houver muitos objetos na exibição de objetos restantes, tente isolar ainda mais o período no qual o vazamento de memória está ocorrendo e tire novamente mais três instantâneos. Para isolar ainda mais a perda de memória, use [Associar o código-fonte com os dados de uso de memória](#associate-source-code-with-memory-usage-data), [Associar o código-fonte com os dados de uso de memória](#associate-source-code-with-memory-usage-data) e outros dados de uso de memória disponíveis no analisador de memória.

## <a name="view-live-memory-usage-summary"></a>Exibir resumo do uso de memória em tempo real
 A exibição do resumo do uso de memória em tempo real fornece um gráfico de uso de memória para o aplicativo em execução e uma coleção de todos os quadros de resumo de instantâneos. Nesta exibição, você pode executar tarefas básicas como obter instantâneos, analisar informações resumidas e navegar para outros modos de exibição. Quando você parar a coleta de dados, o gráfico de memória desaparecerá e você verá apenas a exibição [Ver resumo de instantâneo](#view-a-snapshot-summary).

 O gráfico de memória mostra uma exibição em tempo real da memória do processo do aplicativo, que inclui bytes particulares, a memória nativa e o heap de JavaScript. O gráfico de memória é uma exibição rolável da memória do processo. Esta é a aparência dele:

 ![Grafo de memória do analisador de memória JavaScript](../profiling/media/js_mem_memory_graph.png "JS_Mem_Memory_Graph")

 Se você tiver adicionado marcas de usuário ao código do aplicativo (consulte [Associar o código-fonte com os dados de uso de memória](#associate-source-code-with-memory-usage-data)), um triângulo invertido aparecerá no gráfico de uso de memória para indicar quando essa seção de código for atingida.

 Parte da memória mostrada no gráfico é atribuída pelo runtime JavaScript. Não é possível controlar esse uso de memória do seu aplicativo. O uso de memória mostrado no gráfico aumenta quando você usa o primeiro instantâneo e, em seguida, aumenta em níveis mínimos para cada instantâneo adicional.

## <a name="view-a-snapshot-summary"></a>Exibir um resumo de instantâneo
 Para obter um instantâneo do estado atual do uso de memória do aplicativo, escolha **Obter uma imagem instantânea do heap** no gráfico de memória. Um quadro de resumo de instantâneo, que aparece no resumo do uso de memória em tempo real (quando o aplicativo está em execução) e o resumo de instantâneo (quando o aplicativo está parado), fornece informações sobre o heap de JavaScript e links para informações mais detalhadas. Se você obtiver dois ou mais instantâneos, um instantâneo fornecerá informações adicionais que comparam seus dados aos dados do instantâneo anterior.

> [!NOTE]
> O analisador de memória de JavaScript força uma coleta de lixo antes de cada instantâneo. Isso ajuda a garantir mais resultados consistentes entre as execuções.

 Este é um exemplo de resumo de instantâneo quando se obtém vários instantâneos.

 ![Resumo do instantâneo](../profiling/media/js_mem_snapshot_summary.png "JS_Mem_Snapshot_Summary")

 O resumo de instantâneo inclui:

- Título do instantâneo e o carimbo de data/hora.

- Número de problemas em potencial (marcado por um ícone azul de informações). Esse número, se presente, identifica possíveis problemas de memória, como os nós que não estão anexados ao DOM. A contagem é vinculada à exibição Tipos do instantâneo, que é classificada pelo tipo de problema para realçar os possíveis problemas. Uma dica de ferramenta mostra a descrição do problema.

- Tamanho do heap. Esse número inclui elementos DOM e objetos que o mecanismo de runtime JavaScript adiciona ao heap de JavaScript. O tamanho do heap é vinculado à exibição Tipos do instantâneo.

- Tamanho diferencial do heap. Esse valor mostra a diferença entre o tamanho do heap do instantâneo atual e o tamanho do heap do instantâneo anterior. O valor é seguido por uma seta para cima vermelha se houver um aumento de memória ou uma seta para baixo verde se houver uma redução de memória. Se o tamanho do heap não tiver sido alterado entre instantâneos, você verá o texto **Sem alteração** em vez de um número. Para o primeiro instantâneo, você verá o texto **Linha de base**. O tamanho diferencial do heap está vinculado à exibição Tipos do diferencial de instantâneo.

- Contagem de objeto. Essa contagem mostra apenas objetos criados no seu aplicativo e filtra os objetos internos criados no runtime JavaScript. A contagem de objeto é vinculada à exibição Tipos dos detalhes do instantâneo.

- Contagem diferencial de objeto. Isso mostra dois valores: o primeiro valor é o número de novos objetos adicionados desde o instantâneo anterior, e o segundo valor é o número de objetos removidos desde o instantâneo anterior. Por exemplo, a ilustração mostra que 1.859 objetos foram adicionados e 1.733 objetos foram removidos do Instantâneo 1. Essas informações serão acompanhadas de uma seta para cima vermelha se o número de objetos aumentar, ou de uma seta para baixo verde se o número diminuir. Se a contagem de objetos não for alterada, você verá o texto **Sem alteração** em vez de um número. Para o primeiro instantâneo, você verá o texto **Linha de base**. A contagem diferencial de objeto é vinculada à exibição Tipos da diferença do instantâneo.

- Captura da tela no momento em que o instantâneo é obtido.

## <a name="view-snapshot-details"></a>Exibir detalhes do instantâneo
 Você pode exibir informações detalhadas sobre o uso de memória para cada instantâneo nas exibições detalhadas de instantâneo.

 Na exibição de resumo de instantâneo, escolha um link para ver os detalhes do instantâneo. Por exemplo, o link de tamanho do heap abre detalhes do instantâneo com a exibição Tipos aberta por padrão.

 Esta ilustração mostra a exibição Tipos, em um detalhe do instantâneo, com os dados de uso da memória classificados por tamanho retido.

 ![Exibição de detalhes do instantâneo mostrando possíveis problemas](../profiling/media/js_mem_snapshot_details.png "JS_Mem_Snapshot_Details")

 Na exibição de detalhes de instantâneo, você pode examinar os dados de uso de memória por dominador, tipo ou raiz, escolhendo uma opção da barra de ferramentas:

- **Tipos**. Mostra a contagem de instâncias e o tamanho total de objetos no heap, agrupados pelo tipo de objeto. Por padrão, eles são classificados pela contagem de instância.

  > [!TIP]
  > Normalmente, exibições de comparação dos tipos no heap do objeto são as exibições mais úteis para identificar uma perda de memória, pois oferecem um filtro de **Escopo** para ajudar a identificar objetos restantes.

- **Raízes**. Mostra uma exibição hierárquica de objetos desde objetos raiz até referências de filhos. Por padrão, os nós filho são classificados pela coluna de tamanho retido, com o maior na parte superior.

- **Dominadores**. Mostra uma lista de objetos do heap que têm referências exclusivas a outros objetos. Os dominadores são classificados pelo tamanho retido.

  > [!TIP]
  > Quando você remove um dominador da memória, recupera toda a memória que o objeto retém. Para alguns aplicativos, a exibição Dominadores pode ajudar a esclarecer os tamanhos de memória retida, visto que é possível analisar toda a cadeia de referência do objeto.

  Todas as três exibições mostram os tipos de valores semelhantes, incluindo:

- **Identificador (es)**. Nome que melhor identifica o objeto. Por exemplo, para elementos HTML, os detalhes do instantâneo mostram o valor do atributo ID, se um for usado.

- **Type**. Tipo de objeto (por exemplo, elemento de link HTML ou elemento div).

- **Tamanho**. Tamanho do objeto, não incluindo o tamanho de nenhum objeto referenciado.

- **Tamanho retido**. Tamanho do objeto mais o tamanho de todos os objetos filho que não têm outro pai. Para fins práticos, essa é a quantidade de memória retida pelo objeto, então, se você excluir o objeto, recuperará a quantidade de memória especificada.

- **Contagem**. Número de instâncias de objeto. Esse valor aparece apenas na exibição Tipos.

## <a name="view-a-snapshot-diff"></a>Exibir a diferença de um instantâneo
 No analisador de memória de JavaScript, você pode comparar um instantâneo com o instantâneo anterior nas exibições diferenciais.

 Na exibição resumida de instantâneo, você pode exibir os detalhes diferenciais escolhendo os links de tamanho de heap ou de número de objetos diferenciais após a obtenção de dois ou mais instantâneos.

 Você pode exibir informações diferenciais sobre dominadores, tipos e raízes. O diferencial de instantâneo mostra todos os objetos que foram adicionados ao heap entre os dois instantâneos.

 Esta ilustração mostra a exibição Tipos em uma diferença de instantâneo.

 ![Exibição de comparação de instantâneos mostrando tipos](../profiling/media/js_mem_snapshot_diff.png "JS_Mem_Snapshot_Diff")

 Na janela de comparação de instantâneos, as exibições de Dominadores, Tipos e Raízes são as mesmas que na janela [Exibir detalhes do instantâneo](#view-snapshot-details). A diferença de instantâneo mostra as mesmas informações dos detalhes do instantâneo, com estes valores adicionais:

- **Diferença de tamanho**. Diferença entre o tamanho do objeto no instantâneo atual e seu tamanho no instantâneo anterior, não incluindo o tamanho de nenhum objeto referenciado.

- **Diferença de tamanho retido**. Diferença entre o tamanho retido do objeto no instantâneo atual e seu tamanho retido no instantâneo anterior. O tamanho retido inclui o tamanho do objeto mais o tamanho dos objetos filho que não têm outro pai. Para fins práticos, o tamanho retido é a quantidade de memória retida pelo objeto, então, se você excluir o objeto, recuperará a quantidade de memória especificada.

  Para filtrar informações de comparação entre os instantâneos, escolha um dos filtros de **Escopo** na parte superior das exibições de comparação.

- **Objetos restantes do instantâneo # \<number>**. Esse filtro mostra o diferencial entre os objetos adicionados ao heap e removidos do heap em comparação com o instantâneo de linha de base e o instantâneo anterior. Por exemplo, se o resumo de instantâneo mostrar +205 / -195 na contagem de objetos, esse filtro mostrará a você os 10 objetos que foram adicionados, mas não removidos.

  > [!TIP]
  > Para mostrar as informações mais úteis nesse filtro, siga as etapas descritas em [Isolar uma perda de memória](#isolate-a-memory-leak).

- **Objetos adicionados entre o instantâneo # \<number> e \<number> #**. Esse filtro mostra todos os objetos adicionados ao heap desde o instantâneo anterior.

- **Todos os objetos no instantâneo \<number> #**. Essa configuração de filtro não descarta objetos no heap.

  Para mostrar referências de objeto que não correspondem ao filtro de **escopo** atual, selecione **Mostrar referências não correspondentes** nas configurações da lista de configurações ![drop&#45;lista suspensa no analisador de memória](../profiling/media/js_mem_settings.png "JS_Mem_Settings") no canto superior direito do painel. Se habilitar esta configuração, as referências não coincidentes são exibidas em cinza.

> [!TIP]
> Recomendamos que você siga as etapas em [Isolar uma perda de memória](#isolate-a-memory-leak) e use os objetos que sobraram do filtro de **Escopo** para ajudar a identificar os objetos com perda de memória.

## <a name="view-objects-by-dominator"></a>Exibir objetos por dominador
 Nas exibições Tipos e Dominadores, você pode optar por exibir os objetos classificados pelos dominadores (esta é a exibição padrão na guia **Dominadores**). Ao selecionar esta exibição, somente os dominadores são mostrados na exibição superior dos objetos. (Objetos que são descendentes de objetos não globais são ocultados da exibição de nível superior.) Para alguns aplicativos, isso pode esclarecer quais objetos estão causando um vazamento de memória, reduzindo o ruído nos dados.

 Para alternar a exibição de objetos por dominador, pressione o botão **Dobrar objetos pelo dominador**. ![Dobrando objetos em seus dominadores](../profiling/media/js_mem_fold_objects.png "JS_Mem_Fold_Objects")

 Para obter mais informações sobre dominadores, consulte [Exibir detalhes do instantâneo](#view-snapshot-details).

## <a name="filter-data-by-identifier"></a>Filtrar dados por identificador
 Nas exibições Dominadores e Tipos, você pode filtrar dados procurando por identificadores específicos. Para pesquisar por um identificador, basta digitar seu nome na caixa de texto **Filtro de identificador**, no canto superior direito. Quando você começar a digitar, os identificadores que não contiverem os caracteres digitados serão removidos.

 Cada exibição tem seu próprio filtro. Portanto, o filtro não é preservado quando você alterna para outra exibição.

## <a name="find-an-object-in-the-object-tree"></a>Localizar um objeto na árvore de objetos
 Nas exibições Dominadores e Tipos, você pode ver a relação entre um objeto específico e o objeto `Global`. Objetos vinculados ao `Global` não serão coletados como lixo. Você pode localizar facilmente um objeto conhecido na exibição Raízes sem pesquisar a árvore de objeto `Global`. Para isso, abra o menu de atalho de um objeto na exibição Dominadores ou Tipo e escolha **Mostrar na exibição de raiz**.

## <a name="view-shared-object-references"></a>Exibir referências de objeto compartilhadas
 Nas exibições Dominadores e Tipos, o painel inferior contém uma lista Referências de objeto que exibe referências compartilhadas. Quando você escolhe um objeto no painel superior, a lista Referências de objeto exibe todos os objetos que apontam para o objeto.

> [!NOTE]
> Referências circulares são exibidas com um (*) asterisco e uma dica de ferramenta informativa e não podem ser expandidas. Do contrário, elas impediriam que você percorra a árvore de referências e identifique objetos que estão retendo memória.

 Se você quiser obter ajuda adicional para identificar objetos equivalentes, escolha **Exibir IDs de objeto** nas configurações listar ![configurações drop&#45;lista suspensa no analisador de memória](../profiling/media/js_mem_settings.png "JS_Mem_Settings") no canto superior direito do painel superior. Essa opção exibe IDs de objetos ao lado dos nomes dos objetos na lista **Identificador(es)** (as IDs aparecem em todas as exibições, não apenas na lista de Referências de objeto). Os objetos que têm a mesma ID são referências compartilhadas.

 A ilustração a seguir mostra a lista Referências de objeto para um item selecionado com as IDs exibidas.

 ![Referências de objeto com IDs exibidas](../profiling/media/js_mem_shared_refs.png "JS_Mem_Shared_Refs")

## <a name="show-built-in-objects"></a>Mostrar objetos internos
 Por padrão, as exibições Dominadores e Tipos mostram apenas a objetos criados em seu aplicativo. Isso ajuda a filtrar informações desnecessárias e isolar problemas relacionados ao aplicativo. No entanto, às vezes pode ser útil exibir todos os objetos gerados pelo runtime JavaScript para o aplicativo.

 Para exibir esses objetos, escolha **Mostrar incorporados** na lista configurações&#45;lista ![de configurações, menu para baixo no analisador de memória](../profiling/media/js_mem_settings.png "JS_Mem_Settings") no canto superior direito do painel.

## <a name="save-diagnostic-session-files"></a>Salvar arquivos de sessão de diagnóstico
 Os resumos de instantâneo de diagnóstico e as exibições detalhadas associadas são salvos como arquivos .*diagsession*. O **Gerenciador de Soluções** exibe sessões de diagnóstico anteriores na pasta Sessões de Diagnóstico. No **Gerenciador de Soluções**, você pode abrir sessões anteriores ou remover ou renomear arquivos.

## <a name="associate-source-code-with-memory-usage-data"></a>Associar o código-fonte com dados de uso de memória
 Para ajudar a isolar a seção de código que tem um problema de memória, use os seguintes métodos:

- Procure nomes de classes e IDs para elementos DOM nas exibições de detalhes e diferenciais.

- Procure valores de cadeia de caracteres nas exibições de detalhes e diferenciais que possam estar associados ao seu código-fonte.

- Use o comando [Localizar um objeto na árvore de objetos](#find-an-object-in-the-object-tree) para percorrer a árvore de objetos. Isso pode ajudá-lo a identificar o código-fonte associado.

- Adicione comandos do analisador de memória ao código-fonte.

  Você poderá usar os seguintes comandos em seu código-fonte:

- `console.takeHeapSnapshot` obtém um instantâneo de heap que aparece no analisador de memória de JavaScript. Esse comando é um dos [Comandos do Console JavaScript](../debugger/javascript-console-commands.md).

- `performance.mark` define uma marca de usuário (o triângulo invertido) que aparece na linha de tempo do gráfico de memória na exibição resumida durante a execução do aplicativo. Esse comando usa um argumento de cadeia de caracteres que descreve o evento e aparece como uma dica de ferramenta no gráfico de memória. Essa descrição não deve exceder 100 caracteres.

> [!TIP]
> Use `console.takeHeapSnapshot` para acelerar a análise ao repetir cenários de uso de memória.

 Esses comandos geram uma exceção se você os adiciona ao aplicativo e o executa fora do analisador de memória de JavaScript. No entanto, você pode testar se os comandos existem antes de usá-los. (Os comandos não existem no início da fase de inicialização da sessão.) Para verificar se você pode chamar com segurança `takeHeapSnapshot` , use este código:

```javascript
if (console && console.takeHeapSnapshot) {
    console.takeHeapSnapshot();
}
```

 Para verificar se você pode chamar `performance.mark` com segurança, use este código:

```javascript
if (performance && performance.mark) {
    performance.mark("message_string");
}

```

 Este é um gráfico de memória com várias marcas de usuário e a dica de ferramenta para a marca de usuário atualmente selecionada, para qual o parâmetro de cadeia de caracteres `performance.mark` é definido como “dados gerados”:

 ![Usando uma marca de perfil](../profiling/media/js_mem_performance_marks.png "JS_Mem_Performance_Marks")

## <a name="tips-to-identify-memory-issues"></a>Dicas para identificar problemas de memória

- Siga o fluxo de trabalho descrito em [isolar uma perda de memória](#isolate-a-memory-leak) e use os **objetos restantes \<number> do filtro instantâneo #** em uma exibição de comparação para identificar prováveis candidatos a vazamentos de memória.

- Use [Localizar um objeto na árvore de objetos](#find-an-object-in-the-object-tree) para ver onde um objeto é referenciado na hierarquia da memória. A exibição Raiz mostra como um objeto é vinculado ao objeto global, o que o impediria de ser coletado como lixo.

- Quando a causa de um problema de memória for difícil de identificar, use as diversas exibições (como Dominadores e Tipos) para buscar aspectos em comum, especialmente para ajudar a identificar um objeto (ou alguns objetos) que possam conter referências a muitos dos outros objetos que aparecem na exibição.

- Procurar os objetos retidos acidentalmente na memória depois que o usuário navegar para uma nova página, que é uma causa comum de problemas de memória. Por exemplo:

  - o uso incorreto da função [URL.CreateObjectUrl](https://developer.mozilla.org/docs/Web/API/URL/createObjectURL) pode causar esse problema.

  - Alguns objetos podem oferecer um método `dispose` e recomendações para o uso. Por exemplo, você deve chamar `dispose` em uma [WinJS.Binding.List](/previous-versions/windows/apps/hh700774\(v\=win.10\)) caso chame o método `createFiltered` da lista e, depois, navegue para outra página.

  - Você pode precisar remover um ou mais ouvintes de eventos. Para obter mais informações, consulte [Exibir ouvintes de eventos DOM](../debugger/quickstart-debug-html-and-css.md).

- Assista à última parte [deste vídeo](https://channel9.msdn.com/Events/Build/2013/3-316) da conferência Build 2013 sobre o analisador de memória de JavaScript.

- Leia [Gerenciar memória em aplicativos UWP](/archive/msdn-magazine/2012/windows-8-special-issue/javascript-managing-memory-in-windows-store-apps).

- Considere temporariamente modificar o código para isolar problemas. Por exemplo, você pode querer:

  - Usar os comandos para o Memory Analyzer, `console.takeSnapshot` e `performance.mark`. (Consulte [Associar o código-fonte com os dados de uso de memória](#associate-source-code-with-memory-usage-data).)

    É possível usar esses comandos como auxílio para isolar os problemas que você não pode isolar manualmente obtendo um instantâneo de heap.

  - Crie um objeto de teste e controle-o nas exibições do analisador de memória do JavaScript, por exemplo, na exibição Tipos. Por exemplo, você pode anexar um objeto muito grande a outro objeto para ver se um objeto ou um elemento específico foi coletado como lixo.