---
title: Criar um plug-in de nível de solicitação para testes de desempenho Web no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- request-level plug-in, creating
- Web performance tests, requests
ms.assetid: d0b5b23c-7e94-4637-be6c-2620a5442d46
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: cf94de633554cef495b0a9a023426ac49de75c76
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895269"
---
# <a name="how-to-create-a-request-level-plug-in"></a>Como criar um plug-in no nível da solicitação

*Solicitações* são as instruções declarativas que constituem testes de desempenho Web. Plug-ins de teste de desempenho na Web permitem isolar e reutilizar o código fora das instruções declarativas principais no teste de desempenho na Web. Você pode criar plug-ins e adicioná-los a uma solicitação individual, bem como ao teste de desempenho na Web que a contém. Um *plug-in de solicitação* personalizado oferece uma maneira de chamar um código quando uma solicitação específica é executada em um teste de desempenho Web.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Cada plug-in de solicitação de teste de desempenho na Web tem um método PreRequest e um método PostRequest. Depois de anexar um plug-in de solicitação a uma solicitação HTTP específica, o evento PreRequest será acionado antes de a solicitação ser emitido, e o PostRequest é acionado depois que a resposta é recebida.

Você pode criar um plug-in de solicitação de teste de desempenho na Web personalizado com sua própria classe a partir da classe base <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>.

Você pode usar plug-ins personalizados de solicitação de teste de desempenho na Web com os testes de desempenho na Web que você gravou. Os plug-ins personalizados de solicitação de teste de desempenho na Web permitem escrever uma quantidade mínima de código para alcançar um nível de maior controle sobre os testes de desempenho na Web. No entanto, também é possível usá-los com testes de desempenho na Web codificados. Consulte [Gerar e executar um teste de desempenho Web codificado](../test/generate-and-run-a-coded-web-performance-test.md).

## <a name="to-create-a-request-level-plug-in"></a>Para criar um plug-in de solicitação

1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução, selecione **Adicionar** e, em seguida, escolha **Novo Projeto**.

     A caixa de diálogo **Adicionar Novo Projeto** é exibida.

2.  Em **Modelos Instalados**, selecione **Visual C#**.

3.  Na lista de modelos, selecione **Biblioteca de Classes**.

4.  Na caixa de texto **Nome**, digite um nome para a classe e escolha **OK**.

     O novo projeto da biblioteca de classes é adicionado ao **Gerenciador de Soluções** e a nova classe é exibida no **Editor de Códigos**.

5.  No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Referências** da nova biblioteca de classes e selecione **Adicionar Referência**.

     A caixa de diálogo **Adicionar Referência** é exibida.

6.  Escolha a guia **.NET**, role para baixo, selecione **Microsoft.VisualStudio.QualityTools.WebTestFramework** e clique em **OK**

     A referência a **Microsoft.VisualStudio.QualityTools.WebTestFramework** é adicionada à pasta **Referência** do **Gerenciador de Soluções**.

7.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó superior do projeto de teste de carga e de desempenho Web que contém o teste de carga ao qual você deseja adicionar o plug-in do teste de solicitação do teste de desempenho Web. Selecione **Adicionar Referência**.

     A **caixa de diálogo Adicionar Referência é exibida**.

8.  Escolha a guia **Projetos**, selecione o **Projeto da Biblioteca de Classes** e, em seguida, escolha **OK**.

9. No **Editor de Códigos**, escreva o código do plug-in. Primeiro, crie uma nova classe pública que derive de <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>.

10. Implemente o código dentro de um dos manipuladores de eventos <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin.PreRequest*> e <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin.PostRequest*>. Consulte a seção Exemplo a seguir para obter uma implementação de exemplo.

11. Depois de gravar o código, compile o novo projeto.

12. Abra o teste de desempenho na Web ao qual deseja adicionar o plug-in de solicitação.

13. Clique com o botão direito do mouse na solicitação à qual você deseja adicionar o plug-in de solicitação e selecione **Adicionar plug-in de solicitações**.

     A caixa de diálogo **Adicionar plug-in de solicitação de teste na Web** é exibida.

14. Em **Selecionar um plug-in**, selecione o novo plug-in.

15. No painel **Propriedades do plug-in selecionado**, defina os valores iniciais a serem usados pelo plug-in em tempo de execução.

    > [!NOTE]
    > Você pode expor quantas propriedades quiser de seus plug-ins; apenas torne-os públicos, definíveis e de um tipo de base como Inteiro, Booliano ou Cadeia de Caracteres. Você também pode alterar as propriedades de plug-in de teste de desempenho na Web mais tarde usando a janela Propriedades.

16. Escolha **OK**.

     O plug-in é adicionado à pasta **Plug-ins de solicitação**, que é uma pasta filho da solicitação HTTP.

    > [!WARNING]
    > Você talvez receba um erro semelhante ao seguinte quando executar um teste de desempenho na Web ou um teste de carga usando seu plug-in:
    >
    > **Falha na solicitação: exceção em \<plug-in> evento: não foi possível carregar arquivo ou assembly '\<"Nome do plug-in".dll arquivo>, versão =\<n.n.n. n >, Culture=neutral, PublicKeyToken=null' ou uma de suas dependências. O sistema não pode localizar o arquivo especificado.**
    >
    > Isso acontecerá se você fizer alterações no código de qualquer um de seus plug-ins e criar uma nova versão de DLL **(versão=0.0.0.0)**, mas o plug-in ainda estiver referenciando a versão original do plug-in. Para corrigir esse problema, siga estas etapas:
    >
    > 1.  Em seu projeto de teste de carga e desempenho na Web, você verá um aviso em referências. Remova e adicione novamente a referência à DLL do plug-in.
    > 2.  Remova o plug-in do teste ou do local apropriado e adicione-o de volta.

## <a name="example"></a>Exemplo

Você pode usar o seguinte código para criar um plug-in personalizado de teste de desempenho na Web que exibe duas caixas de diálogo. Uma caixa de diálogo exibe a URL associada à solicitação à qual você anexa o suplemento de solicitação. A segunda caixa de diálogo exibe o nome do computador para o agente.

> [!NOTE]
> O código a seguir exige que você adicione uma referência a System.Windows.Forms.

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;
using Microsoft.VisualStudio.TestTools.WebTesting;

namespace RequestPluginNamespace
{
    public class MyWebRequestPlugin : WebTestRequestPlugin
    {
        public override void PostRequest(object sender, PostRequestEventArgs e)
        {
            MessageBox.Show(e.WebTest.Context.AgentName);
        }
        public override void PreRequest(object sender, PreRequestEventArgs e)
        {
            MessageBox.Show(e.Request.Url);
        }
    }
}
```

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>
- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [Codificar uma regra de extração personalizada para um teste de desempenho Web](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
- [Codificar uma regra de validação personalizada para um teste de desempenho Web](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
- [Como criar um plug-in de teste de carga](../test/how-to-create-a-load-test-plug-in.md)
- [Gerar e executar um teste de desempenho Web codificado](../test/generate-and-run-a-coded-web-performance-test.md)