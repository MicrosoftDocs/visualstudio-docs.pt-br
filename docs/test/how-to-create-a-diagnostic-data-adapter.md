---
title: Como criar um adaptador de dados de diagnóstico no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Diagnostic Data Adapter, creating
ms.assetid: bd7ad36c-54cb-4d2a-9aea-9d10ad98d7ba
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 25adfc867ca208f367f047e4cb94322718e12b52
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895308"
---
# <a name="how-to-create-a-diagnostic-data-adapter"></a>Como criar um adaptador de dados de diagnóstico

Para criar um *adaptador de dados de diagnóstico*, crie uma biblioteca de classes usando o Visual Studio e adicione as APIs do Adaptador de Dados de Diagnóstico fornecidas pelo Visual Studio Enterprise à sua biblioteca de classes. Envie quaisquer informações que você desejar como um fluxo ou um arquivo ao <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionSink> fornecido pela estrutura ao manipular eventos gerados durante a execução de teste. Os fluxos ou arquivos enviados a <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionSink> são armazenados como arquivos anexos aos resultados de teste quando seu teste é concluído. Se você criar um bug desses resultados de teste ou quando usar o [!INCLUDE[mtrlong](../test/includes/mtrlong_md.md)], os arquivos também serão vinculados ao bug.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Você pode criar um adaptador de dados de diagnóstico que afeta o computador onde seus testes são executados, ou um computador que é parte do ambiente que você está usando para executar o aplicativo do teste. Por exemplo, coletando arquivos em seu computador de teste onde os testes são executados ou coletando arquivos no computador que serve na função de servidor Web para seu aplicativo.

Você pode dar ao adaptador de dados de diagnóstico um nome amigável a ser exibido quando você criar suas configurações de teste usando o Microsoft Test Manager ou usando o Visual Studio. As configurações de teste permitem que você defina qual função de computador executará adaptadores de dados de diagnóstico específicos em seu ambiente quando você executar os testes. Você também pode configurar os adaptadores de dados de diagnóstico ao criar suas configurações de teste. Por exemplo, você pode criar um adaptador de dados de diagnóstico que colete logs personalizados do servidor Web. Quando você cria suas configurações de teste, você pode selecionar para executar este adaptador de dados de diagnóstico no computador ou computadores que estão executando esta função do servidor Web, e pode alterar a configuração para que suas configurações de teste coletem somente os últimos três logs que foram criados. Para obter mais informações sobre as configurações de teste, confira [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md).

Os eventos são gerados quando você executa seus testes de modo que o adaptador de dados de diagnóstico possa executar tarefas nesse ponto no teste.

> [!IMPORTANT]
> Esses eventos podem ser gerados em threads diferentes, especialmente quando você tem testes que são executados em vários computadores. Portanto, você deve estar ciente de possíveis problemas de threading e não corromper inadvertidamente os dados internos do adaptador personalizado. Certifique-se de que o adaptador de dados de diagnóstico seja do tipo thread-safe.

A seguir está uma lista parcial dos principais eventos que você pode usar ao criar seu adaptador de dados de diagnóstico. Para obter uma lista completa de eventos do adaptador de dados de diagnóstico, consulte a classe abstrata <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents>.

|evento|Descrição|
|-|-----------------|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.SessionStart>|Início da execução do teste|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.SessionEnd>|Fim da execução do teste|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestCaseStart>|Início de cada teste na execução de testes|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestCaseEnd>|Fim de cada teste na execução de testes|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestStepStart>|Início de cada etapa de um teste|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestStepEnd>|Fim de cada etapa de um teste|

> [!NOTE]
> Quando um teste manual terminar, nenhum evento de coleção de dados é enviado ao adaptador de dados de diagnóstico. Quando um teste é executado novamente, terá um novo identificador de situação de teste. Se um usuário redefinir um teste durante um teste (gerando o evento <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestCaseReset>) ou se alterar um resultado da etapa de teste, nenhum evento da coleção de dados será enviado ao adaptador de dados de diagnóstico, mas o identificador de caso de teste permanecerá o mesmo. Para determinar se um caso de teste foi redefinido, você deve rastrear o identificador de caso de teste em seu adaptador de dados de diagnóstico.

