---
title: Gerenciar os resultados do teste de carga
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, results repository
- results, load test
- load test results, repository
- Load Test Results Repository
ms.assetid: 1cd63c4b-4f74-4133-b675-5e8fbeab25f3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9945551469541cdcffe520844da600d758dc43b5
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286759"
---
# <a name="manage-load-test-results-in-the-load-test-results-repository"></a>Gerenciar resultados do teste de carga no repositório de Resultados do Teste de Carga

Quando você executa seus testes de carga, todas as informações obtidas durante uma execução de teste de carga podem ser armazenadas no *Repositório de Resultados de Teste de Carga*, que é um banco de dados SQL. O Repositório de Resultados de Teste de Carga contém dados do contador de desempenho e todas as informações sobre erros gravados. O banco de dados Repositório de Resultados é criado pela configuração para controladores ou criada automaticamente na primeira execução local de um teste de carga. Para uma execução local, o banco de dados será criado automaticamente se o esquema de teste de carga não estiver presente.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Se você modificar a cadeia de conexão do repositório de resultados do controlador para usar outro servidor, o novo servidor precisará executar o script *loadtestresultsrepository.sql* para criar o esquema.

O Visual Studio Enterprise fornece conjuntos de contadores nomeados que coletam contadores de desempenho comuns baseados em uma tecnologia. Esses conjuntos são úteis quando você está analisando um servidor IIS, um servidor ASP.NET ou um servidor SQL. Todos os dados coletados com conjuntos de contadores são armazenados no Repositório de Resultados do Teste de Carga.

> [!IMPORTANT]
> Há uma diferença entre um conjunto de contadores e os dados do contador de desempenho. Um conjunto de contadores é metadados. Ele define um grupo de contadores de desempenho que devem ser coletados de um computador que esteja executando uma função específica como, por exemplo, o IIS ou o SQL Server. O contador faz parte da definição do teste de carga. Os dados do contador de desempenho são coletados com base nos conjuntos de contadores, no mapeamento do conjunto de contadores para um computador específico e na taxa de amostragem.

## <a name="sql-server-versions"></a>Versões do SQL Server

Para usar testes de carga, você pode usar o LocalDB do SQL Server Express, que é instalado com o Visual Studio. Ele é o servidor de banco de dados padrão para testes de carga (inclusive para a integração do Microsoft Excel). SQL Server Express LocalDB é um modo de execução do SQL Server Express destinado a desenvolvedores de programas. A instalação do SQL Server Express LocalDB copia um conjunto mínimo de arquivos necessários para iniciar o Mecanismo de Banco de Dados do SQL Server.

Se sua equipe espera ter demandas intensas do banco de dados ou se seus projetos excedem o LocalDB do SQL Server Express, considere a atualização para o SQL Express ou para o SQL Server completo para conseguir um potencial maior de dimensionamento. Se você atualizar o SQL Server, os arquivos MDF e LDF do LocalDB do SQL Server Express serão armazenados na pasta de perfil do usuário. Esses arquivos podem ser usados para importar o banco de dados de teste de carga para o SQL Server Express ou o SQL Server.

## <a name="load-test-results-store-considerations"></a>Considerações sobre o repositório de resultados do teste de carga

Quando o Visual Studio Enterprise é instalado, o repositório de resultados de teste de carga é configurado para usar uma instância do SQL Express instalada no computador. O SQL Express está limitado a usar no máximo 4 GB de espaço em disco. Se for executar muitos testes de carga por um longo período, você deverá considerar a configuração do armazenamento de resultados de teste de carga para usar uma instância do produto SQL Server completo, se disponível.

## <a name="load-test-analyzer-tasks"></a>Tarefas do Analisador de Teste de Carga

|Tarefas|Tópicos associados|
|-|-----------------------|
|**Configurar um repositório de resultados de teste de carga:** você pode configurar um repositório de resultados de teste de carga em um banco de dados SQL. **Observação:** um repositório de teste de carga também pode ser criado durante a instalação de um controlador de teste. Para obter mais informações, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).||
|**Selecionando e exibindo um repositório de resultados:** é possível selecionar um repositório de resultados específico. Você não está limitado a um repositório de resultados local. Geralmente, os testes de carga são executados em um conjunto remoto de computadores de agente. Os resultados do teste de seus agentes ou do seu computador local podem ser salvos em qualquer servidor SQL no qual você criou um repositório de resultados de testes de carga. Em ambos os casos, você deve identificar onde armazenar os resultados do teste de carga usando a janela **Administrar controladores de teste**.|-   [Como: selecionar um repositório de resultados de teste de carga](../test/how-to-select-a-load-test-results-repository.md)<br />-   [Como acessar os resultados do teste de carga para análise](../test/how-to-access-load-test-results-for-analysis.md)|
|**Excluindo um resultado do teste de carga do repositório:** você pode remover um resultado do teste de carga do **Editor de Teste de Carga** usando a caixa de diálogo **Abrir e Gerenciar Resultados de Testes de Carga**.|-   [Como excluir resultados de teste de carga de um repositório](../test/how-to-delete-load-test-results-from-a-repository.md)|
|**Importar e exportar resultados em um repositório:** é possível importar e exportar resultados de teste de carga do **Editor de Teste de Carga**.|-   [Como importar resultados de teste de carga para um repositório](../test/how-to-import-load-test-results-into-a-repository.md)<br />-   [Como: exportar resultados de teste de carga de um repositório](../test/how-to-export-load-test-results-from-a-repository.md)|

## <a name="related-tasks"></a>Tarefas relacionadas

[Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)

Você pode exibir os resultados de um teste de carga em execução e um teste de carga concluído usando o **Analisador de Teste de Carga**.

## <a name="see-also"></a>Veja também

- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [Como acessar os resultados do teste de carga para análise](../test/how-to-access-load-test-results-for-analysis.md)
