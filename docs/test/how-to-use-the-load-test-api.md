---
title: API de teste de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- code, load tests
- plug-ins, load test
- APIs, load tests
ms.assetid: e15567bc-1f21-4feb-b81d-f17ba35cfde5
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 3b35b74f7adca4ff794f4d0c78b5585551864c8f
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894391"
---
# <a name="how-to-use-the-load-test-api"></a>Como usar a API de teste de carga

O Visual Studio dá suporte a plug-ins de teste de carga que podem controlar ou aprimorar um teste de carga. Os plug-ins de teste de carga são classes definidas pelo usuário que implementam a interface <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> localizada no namespace <xref:Microsoft.VisualStudio.TestTools.LoadTesting>. Os plug-ins de teste de carga permitem o controle personalizado do teste de carga, como anular um teste de carga quando um contador ou um limite de erros é atingido. Use as propriedades na classe <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest> para obter ou definir parâmetros do teste de carga no código definido pelo usuário. Use os eventos na classe <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest> para anexar delegados para notificações quando o teste de carga está em execução.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!TIP]
> Use o pesquisador de objetos para examinar o namespace <xref:Microsoft.VisualStudio.TestTools.LoadTesting>. Os editores do Visual C# e do Visual Basic oferecem suporte do IntelliSense para codificação com as classes no namespace.

Você também pode criar plug-ins para testes de desempenho na Web. Para obter mais informações, confira [Como criar um plug-in de teste de desempenho Web](../test/how-to-create-a-web-performance-test-plug-in.md) e [Como criar um plug-in no nível da solicitação](../test/how-to-create-a-request-level-plug-in.md).

## <a name="to-use-the-loadtesting-namespace"></a>Para usar o namespace LoadTesting

1.  Abra um projeto de teste de carga e de desempenho Web que contenha um teste de carga.

2.  Adicione um novo projeto de biblioteca de classes Visual C# ou Visual Basic à sua solução de teste.

3.  Adicione uma referência do projeto de teste de desempenho na Web e de carga ao projeto de biblioteca de classes.

4.  Adicione uma referência à DLL Microsoft.VisualStudio.QualityTools.LoadTestFramework no projeto de biblioteca de classes.

5.  No arquivo da classe no projeto de biblioteca de classes, adicione uma instrução `using` para o namespace <xref:Microsoft.VisualStudio.TestTools.LoadTesting>.

6.  Crie uma classe pública que implemente a interface <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>.

7.  Compile o projeto.

8.  Adicionar o novo plug-in de teste de carga usando o Editor de testes de carga:

    1.  Clique com o botão direito do mouse no nó raiz do teste de carga e escolha **Adicionar Plug-in de Teste de Carga**.

    2.  A caixa de diálogo **Adicionar Plug-in de Teste de Carga** é exibida.

    3.  No painel **Propriedades do plug-in selecionado**, defina os valores iniciais a serem usados pelo plug-in em tempo de execução.

        > [!NOTE]
        > Você pode expor quantas propriedades quiser de seus de plug-ins. Torne-os do tipo público, configurável ou base, como Inteiro, booliano ou Cadeia de Caracteres. Edite também as propriedades do plug-in de teste de carga posteriormente usando a janela **Propriedades**.

9. Execute o teste de carga.

     Para obter uma implementação de <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>, confira [Como criar um plug-in de teste de carga](../test/how-to-create-a-load-test-plug-in.md).

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting>
- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [Como usar a API de teste de desempenho Web](../test/how-to-use-the-web-performance-test-api.md)
- [Como criar um plug-in de teste de carga](../test/how-to-create-a-load-test-plug-in.md)