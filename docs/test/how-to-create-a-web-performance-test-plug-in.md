---
title: Criar um plug-in de teste de desempenho Web
ms.date: 10/03/2016
ms.topic: how-to
f1_keywords:
- vs.test.web.webtestplugin
helpviewer_keywords:
- Web performance tests, creating plug-ins
- plug-ins, creating in Web performance tests
ms.assetid: a612f2d2-9806-477d-a126-12842f07da6e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3c9651f4003647e18ba52e916aeb21e176274de5
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287929"
---
# <a name="how-to-create-a-web-performance-test-plug-in"></a>Como criar um plug-in de teste de desempenho Web

Plug-ins de teste de desempenho na Web permitem isolar e reutilizar o código fora das instruções declarativas principais no teste de desempenho na Web. Um plug-in de teste de desempenho na Web personalizado oferece uma maneira de chamar um código quando o teste de desempenho na Web é executado. O plug-in de teste de desempenho na Web é executado uma vez para cada iteração de teste. Além disso, se você substituir os métodos PreRequest ou PostRequest no plug-in de teste, esses plug-ins de solicitação serão executados antes ou depois de cada solicitação, respectivamente.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Você pode criar um plug-in de teste de desempenho na Web personalizado com sua própria classe a partir da classe base <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin>.

Você pode usar plug-ins de teste de desempenho na Web personalizados com os testes de desempenho na Web que você gravou, o que permite escrever uma quantidade mínima de código para obter um nível de maior controle sobre os testes de desempenho na Web. No entanto, também é possível usá-los com testes de desempenho na Web codificados. Para obter mais informações, consulte [Gerar e executar um teste de desempenho Web codificado](../test/generate-and-run-a-coded-web-performance-test.md).

> [!NOTE]
> Você também pode criar plug-ins de teste de carga. Consulte [como: criar um plug-in de teste de carga](../test/how-to-create-a-load-test-plug-in.md).

## <a name="to-create-a-custom-web-performance-test-plug-in"></a>Para criar um plug-in de teste de desempenho Web personalizado

1. Abra um projeto de teste de carga e de desempenho na Web contendo um teste de desempenho na Web.

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução e selecione **Adicionar** e, em seguida, escolha **novo projeto**.

3. Crie um projeto de **Biblioteca de Classes**.

   O novo projeto da biblioteca de classes é adicionado ao **Gerenciador de Soluções** e a nova classe é exibida no **Editor de Códigos**.

4. Em **Gerenciador de soluções**, clique com o botão direito do mouse na pasta **referências** na nova biblioteca de classes e selecione **Adicionar referência**.

   A caixa de diálogo **Adicionar Referência** é exibida.

5. Escolha a guia **.NET**, role para baixo e selecione **Microsoft.VisualStudio.QualityTools.WebTestFramework**

6. Escolha **OK**.

     A referência a **Microsoft. VisualStudio. QualityTools. WebTestFramework** é adicionada à pasta de **referência** em **Gerenciador de soluções**.

7. No **Gerenciador de soluções**, clique com o botão direito do mouse no nó superior do projeto de teste de carga e desempenho na Web que contém o teste de carga ao qual você deseja adicionar o plug-in de teste de desempenho da Web e selecione **Adicionar referência**.

8. A **caixa de diálogo Adicionar referência é exibida**.

9. Escolha a guia **projetos** e selecione o **projeto de biblioteca de classes**.

10. Escolha **OK**.

11. No **Editor de Códigos**, escreva o código do plug-in. Primeiro, crie uma nova classe pública que derive de <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin>.

12. Implemente o código dentro de um ou mais manipuladores de eventos. Consulte a seção Exemplo a seguir para obter uma implementação de exemplo.

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostWebTestRecordingEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostWebTestEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PreRequestEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostRequestEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PrePageEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostPageEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PreTransactionEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostTransactionEventArgs>

13. Depois de gravar o código, compile o novo projeto.

14. Abra um teste de desempenho na Web.