Use o seguinte procedimento para criar o adaptador de dados de diagnóstico que coleta um arquivo de dados que é baseado nas informações que você configura quando você cria suas configurações de teste.

Para obter um projeto completo do adaptador de dados de diagnóstico de exemplo, incluindo um editor de configuração personalizado, confira [Projeto de exemplo para criar um adaptador de dados de diagnóstico](../test/sample-project-for-creating-a-diagnostic-data-adapter.md).

##  <a name="create-and-install-a-diagnostic-data-adapter"></a>Criar e instalar um adaptador de dados de diagnóstico

### <a name="to-create-and-install-a-diagnostic-data-adapter"></a>Para criar e instalar um adaptador de dados de diagnóstico

1. Criar uma nova biblioteca de classes.

   1.  No menu **Arquivo**, selecione **Novo** e aponte para **Novo projeto**.

   2.  De **Tipos de projeto**, selecione a linguagem a ser usada.

   3.  Em **Modelos instalados do Visual Studio**, clique em **Biblioteca de Classes**.

   4.  Digite um nome para o adaptador de dados de diagnóstico.

   5.  Escolha **OK**.

2. Adicione o assembly **Microsoft.VisualStudio.QualityTools.ExecutionCommon**.

   1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** e escolha o comando **Adicionar Referência**.

   2.  Escolha **.NET** e localize **Microsoft.VisualStudio.QualityTools.ExecutionCommon.dll**.

   3.  Escolha **OK**.

3. Adicione o assembly **Microsoft.VisualStudio.QualityTools.Common**.

   1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** e selecione o comando **Adicionar Referência**.

   2.  Escolha **.NET** e localize **Microsoft.VisualStudio.QualityTools.Common.dll**.

   3.  Escolha **OK**.

4. Adicione as seguintes instruções `using` para seu arquivo de classe:

   ```csharp
   using Microsoft.VisualStudio.TestTools.Common;
   using Microsoft.VisualStudio.TestTools.Execution;
   using System.Linq;
   using System.Text;
   using System.Xml;
   using System;
   ```

5. Adicione <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorTypeUriAttribute> à classe do seu adaptador de dados de diagnóstico para identificá-la como um adaptador de dados de diagnóstico, substituindo **Empresa**, **Produto** e **Versão** pelas informações apropriadas do seu adaptador de dados de diagnóstico:

   ```csharp
   [DataCollectorTypeUri("datacollector://Company/Product/Version")]
   ```

6. Adicione o atributo de <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorFriendlyNameAttribute> à classe, substituindo os parâmetros pelas informações apropriadas para o adaptador de dados de diagnóstico:

   ```csharp
   [DataCollectorFriendlyName("Collect Log Files", false)]
   ```

    Este nome amigável é exibido na atividade de configurações de teste.

   > [!NOTE]
   > Você também pode adicionar <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorConfigurationEditorAttribute> para especificar `Type` do editor de configuração personalizada para este adaptador de dados, e opcionalmente para especificar o arquivo de ajuda para usar o editor.
   >
   > Você também pode aplicar <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorEnabledByDefaultAttribute> para especificar que ele sempre deve ser ativado.

7. A classe do adaptador de dados de diagnóstico deve herdar da classe de <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollector> como segue:

   ```csharp
   public class MyDiagnosticDataAdapter : DataCollector
   ```

8. Adicione as variáveis locais como a seguir:

   ```csharp
   private DataCollectionEvents dataEvents;
   private DataCollectionLogger dataLogger;
   private DataCollectionSink dataSink;
   private XmlElement configurationSettings;
   ```

