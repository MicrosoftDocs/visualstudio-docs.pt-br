---
title: Criar um plug-in de gravador para testes de desempenho Web no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, recorder plug-in
ms.assetid: 6fe13be1-aeb5-4927-9bff-35950e194da9
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 6525327e85d40b9b942e4e29a7d759a15598c824
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895828"
---
# <a name="how-to-create-a-recorder-plug-in"></a>Como criar um plug-in de gravação

O <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin> permite que você modifique um teste de desempenho na Web gravado. A modificação ocorre depois que você escolhe **Parar** na barra de ferramentas do **Gravador de Teste de Desempenho Web**, mas antes de o teste ser salvo e apresentado no Editor de Testes de Desempenho Web.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Um plug-in de gravador permite que você execute sua própria correlação personalizada em parâmetros dinâmicos. Com a funcionalidade de correlação interna, os testes de desempenho Web detectam os parâmetros dinâmicos na gravação da Web no momento da conclusão ou quando você usa **Promover Parâmetros Dinâmicos a Parâmetros de Teste na Web** na barra de ferramentas do **Editor de Testes de Desempenho Web**. No entanto, a funcionalidade de detecção interna nem sempre encontra todos os parâmetros dinâmicos. Por exemplo, ela não encontra uma ID da sessão, que normalmente tem seu valor alterado entre 5 a 30 minutos. Portanto, você precisa executar manualmente o processo de correlação.

O <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin> permite que você escreva código para seu próprio plug-in personalizado. Este plug-in pode executar a correlação ou modificar o teste de desempenho na Web de várias maneiras antes de ser salvo e apresentado no Editor de Testes de Desempenho Web. Portanto, se você determinar que uma variável dinâmica específica deve ser correlacionada para muitas de suas gravações, será possível automatizar o processo.

Um plug-in de gravação também pode ser usado para adicionar regras de extração e de validação, adicionar parâmetros de contexto ou converter comentários em transações em um teste de desempenho na Web.

Os procedimentos a seguir descrevem como criar o código rudimentar para um plug-in de gravação, implantar o plug-in e executar o plug-in. O código de exemplo após os procedimentos demonstra como usar o Visual C# para criar um plug-in de gravação personalizado para correlação de parâmetro dinâmico.

## <a name="create-a-recorder-plug-in"></a>Criar um plug-in do gravador

### <a name="to-create-a-recorder-plug-in"></a>Para criar um plug-in de gravação

1.  Abra uma solução que contenha o projeto de teste de carga e desempenho na Web com o teste de desempenho na Web para o qual você deseja criar um plug-in de gravação.

2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução, selecione **Adicionar** e, em seguida, escolha **Novo Projeto**.

     A caixa de diálogo **Adicionar Novo Projeto** é exibida.

3.  Em **Modelos Instalados**, selecione **Visual C#**.

4.  Na lista de modelos, selecione **Biblioteca de Classes**.

5.  Na caixa de texto **Nome**, digite um nome para o plug-in de gravador.

     A biblioteca de classes é adicionada ao **Gerenciador de Soluções** e a nova classe é aberta no **Editor de Códigos**.

6.  No **Gerenciador de Soluções**, na nova pasta de projeto da biblioteca de classes, clique com o botão direito do mouse na pasta **Referências** e selecione **Adicionar Referência**.

    > [!TIP]
    > Um exemplo de uma nova pasta de projeto de biblioteca de classes é **RecorderPlugins**.

     A caixa de diálogo **Adicionar Referência** é exibida.

7.  Selecione a guia **.NET**.

8.  Role para baixo, selecione **Microsoft.VisualStudio.QualityTools.WebTestFramework** e escolha **OK**.

     O **Microsoft.VisualStudio.QualityTools.WebTestFramework** é adicionado à pasta **Referências** do **Gerenciador de Soluções**.

9. Escreva o código para o plug-in de gravação. Primeiro, crie uma nova classe pública que derive de <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin>.

