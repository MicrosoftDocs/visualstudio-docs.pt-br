---
title: Criar código e plug-ins personalizados para testes de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.dialog.recorderplugin
helpviewer_keywords:
- Web performance tests, plug-ins
- load tests, plug-ins
ms.assetid: 0c0fcc99-673b-4ea0-a268-0475f66e5cb6
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: ed7b588d597626348b4c148c10dad165649b0468
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895750"
---
# <a name="create-custom-code-and-plug-ins-for-load-tests"></a>Criar código personalizado e plug-ins para testes de carga

Um plug-in personalizado usa um código que você grava e anexa a um teste de carga ou a um teste de desempenho na Web. Você pode usar a API do teste de carga API e a API do teste de desempenho na Web a fim de criar plug-ins personalizados para que os testes sejam expandidos até a funcionalidade interna. Você pode adicionar vários plug-ins ao teste de carga.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="tasks"></a>Tarefas

|Tarefas|Tópicos associados|
|-|-----------------------|
|**Criar um plug-in personalizado para o teste de carga**: você pode usar a API do teste de carga para criar um plug-in personalizado a fim de adicionar mais funcionalidade de teste ao teste de carga.|-   [Como usar a API de teste de carga](../test/how-to-use-the-load-test-api.md)<br />-   [Como criar um plug-in de teste de carga](../test/how-to-create-a-load-test-plug-in.md)|
|**Criar um plug-in personalizado para o teste de desempenho Web:** você pode usar a API do teste de desempenho Web para criar um plug-in personalizado a fim de adicionar mais funcionalidade de teste ao teste de desempenho Web, inclusive no nível de solicitação. Você também pode criar um teste de serviço Web.<br /><br /> Além disso, você pode criar um plug-in de gravador da Web capaz de modificar um teste de desempenho na Web depois de gravado, mas antes de ser exibido no Visualizador de Testes de Desempenho Web.|-   [Como usar a API de teste de desempenho Web](../test/how-to-use-the-web-performance-test-api.md)<br />-   [Como criar um plug-in de teste de desempenho Web](../test/how-to-create-a-web-performance-test-plug-in.md)<br />-   [Como criar um plug-in no nível da solicitação](../test/how-to-create-a-request-level-plug-in.md)<br />-   [Como criar um teste de serviço Web](../test/how-to-create-a-web-service-test.md)<br />-   [Como criar um plug-in de gravação](../test/how-to-create-a-recorder-plug-in.md)|
|**Adicionar recursos de interface do usuário ao Visualizador de Resultados de Teste de Desempenho Web:** você pode adicionar mais recursos de interface do usuário ao Visualizador de Resultados de Teste de Desempenho Web usando um suplemento do Visual Studio.|-   [Como criar um suplemento do Visual Studio para o visualizador de resultados do teste de desempenho Web](../test/how-to-create-an-add-in-for-the-web-performance-test-results-viewer.md)|
|**Criar um editor de corpo HTTP personalizado:** você pode criar um editor personalizado para editar respostas XML HTTP de cadeia de caracteres ou binárias de um serviço Web.|-   [Como criar um editor de corpo HTTP personalizado para o editor de teste de desempenho Web](../test/how-to-create-a-custom-http-body-editor-for-the-web-performance-test-editor.md)|

## <a name="reference"></a>Referência

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin>

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>

<xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin>

<xref:Microsoft.VisualStudio.TestTools.LoadTesting>

## <a name="see-also"></a>Consulte também

- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [Gerar e executar um teste de desempenho Web codificado](../test/generate-and-run-a-coded-web-performance-test.md)