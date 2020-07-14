---
title: Criar relatórios de desempenho de teste de carga usando o Microsoft Excel
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, creating Excel reports
- load tests, reporting
ms.assetid: b87fb196-9973-4512-a924-088788def4ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a94a44d0a826cbda1d50b212f61bef86ad29f05c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287812"
---
# <a name="how-to-create-load-test-performance-reports-using-microsoft-excel"></a>Como criar relatórios de desempenho de teste de carga usando o Microsoft Excel

Você pode gerar relatórios de teste de carga do Microsoft Excel baseados em dois ou mais resultados de teste.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Dois tipos de relatórios de teste de carga estão disponíveis:

- **Executar comparação** Isso cria um conjunto de relatórios que compara os dados de dois resultados de testes de carga usando tabelas e gráficos de barras.

- **Tendência** Você pode gerar a análise de tendência em dois ou mais resultados de testes de carga. Os resultados são exibidos usando gráficos de linhas, mas os dados estão disponíveis em tabelas dinâmicas.

> [!TIP]
> Você também pode criar manualmente relatórios do Microsoft Word, copiando e colando dados da exibição de resumo, gráficos e tabelas. Confira [Como criar manualmente um relatório de desempenho de teste de carga usando o Microsoft Word](../test/how-to-manually-create-a-load-test-performance-report-using-microsoft-word.md).

Qualquer relatório pode ser usado para compartilhar dados de desempenho com participantes e informar se o desempenho e a integridade gerais do sistema estão melhorando ou piorando.

As definições de relatório são armazenadas no banco de dados de teste de carga. Quando um relatório é salvo, a definição do relatório é salva no banco de dados e poderá ser reutilizada posteriormente.

Além disso, a pasta de trabalho do Excel pode ser compartilhada com participantes de modo que os participantes não precisem se conectar ao banco de dados para ver o relatório.

> [!NOTE]
> Você pode compartilhar a pasta de trabalho do Excel. No entanto, somente os usuários que têm o Visual Studio instalado no computador poderão alterar as planilhas. Outros usuários não verão a opção **Relatório do Teste de Carga** na faixa de opções do **Office**, mas poderão exibir a pasta de trabalho.

A ilustração a seguir é um exemplo de um relatório que mostra uma correlação entre uma redução na velocidade de transação (Atualizar Carrinho) e a degeneração do contador (% do Processador). Isso aponta para um possível problema no código do aplicativo, em vez do banco de dados ou da rede, e é um candidato adequado para diagnosticar usando o Criador de Perfis do ASP.NET.

![Possível problema no código do aplicativo](../test/media/lt_excel.png)

Os relatórios do Excel podem ser gerados no **Analisador de Teste de Carga**, usando o botão **Criar Relatório do Excel** na barra de ferramentas ou no Excel usando a opção **Relatório do Teste de Carga** na guia de **Teste de Carga** da faixa de opções do **Office**.

> [!NOTE]
> Se você adicionar comentários a um teste de carga, eles aparecerão no relatório do Excel.

## <a name="to-generate-load-test-comparison-reports-using-excel"></a>Para gerar relatórios de comparação de teste de carga usando o Excel

1. Antes de gerenciar um relatório, é necessário executar primeiro um teste de carga.

2. Você pode criar relatórios de teste de carga do Excel em duas maneiras:

   - Após você concluir um teste de carga, na página de **Resultados de testes de carga**, clique no botão **Criar relatório no Excel** na barra de ferramentas.

      > [!NOTE]
      > Se o botão **Criar Relatório no Excel** estiver desabilitado na barra de ferramentas **Visualizador de Resultados do Teste de Desempenho Web**, talvez seja necessário executar o Microsoft Excel uma vez antes que ele seja habilitado. Quando o Visual Studio Enterprise é instalado, o suplemento ao teste de carga do Visual Studio Enterprise é copiado para o computador para o Microsoft Excel. No entanto, o Microsoft Excel deve ser executado para concluir o processo de instalação do suplemento.

      O Microsoft Excel é aberto com o **Assistente para Gerar um relatório de teste de carga**.

   **OR**

   1. Abra o Microsoft Excel, selecione a guia **Teste de Carga** na faixa de opções do **Office** e, em seguida, escolha **Relatório de Teste de Carga**.

       O **Assistente para Gerar um relatório de teste de carga** é exibido.

   2. Na página **Selecione o banco de dados que contém os resultados do teste de carga**, em **Nome do servidor**, digite o nome do servidor que contém os resultados de teste de carga.

   3. Na lista suspensa **Nome do banco de dados**, selecione o banco de dados que contém os resultados de teste de carga.

3. Na página **Como você deseja gerar seu relatório**, verifique se **Criar um relatório** está selecionado e escolha **Avançar**.

4. Na página **Que tipo de relatório você deseja gerar**, verifique se **Comparação de Execuções** está selecionado e escolha **Avançar**.

5. Na página **Insira os detalhes do relatório de teste de carga**, digite um nome para o relatório em **Nome do Relatório**.

6. Selecione o teste de carga para o qual você deseja gerar o relatório e escolha **Avançar**.

7. Na página **Selecione as execuções para seu relatório**, em **Selecionar uma ou mais execuções para adicionar ao relatório**, selecione os dois resultados de teste de carga que você deseja comparar no relatório e escolha **Avançar**.

   > [!NOTE]
   > Você só pode gerar um relatório de comparação em dois resultados de teste de carga. Se você selecionar ou um resultado de teste de carga ou mais de dois resultados de teste de carga, será exibida uma mensagem de aviso.

8. Na página **selecionar os contadores para o relatório** , em **selecionar um ou mais contadores para adicionar ao relatório** , uma lista expansível de contadores está disponível para personalizar o relatório. Selecione os contadores que deseja comparar nas duas execuções de teste selecionadas no relatório e escolha **Concluir**.