10. Substituir o método <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin.PostWebTestRecording*>.

    ```csharp
    public class Class1 : WebTestRecorderPlugin
        {
            public override void PostWebTestRecording(object sender, PostWebTestRecordingEventArgs e)
            {
                base.PostWebTestRecording(sender, e);
            }
        }
    ```

     Os argumentos de evento fornecerão dois objetos para trabalhar: o resultado gravado e o teste de desempenho na Web gravado. Isso permitirá que você itere pelo resultados procurando determinados valores e pule para a mesma solicitação no teste de desempenho na Web para fazer modificações. Você também pode modificar apenas o teste de desempenho na Web se quiser adicionar um parâmetro de contexto ou parametrizar partes da URL.

    > [!NOTE]
    > Se você modificar o teste de desempenho na Web, também será preciso definir a propriedade <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostWebTestRecordingEventArgs.RecordedWebTestModified*> como verdadeira: `e.RecordedWebTestModified = true;`

11. Adicione mais código de acordo com o que você deseja que o plug-in de gravação execute depois da gravação da Web. Por exemplo, você pode adicionar código para manipular a correlação personalizada, conforme mostrado no exemplo abaixo. Também é possível criar um plug-in de gravação para tarefas como converter comentários em transações ou adicionar regras de validação ao teste de desempenho na Web.

12. No menu **Build**, escolha **Compilar \<nome do projeto de biblioteca de classes>**.

13. Em seguida, implante o plug-in de gravador para que ele seja registrado com o Visual Studio.

### <a name="deploy-the-recorder-plug-in"></a>Implantar o plug-in de gravação

Depois de compilar o plug-in de gravação, coloque a DLL resultante em um dos dois locais:

- *%ProgramFiles(x86)%\Microsoft Visual Studio\\[version]\\[edition]\Common7\IDE\PrivateAssemblies\WebTestPlugins*

- *%USERPROFILE%\Documents\Visual Studio [version]\WebTestPlugins*

> [!WARNING]
> Depois de copiar o plug-in de gravador em um dos dois locais, você deverá reiniciar o Visual Studio para que ele seja registrado.

### <a name="to-execute-the-recorder-plug-in"></a>Para executar o plug-in de gravação

1.  Crie um novo teste de desempenho na Web.

     A caixa de diálogo **Habilitar WebTestRecordPlugins** é exibida.

2.  Marque a caixa de seleção do plug-in de gravador e escolha **OK**.

     Depois que o teste de desempenho na Web concluir a gravação, o novo plug-in de gravação será executado.

    > [!WARNING]
    > Você talvez receba um erro semelhante ao seguinte quando executar um teste de desempenho na Web ou um teste de carga usando seu plug-in:
    >
    > **Falha na solicitação: exceção em \<plug-in> evento: não foi possível carregar arquivo ou assembly '\<"Nome do plug-in".dll arquivo>, versão =\<n.n.n. n >, Culture=neutral, PublicKeyToken=null' ou uma de suas dependências. O sistema não pode localizar o arquivo especificado.**
    >
    > Isso acontecerá se você fizer alterações no código de qualquer um de seus plug-ins e criar uma nova versão de DLL **(versão=0.0.0.0)**, mas o plug-in ainda estiver referenciando a versão original do plug-in. Para corrigir esse problema, siga estas etapas:
    >
    > 1. Em seu projeto de teste de carga e desempenho na Web, você verá um aviso em referências. Remova e adicione novamente a referência à DLL do plug-in.
    > 2. Remova o plug-in do teste ou do local apropriado e adicione-o de volta.

## <a name="example"></a>Exemplo

Este exemplo demonstra como criar um plug-in personalizado de gravação de teste de desempenho na Web para executar a correlação personalizada de parâmetro dinâmico.

> [!NOTE]
> Uma listagem completa do código de exemplo está localizada na parte final deste tópico.

**Revisando o código de exemplo**

## <a name="iterate-through-the-result-to-find-first-page-with-reportsession"></a>Iterar pelo resultado para encontrar a primeira página com ReportSession

Esta parte do exemplo de código é iterada em cada objeto gravado e pesquisa o corpo da resposta em busca de ReportSession.

```csharp
foreach (WebTestResultUnit unit in e.RecordedWebTestResult.Children)
 {
     WebTestResultPage page = unit as WebTestResultPage;
     if (page != null)
     {
         if (!foundId)
         {
             int indexOfReportSession = page.RequestResult.Response.BodyString.IndexOf("ReportSession");
             if (indexOfReportSession > -1)
             {
```

