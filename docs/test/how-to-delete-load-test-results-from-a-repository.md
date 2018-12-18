---
title: Como excluir resultados do teste de carga de um repositório no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- results, load test
- load tests, deleting results
- load test results, removing
- Load Test Results Repository
- load tests, removing results
- load test results, deleting
ms.assetid: c2afe36b-d061-4f0e-9580-c18569ec08f9
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: b76e9b79e32ce8c7adf3fb9082e21f25406f7a28
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895412"
---
# <a name="how-to-delete-load-test-results-from-a-repository"></a>Como excluir resultados do teste de carga de um repositório

Quando você executar um teste de carga, as informações que foram coletadas durante a execução serão armazenadas no Repositório de Resultados do Teste de Carga. O Repositório de Resultados de Testes de Carga contém dados do contador de desempenho e informações sobre todos os erros. Para obter mais informações, confira [Gerenciar resultados do teste de carga no repositório de resultados do teste de carga](../test/manage-load-test-results-in-the-load-test-results-repository.md).

É possível gerenciar resultados do teste de carga no Editor de Teste de Carga usando a caixa de diálogo **Abrir e gerenciar resultados de testes de carga**. É possível abrir, importar, exportar e remover resultados de testes de carga.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-delete-results-from-a-repository"></a>Para excluir resultados de um repositório

1.  De um projeto de teste de carga e de desempenho na Web, abra um teste de carga.

2.  Na barra de ferramentas inserida, escolha **Abrir e gerenciar resultados**.

     A caixa de diálogo **Abrir e gerenciar resultados de testes de carga** é exibida.

3.  Em **Digite um nome de controlador para encontrar resultados de testes de carga**, selecione um controlador. Selecione **\<Local – Nenhum controlador>** para acessar os resultados armazenados localmente.

4.  Em **Exibir resultados para o seguinte teste de carga**, selecione o teste de carga cujos resultados deseja exibir. Selecione **\<Mostrar resultados para todos os testes>** para ver todos os resultados de todos os testes.

     Se resultados de testes de carga estiverem disponíveis, eles aparecerão na lista **Resultados de testes de carga**. As colunas são **Hora**, **Duração**, **Usuário**, **Resultado**, **Teste** e **Descrição**. **Teste** contém o nome do teste e **Descrição** contém a descrição opcional adicionada antes da execução do teste. A coluna **Descrição** exibe as descrições resumidas inseridas nos **Comentários de Análise** para esse resultado do teste.

5.  Na lista **Resultados de testes de carga**, escolha um resultado. Use a tecla **Shift**, a tecla **Ctrl** ou ambas para selecionar mais de um resultado.

6.  Escolha **Remover**.

     Os resultados são removidos do repositório.

    > [!NOTE]
    > A caixa de diálogo **Abrir e gerenciar resultados de testes de carga** permanece aberta após os resultados serem removidos.

## <a name="see-also"></a>Consulte também

- [Como exportar resultados do teste de carga de um repositório](../test/how-to-export-load-test-results-from-a-repository.md)
- [Gerenciar resultados do teste de carga no repositório de Resultados do Teste de Carga](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [Como importar resultados do teste de carga para um repositório](../test/how-to-import-load-test-results-into-a-repository.md)