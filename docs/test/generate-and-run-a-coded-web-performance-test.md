---
title: Testes de desempenho Web codificados no Visual Studio
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, walkthroughs
- Web performance tests, creating
- code, Web performance tests
- Web performance tests, coded
ms.assetid: 169e48f9-52fd-4d0b-83d9-54913bde506b
dev_langs:
- CSharp
- VB
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 76b2e7eebf66bb4a9c2564ca30a72a7b17dbdcfc
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895503"
---
# <a name="generate-and-run-a-coded-web-performance-test"></a>Gerar e executar um teste de desempenho Web codificado

Testes de desempenho Web são gravados navegando-se no aplicativo Web. Os testes são incluídos em testes de carga para medir o desempenho de seu aplicativo Web sob o estresse de vários usuários. Um teste de desempenho na Web pode ser convertido em um script baseado em código que você pode editar e personalizar como qualquer outro código-fonte. Por exemplo, você pode adicionar constructos de loop e de ramificação.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="generate-a-coded-web-performance-test"></a>Gerar um teste de desempenho na Web codificado

1.  Se não tiver criado um teste de desempenho Web, consulte [Gravar um teste de desempenho Web](/azure/devops/test/load-test/run-performance-tests-app-before-release#create-a-web-performance-and-load-test-project?view=vsts).

2.  Gere o teste codificado.

     ![Gerar um teste de desempenho na Web codificado](../test/media/web_test_coded_generate.png)

3.  Nomeie o teste.

     ![Insira um nome para o teste de desempenho Web codificado](../test/media/web_test_coded_generate_nametest.png)

     O novo teste codificado é aberto no editor de códigos.

     Dependendo de qual desempenho da Web e do modelo de projeto de teste que você adicionou na sua solução, o código será gerado no Visual Basic ou no Visual C#.

     ![O novo teste codificado é aberto no editor de código](../test/media/web_test_coded_generate_opencodeeditor.png)

     Você pode ver no código que o método GetRequestEnumerator() em C# ou o método Run() em Visual Basic contém cada regra de validação e solicitação da Web que estava no teste gravado.

4.  Para demonstrar a adição de alguns códigos simples, role para baixo até o final do método e depois do código da solicitação da Web mais recente e adicione o seguinte código:

    ```c#
    if (DateTime.Today.DayOfWeek == DayOfWeek.Wednesday)
    {
        WebTestRequest customRequest = new WebTestRequest("http://weather.msn.com/");
        yield return customRequest;
    }
    else
    {
        WebTestRequest customRequest = new WebTestRequest("https://msdn.microsoft.com/");
        yield return customRequest;
    }
    ```

    ```vb
    If DateTime.Today.DayOfWeek = DayOfWeek.Wednesday Then
        Dim customRequest As WebTestRequest = New WebTestRequest("http://weather.msn.com/")
        MyBase.Send(customRequest)
    Else
        Dim customRequest As WebTestRequest = New WebTestRequest("https://msdn.microsoft.com/")
        MyBase.Send(customRequest)
    End If
    ```

5.  Compile a solução para verificar se o código personalizado é compilado.

6.  Execute o teste.

     ![Executar o teste de desempenho Web codificado](../test/media/web_test_coded_generate_run.png)

     E calhou do teste ter acontecido em uma quarta-feira…

     ![Resultados de teste de desempenho Web codificado](../test/media/web_test_coded_generate_results.png)

## <a name="qa"></a>PERGUNTAS E RESPOSTAS

### <a name="q-can-i-run-more-than-one-test-at-a-time"></a>P: Posso executar mais de um teste por vez?
 **R** Sim, use o menu de contexto no **Gerenciador de Soluções**.

### <a name="q-should-i-add-a-data-source-before-or-after-i-generate-a-coded-test"></a>P: Devo adicionar uma fonte de dados antes ou depois de gerar um teste codificado?
 **R** É mais fácil adicionar uma [fonte de dados](../test/add-a-data-source-to-a-web-performance-test.md) antes de gerar o teste codificado, pois o código será gerado automaticamente para você.

 Ao executar um teste codificado com uma fonte de dados, você talvez veja a seguinte mensagem de erro:

 **Não foi possível executar o teste \<Nome do teste> no agente \<Nome do computador>: Referência de objeto não definida para uma instância de um objeto.**

 Isso pode ocorrer porque você tem um DataSourceAttribute definido para a classe de teste, sem um DataBindingAttribute correspondente. Para resolver esse erro, adicione um DataBindingAttribute apropriado, exclua-o ou insira um comentário fora do código.

### <a name="q-should-i-add-validation-and-extraction-rules-before-or-after-i-generate-a-coded-test"></a>P: Devo adicionar regras de validação e extração antes ou depois de gerar um teste codificado?
 **R:** É mais fácil adicionar as regras de validação e de extração antes de gerar o teste codificado. No entanto, recomendamos que você use [testes de IU codificados](../test/use-ui-automation-to-test-your-code.md) para fins de validação.