9. Adicione o método de <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollector.Initialize*> e um método **Dispose**. No método `Initialize`, você inicializa o coletor de dados, quaisquer dados de configuração das configurações de teste e registra os manipuladores de eventos que deseja usar como segue:

    ```csharp
    public override void Initialize(
        XmlElement configurationElement,
        DataCollectionEvents events,
        DataCollectionSink sink,
        DataCollectionLogger logger,
        DataCollectionEnvironmentContext environmentContext)
    {
           dataEvents = events;  // The test events
           dataLogger = logger;  // The error and warning log
           dataSink = sink;      // Saves collected data
           // Configuration from the test settings
           configurationSettings = configurationElement;

           // Register common events for the data collector
           // Not all of the events are used in this class
        dataEvents.SessionStart +=
            new EventHandler<SessionStartEventArgs>(OnSessionStart);
        dataEvents.SessionEnd +=
            new EventHandler<SessionEndEventArgs>(OnSessionEnd);
        dataEvents.TestCaseStart +=
            new EventHandler<TestCaseStartEventArgs>(OnTestCaseStart);
        dataEvents.TestCaseEnd +=
            new EventHandler<TestCaseEndEventArgs>(OnTestCaseEnd);
    }

    public override void Dispose(bool disposing)
    {
        if (disposing)
        {
            // Unregister the registered events
            dataEvents.SessionStart -=
                new EventHandler<SessionStartEventArgs>(OnSessionStart);
            dataEvents.SessionEnd -=
                new EventHandler<SessionEndEventArgs>(OnSessionEnd);
            dataEvents.TestCaseStart -=
                new EventHandler<TestCaseStartEventArgs>(OnTestCaseStart);
            dataEvents.TestCaseEnd -=
                new EventHandler<TestCaseEndEventArgs>(OnTestCaseEnd);
        }
    }
    ```

10. Use o seguinte código de manipulador de eventos e o método particular para coletar o arquivo de log gerado durante o teste:

    ```csharp
    public void OnTestCaseEnd(sender, TestCaseEndEventArgs e)
    {
        // Get any files to be collected that are
        // configured in your test settings
        List<string> files = getFilesToCollect();

        // For each of the files, send the file to the data sink
        // which will attach it to the test results or to a bug
        foreach (string file in files)
        {
            dataSink.SendFileAsync(e.Context, file, false);
        }
    }

    // A private method that returns the file names
    private List<string> getFilesToCollect()
    {
        // Get a namespace manager with our namespace
        XmlNamespaceManager nsmgr =
            new XmlNamespaceManager(
                configurationSettings.OwnerDocument.NameTable);
        nsmgr.AddNamespace("ns",
            "http://MyCompany/schemas/MyDataCollector/1.0");

        // Find all of the "File" elements under our configuration
        XmlNodeList files =
            configurationSettings.SelectNodes(
                "//ns:MyDataCollector/ns:File");

        // Build the list of files to collect from the
        // "FullPath" attributes of the "File" nodes.
        List<string> result = new List<string>();
        foreach (XmlNode fileNode in files)
        {
            XmlAttribute pathAttribute =
                fileNode.Attributes["FullPath"];
            if (pathAttribute != null &&
                !String.IsNullOrEmpty(pathAttribute.Value))
            {
                result.Add(pathAttribute.Value);
            }
        }

        return result;
    }
    ```

     Esses arquivos são anexados aos resultados de teste. Se você criar um bug desses resultados de teste ou quando usar o [!INCLUDE[mtrlong](../test/includes/mtrlong_md.md)], os arquivos também serão anexados ao bug.

     Caso deseje usar seu próprio editor para coletar dados para uso nas configurações de teste, confira [Como criar um editor personalizado de dados para o adaptador de dados de diagnóstico](../test/how-to-create-a-custom-editor-for-data-for-your-diagnostic-data-adapter.md).