15. Para adicionar o plug-in de teste de desempenho da Web, escolha **Adicionar plug-in de teste** na barra de ferramentas.

     A caixa de diálogo **Adicionar plug-in de teste na Web** é exibida.

16. Em **selecionar um plug-in**, selecione sua classe de plug-in de teste de desempenho na Web.

17. No painel **Propriedades do plug-in selecionado**, defina os valores iniciais a serem usados pelo plug-in em tempo de execução.

    > [!NOTE]
    > Você pode expor quantas propriedades quiser de seus plug-ins; apenas torne-os públicos, definíveis e de um tipo de base como Inteiro, Booliano ou Cadeia de Caracteres. Você também pode alterar as propriedades de plug-in de teste de desempenho na Web mais tarde usando a janela Propriedades.

18. Escolha **OK**.

     O plug-in é adicionado à pasta **Plug-ins de teste na Web**.

    > [!WARNING]
    > Você talvez receba um erro semelhante ao seguinte quando executar um teste de desempenho na Web ou um teste de carga usando seu plug-in:
    >
    > **Falha na solicitação: exceção no \<plug-in> evento: não foi possível carregar o arquivo ou assembly ' \<"Plug-in name".dll file> , versão = \<n.n.n.n> , cultura = neutral, PublicKeyToken = null ' ou uma de suas dependências. O sistema não pode localizar o arquivo especificado.**
    >
    > Isso acontecerá se você fizer alterações no código de qualquer um de seus plug-ins e criar uma nova versão de DLL **(versão=0.0.0.0)**, mas o plug-in ainda estiver referenciando a versão original do plug-in. Para corrigir esse problema, siga estas etapas:
    >
    > 1. Em seu projeto de teste de carga e desempenho na Web, você verá um aviso em referências. Remova e adicione novamente a referência à DLL do plug-in.
    > 2. Remova o plug-in do teste ou do local apropriado e adicione-o de volta.

## <a name="example"></a>Exemplo

O código a seguir cria um plug-in de teste de desempenho na Web personalizado que adiciona um item a <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestContext> que representa a iteração de teste.

Depois de executar o teste de desempenho da Web, usando esse plug-in, você pode ver o item adicionado chamado **TestIteratnionNumber** na guia **contexto** do Visualizador de **resultados de desempenho da Web**.

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using System.ComponentModel;
using Microsoft.VisualStudio.TestTools.WebTesting;

namespace SampleRules
{
    [Description("This plugin can be used to set the ParseDependentsRequests property for each request")]
    public class SampleWebTestPlugin : WebTestPlugin
    {
        private bool m_parseDependents = true;

        public override void PreWebTest(object sender, PreWebTestEventArgs e)
        {
            // TODO: Add code to execute before the test.
        }

        public override void PostWebTest(object sender, PostWebTestEventArgs e)
        {
            // TODO: Add code to execute after the test.
        }

        public override void PreRequest(object sender, PreRequestEventArgs e)
        {
            // Code to execute before each request.
            // Set the ParseDependentsRequests value on the request
            e.Request.ParseDependentRequests = m_parseDependents;
        }

        // Properties for the plugin.
        [DefaultValue(true)]
        [Description("All requests will have their ParseDependentsRequests property set to this value")]
        public bool ParseDependents
        {
            get
            {
                return m_parseDependents;
            }
            set
            {
                m_parseDependents = value;
            }
        }
    }
}
```

## <a name="see-also"></a>Veja também

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>
- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [Como criar um plug-in no nível da solicitação](../test/how-to-create-a-request-level-plug-in.md)
- [Codificar uma regra de extração personalizada para um teste de desempenho Web](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
- [Codificar uma regra de validação personalizada para um teste de desempenho Web](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
- [Como criar um plug-in de teste de carga](../test/how-to-create-a-load-test-plug-in.md)
- [Gerar e executar um teste de desempenho para Web codificado](../test/generate-and-run-a-coded-web-performance-test.md)
