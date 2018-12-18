---
title: API de teste de desempenho Web no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, using the API
- APIs, Web performance tests
ms.assetid: 93a6a1dd-663b-4ab5-8760-7d6b081561d3
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 1f0fc5bdc5b17c13bfb0d4adf07a4a48347ce38b
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896452"
---
# <a name="how-to-use-the-web-performance-test-api"></a>Como usar a API de teste de desempenho Web

Você pode escrever o código para os testes de desempenho na Web. A API de teste de desempenho na Web é usada para criar testes de desempenho na Web codificados, plug-ins de teste de desempenho na Web, plug-ins de solicitação, solicitações, regras de extração e regras de validação. As classes que compõem esses tipos são as classes principais nessa API. Os outros tipos nessa API são usados para oferecer suporte à criação de objetos <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTest>, <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin>, <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>, <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequest>, <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule> e <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule>. Você usa o namespace <xref:Microsoft.VisualStudio.TestTools.WebTesting> para criar testes de desempenho na Web personalizados.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Você também pode usar a API de teste de desempenho na Web para criar e salvar programaticamente testes de desempenho na Web declarativos. Para fazer isso, use as classes <xref:Microsoft.VisualStudio.TestTools.WebTesting.DeclarativeWebTest> e <xref:Microsoft.VisualStudio.TestTools.WebTesting.DeclarativeWebTestSerializer>.

> [!TIP]
> Use o pesquisador de objetos para examinar o namespace <xref:Microsoft.VisualStudio.TestTools.WebTesting>. Os editores do Visual C# e do Visual Basic oferecem suporte do IntelliSense para codificação com as classes no namespace.

Você também pode criar plug-ins para teste de carga. Para obter mais informações, confira [Como usar a API de teste de carga](../test/how-to-use-the-load-test-api.md) e [Como criar um plug-in de teste de carga](../test/how-to-create-a-load-test-plug-in.md).

## <a name="to-use-the-webtesting-namespace"></a>Para usar o namespace WebTesting

1.  Abra um projeto de teste de carga e de desempenho na Web contendo um teste de desempenho na Web.

2.  Adicione um novo projeto de biblioteca de classes Visual C# ou Visual Basic à sua solução de teste.

3.  Adicione uma referência do projeto de teste de desempenho na Web e de carga ao projeto de biblioteca de classes.

4.  Adicione uma referência à DLL Microsoft.VisualStudio.QualityTools.WebTestFramework no projeto de biblioteca de classes.

5.  No arquivo da classe que está localizado no projeto de biblioteca de classes, adicione uma instrução `using` para o namespace <xref:Microsoft.VisualStudio.TestTools.WebTesting>.

6.  Crie uma nova classe que implemente a interface <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin>.

7.  Compile o projeto.

8.  Adicione o novo plug-in de teste de desempenho na Web usando o Editor de Testes de Desempenho Web:

    1.  Escolha **Adicionar plug-in de teste na Web** na barra de ferramentas.

         A caixa de diálogo **Adicionar plug-in de teste na Web** é exibida.

    2.  Em **Selecionar um plug-in**, selecione a classe do plug-in do teste de desempenho da Web.

    3.  No painel **Propriedades do plug-in selecionado**, defina os valores iniciais a serem usados pelo plug-in em tempo de execução.

        > [!NOTE]
        > Você pode expor quantas propriedades quiser de seus plug-ins; apenas torne-os públicos, definíveis e de um tipo de base como Inteiro, Booliano ou Cadeia de Caracteres. Você também pode editar as propriedades de plug-in de teste de desempenho na Web mais tarde usando a janela Propriedades.

    4.  Escolha **OK**.

9. Execute o teste de desempenho na Web.

     Para obter um exemplo de implementação de <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin>, confira [Como criar um plug-in de teste de desempenho Web](../test/how-to-create-a-web-performance-test-plug-in.md).

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.WebTesting>
- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [Como usar a API de teste de carga](../test/how-to-use-the-load-test-api.md)
- [Como criar um plug-in de teste de desempenho Web](../test/how-to-create-a-web-performance-test-plug-in.md)