## <a name="add-an-extraction-rule"></a>Adicionar uma regra de extração

Agora que uma resposta foi encontrada, você precisa adicionar uma regra de extração. Esta parte do exemplo de código cria a regra de extração usando a classe <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRuleReference> e, em seguida, localiza a solicitação correta no teste de desempenho na Web à qual adicionar a regra de extração. Cada objeto de resultado tem uma nova propriedade DeclarativeWebTestItemId adicionada, que é a que está sendo usada no código para obtenção da solicitação correta no teste de desempenho na Web.

```csharp
ExtractionRuleReference ruleReference = new ExtractionRuleReference();
     ruleReference.Type = typeof(ExtractText);
     ruleReference.ContextParameterName = "SessionId";
     ruleReference.Properties.Add(new PluginOrRuleProperty("EndsWith", "&ControlID="));
     ruleReference.Properties.Add(new PluginOrRuleProperty("HtmlDecode", "True"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("IgnoreCase", "True"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("Index", "0"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("Required", "True"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("StartsWith", "ReportSession="));
     ruleReference.Properties.Add(new PluginOrRuleProperty("UseRegularExpression", "False"));

     WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
     if (requestInWebTest != null)
     {
         requestInWebTest.ExtractionRuleReferences.Add(ruleReference);
         e.RecordedWebTestModified = true;
     }
```

## <a name="replace-query-string-parameters"></a>Substituir parâmetros da cadeia de caracteres de consulta

Agora o código localiza os parâmetros da cadeia de caracteres de consulta que têm ReportSession como o nome e altera o valor para {{SessionId}}, conforme mostrado nesta parte do exemplo de código:

```csharp
WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
if (requestInWebTest != null)
{
    foreach (QueryStringParameter param in requestInWebTest.QueryStringParameters)
    {
         if (param.Name.Equals("ReportSession"))
         {
             param.Value = "{{SessionId}}";
         }
     }
 }
```

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.TestTools.WebTesting;
using Microsoft.VisualStudio.TestTools.WebTesting.Rules;

namespace RecorderPlugin
{
    [DisplayName("Correlate ReportSession")]
    [Description("Adds extraction rule for Report Session and binds this to querystring parameters that use ReportSession")]
    public class CorrelateSessionId : WebTestRecorderPlugin
    {
        public override void PostWebTestRecording(object sender, PostWebTestRecordingEventArgs e)
        {
            //first find the session id
            bool foundId = false;
            foreach (WebTestResultUnit unit in e.RecordedWebTestResult.Children)
            {
                WebTestResultPage page = unit as WebTestResultPage;
                if (page != null)
                {
                    if (!foundId)
                    {
                        int indexOfReportSession = page.RequestResult.Response.BodyString.IndexOf("ReportSession");
                        if (indexOfReportSession > -1)
                        {
                            //add an extraction rule to this request
                            // Get the corresponding request in the Declarative Web performance test
                            ExtractionRuleReference ruleReference = new ExtractionRuleReference();

                            ruleReference.Type = typeof(ExtractText);
                            ruleReference.ContextParameterName = "SessionId";
                            ruleReference.Properties.Add(new PluginOrRuleProperty("EndsWith", "&ControlID="));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("HtmlDecode", "True"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("IgnoreCase", "True"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("Index", "0"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("Required", "True"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("StartsWith", "ReportSession="));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("UseRegularExpression", "False"));

                            WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
                            if (requestInWebTest != null)
                            {
                                requestInWebTest.ExtractionRuleReferences.Add(ruleReference);
                                e.RecordedWebTestModified = true;
                            }
                            foundId = true;

                        }
                    }
                    else
                    {
                        //now update query string parameters
                        WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
                        if (requestInWebTest != null)
                        {
                            foreach (QueryStringParameter param in requestInWebTest.QueryStringParameters)
                            {
                                if (param.Name.Equals("ReportSession"))
                                {
                                    param.Value = "{{SessionId}}";
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin.PostWebTestRecording*>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRuleReference>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin.PostWebTestRecording*>
- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [Gerar e executar um teste de desempenho Web codificado](../test/generate-and-run-a-coded-web-performance-test.md)