11. Para coletar um arquivo de log quando um teste for concluído com base no que o usuário configurou nas configurações de teste, é necessário criar um arquivo *App.config* e adicioná-lo à solução. Este arquivo tem o seguinte formato e deve conter o URI para que o adaptador de dados de diagnóstico identifique-o. Substitua os valores reais de "Company/ProductName/Version".

    > [!NOTE]
    > Se você não precisar configurar quaisquer informações para o adaptador de dados de diagnóstico, então não será necessário criar um arquivo de configuração.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <configSections>
        <section name="DataCollectorConfiguration" type="Microsoft.VisualStudio.TestTools.Execution.DataCollectorConfigurationSection, Microsoft.VisualStudio.QualityTools.ExecutionCommon, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a "/>
      </configSections>
      <DataCollectorConfiguration xmlns="http://microsoft.com/schemas/VisualStudio/TeamTest/2010">
        <DataCollector typeUri="datacollector://MyCompany/MyProduct/1.0">
          <DefaultConfiguration>
            <!-- Your default config settings -->
            <Binaries>
              <Binary FullPath="C:\Example\Example.dll"/>
              <Binary FullPath="\\Server2\Example2.dll"/>
            </Binaries>
            <Symbols>
              <Symbol FullPath="\\ExampleServer\ExampleSymbol.pdb"/>
            </Symbols>
          </DefaultConfiguration>
        </DataCollector>
      </DataCollectorConfiguration>
    </configuration>
    ```

    > [!NOTE]
    > O elemento de configuração padrão pode conter todos os dados de que você precisar. Se o usuário não configurar o adaptador de dados de diagnóstico nas configurações de teste, os dados padrão serão passados para seu adaptador de dados de diagnóstico quando ele for executado. Como o XML que você adiciona à seção `<DefaultConfigurations>` provavelmente não é parte do esquema declarado, você pode ignorar todos os erros que o XML gerar.
    >
    > Existem outros exemplos dos arquivos de configuração no seguinte caminho baseado no diretório de instalação: *Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\DataCollectors*.

     Para obter mais informações sobre como definir suas configurações de teste para usar um ambiente ao executar testes, confira [Coletar dados de diagnóstico em testes manuais (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts).

     Para obter mais informações sobre como instalar o arquivo de configuração, confira [Como instalar um adaptador de dados de diagnóstico personalizado](../test/how-to-install-a-custom-diagnostic-data-adapter.md)

12. Construa sua solução para criar o assembly do adaptador de dados de diagnóstico.

13. Para obter informações sobre como instalar o editor personalizado, confira [Como instalar um adaptador de dados de diagnóstico personalizado](../test/how-to-install-a-custom-diagnostic-data-adapter.md).

14. Para obter mais informações sobre como definir suas configurações de teste para usar um ambiente ao executar testes, confira [Coletar dados de diagnóstico em testes manuais (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts).

15. Para selecionar o adaptador de dados de diagnóstico, primeiro você deve selecionar as configurações existentes de um teste ou criar um novo do Microsoft Test Manager ou do Visual Studio. O adaptador é exibido na guia **Dados e Diagnósticos** das configurações de teste com o nome amigável que você atribuiu à classe.

16. Defina as configurações de teste como ativas. Para obter mais informações sobre as configurações de teste, confira [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md).

17. Execute seus testes usando as configurações de teste com o adaptador de dados de diagnóstico selecionado.

    O arquivo de dados que você especificou está anexado aos resultados do teste.

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorConfigurationEditorAttribute>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollector>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionSink>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorTypeUriAttribute>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorFriendlyNameAttribute>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorEnabledByDefaultAttribute>
- [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md)
- [Coletar dados de diagnóstico em testes manuais (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)
- [Coletar dados de diagnóstico durante testes (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts)
- [Como criar um editor personalizado de dados para o adaptador de dados de diagnóstico](../test/how-to-create-a-custom-editor-for-data-for-your-diagnostic-data-adapter.md)