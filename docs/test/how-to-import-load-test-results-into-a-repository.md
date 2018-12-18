---
title: Como importar resultados de teste de carga para um repositório no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- results, load test
- load test results, importing
- Load Test Results Repository
- load tests, importing results
ms.assetid: a955b3d2-c8ad-40dd-8ea3-9f1a271e1eed
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 80bb7f0998dd8ee1bc46105892e0e6f4e23b74c1
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895061"
---
# <a name="how-to-import-load-test-results-into-a-repository"></a>Como importar resultados do teste de carga para um repositório

Quando você executar um teste de carga, as informações coletadas durante a execução serão armazenadas no Repositório de Resultados de Testes de Carga. O Repositório de Resultados de Testes de Carga contém dados do contador de desempenho e informações sobre todos os erros. Para obter mais informações, confira [Gerenciar resultados do teste de carga no repositório de resultados do teste de carga](../test/manage-load-test-results-in-the-load-test-results-repository.md).

É possível gerenciar resultados do teste de carga no Editor de Teste de Carga usando a caixa de diálogo **Abrir e gerenciar resultados de testes de carga**. É possível abrir, importar, exportar e remover resultados de testes de carga.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-import-results-into-a-repository"></a>Para importar resultados para um repositório

1.  De um projeto de teste de carga e de desempenho na Web, abra um teste de carga.

2.  Na barra de ferramentas inserida, escolha **Abrir e gerenciar resultados**.

     A caixa de diálogo **Abrir e gerenciar resultados de testes de carga** é exibida.

3.  Em **Digite um nome de controlador para encontrar resultados de testes de carga**, selecione um controlador. Selecione **<local>\<** para acessar resultados armazenados localmente.

     Se houver resultados de testes de carga disponíveis, eles aparecerão na lista **Resultados de testes de carga**. As colunas são **Hora**, **Duração**, **Usuário**, **Resultado**, **Teste** e **Descrição**. **Teste** contém o nome do teste e **Descrição** contém a descrição opcional adicionada antes da execução do teste.

4.  Escolha **Importar**.

     A caixa de diálogo **Importar resultados de testes de carga** é exibida.

5.  Na caixa **Nome do arquivo**, digite o nome de um arquivo de resultados de teste armazenado e escolha **Abrir**.

     \- ou -

     Navegue até o arquivo e escolha **Abrir**.

    > [!NOTE]
    > O arquivo de resultados de teste armazenado que você especifica nesta etapa deve ter sido criado executando a operação Export.

     Os resultados são importados e aparecem na lista **Resultados de testes de carga**.

## <a name="see-also"></a>Consulte também

- [Gerenciar resultados do teste de carga no repositório de Resultados do Teste de Carga](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [Como exportar resultados do teste de carga de um repositório](../test/how-to-export-load-test-results-from-a-repository.md)