9. O relatório de pasta de trabalho do Excel é gerado com as seguintes guias da planilha:

   - **Sumário** – exibe o nome do relatório de teste de carga e fornece um sumário com links para as várias guias no relatório.

   - **Execuções –** fornece detalhes sobre quais são as duas execuções que estão sendo comparadas no relatório.

   - **Comparação de Testes –** fornece detalhes do gráfico de barras em regressões de desempenho e aprimoramentos entre as duas execuções que estão sendo comparadas.

   - **Comparação de Páginas –** fornece dados de comparação de desempenho em percentual e em gráfico de barra entre as duas execuções nas várias páginas das execuções de teste.

   - **Comparação de Computadores –** fornece dados de comparação entre as duas execuções com base nos computadores usados.

   - **Comparação de Erros –** compara os tipos de erro encontrados entre as duas execuções e o número de ocorrências.

     > [!TIP]
     > Para obter relatórios melhores, várias propriedades estão disponíveis em testes de carga e testes de desempenho na Web que permitem a geração de relatórios mais ricos. A solicitação de página tem duas propriedades que são apresentadas nos relatórios: Meta e Nome de Relatório. Os tempos de resposta da página serão relatados em relação à meta, e o nome de relatório será usado no lugar da URL nos relatórios. Em Configurações de Execução de teste de carga, em Gerenciar Conjuntos de Contadores, a propriedade Marcas de Computador é apresentada nos nomes de computador do relatório. Isso é muito útil para descrever a função de um computador específico no relatório.

## <a name="to-generate-load-test-trend-reports-using-excel"></a>Para gerar relatórios de tendência de teste de carga usando o Excel

1. Antes de gerenciar um relatório, é necessário executar um teste de carga.

2. Você pode criar relatórios de teste de carga do Excel em duas maneiras:

   - Após você concluir um teste de carga, na página de **Resultados de testes de carga**, clique no botão **Criar relatório no Excel** na barra de ferramentas.

      > [!NOTE]
      > Se o botão **Criar Relatório no Excel** estiver desabilitado na barra de ferramentas **Visualizador de Resultados do Teste de Desempenho Web**, talvez seja necessário executar o Microsoft Excel uma vez antes que ele seja habilitado. Quando o Visual Studio Enterprise é instalado, o suplemento ao teste de carga do Visual Studio Enterprise é copiado para o computador para o Microsoft Excel. No entanto, o Microsoft Excel deve ser executado para concluir o processo de instalação do suplemento.

      O Microsoft Excel é aberto com o **Assistente para Gerar um relatório de teste de carga**.

   **OR**

   1. Abra o Microsoft Excel, selecione a guia **Teste de Carga** na faixa de opções do **Office** e, em seguida, escolha **Relatório de Teste de Carga**.

       O **Assistente para Gerar um relatório de teste de carga** é exibido.

   2. Na página **Selecione o banco de dados que contém os resultados do teste de carga**, em **Nome do servidor**, digite o nome do servidor que contém os resultados de teste de carga.

   3. Na lista suspensa **Nome do banco de dados**, selecione o banco de dados que contém os resultados de teste de carga.

3. Na página **Como você deseja gerar seu relatório**, verifique se **Criar um relatório** está selecionado e escolha **Avançar**.

4. Na página **Que tipo de relatório você deseja gerar**, verifique se **Tendência** está selecionado e escolha **Avançar**.

5. Na página **Insira os detalhes do relatório de teste de carga**, digite um nome para o relatório em **Nome do Relatório**.

6. Selecione o teste de carga para o qual você deseja gerar o relatório e escolha **Avançar**.

7. Na página **Selecione as execuções para seu relatório**, em **Selecionar uma ou mais execuções para adicionar ao relatório**, selecione os resultados de teste de carga que você deseja comparar no relatório e escolha **Avançar**.

8. Na página **Selecionar os contadores para o relatório**, em **Selecione ou mais sobre contadores para adicionar ao relatório**, uma lista expansível de contadores estará disponível para personalizar o relatório. Selecione os contadores que você deseja comparar para análise de tendências e escolha **Concluir**.

9. O relatório é gerado com um sumário que possui links para várias guias de pasta de trabalho do Excel geradas no relatório. Os links são baseados nos contadores selecionados para o relatório de tendências. Por exemplo, se você deixou os contadores padrão selecionados na etapa 7, então o relatório irá gerar dados apresentados em guias separadas no Excel para cada contador listado na etapa 7. Os dados que são gerados para cada contador são apresentados em gráficos de tendências.

   > [!TIP]
   > Para obter relatórios melhores, várias propriedades estão disponíveis em testes de carga e testes de desempenho na Web que permitem a geração de relatórios mais ricos. A solicitação de página tem duas propriedades que são apresentadas nos relatórios: Meta e Nome de Relatório. Os tempos de resposta da página serão relatados em relação à meta, e o nome de relatório será usado no lugar da URL nos relatórios. Em Configurações de Execução de teste de carga, em Gerenciar Conjuntos de Contadores, a propriedade Marcas de Computador é apresentada nos nomes de computador do relatório. Isso é muito útil para descrever a função de um computador específico no relatório.

## <a name="net-security"></a>Segurança do .NET

Os resultados de teste de carga e os relatórios contêm possivelmente informações sigilosas que podem ser usadas para criar um ataque no seu computador ou sua rede. Os resultados de teste de carga e os relatórios contêm nomes de computadores e cadeias de conexão. Você deve estar ciente disso quando compartilhar relatórios de teste de carga com outras pessoas.

## <a name="see-also"></a>Veja também

- [Relatar resultados do teste de carga para comparações de testes ou análise de tendências](../test/compare-load-test-results.md)
