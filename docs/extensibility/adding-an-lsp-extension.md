---
title: Adicionando uma extensão de protocolo de servidor de linguagem | Microsoft Docs
description: Saiba como criar uma extensão do Visual Studio que integre um servidor de idiomas com base no LSP (protocolo de servidor de idiomas).
ms.custom: SEO-VS-2020
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 52f12785-1c51-4c2c-8228-c8e10316cd83
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: accf054cbf0b58066568124a3f35e064ce3cba78
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094985"
---
# <a name="add-a-language-server-protocol-extension"></a>Adicionar uma extensão do Language Server Protocol

O LSP (protocolo de servidor de linguagem) é um protocolo comum, na forma de JSON RPC v 2.0, usado para fornecer recursos de serviço de linguagem a vários editores de código. Usando o protocolo, os desenvolvedores podem escrever um único servidor de linguagem para fornecer recursos de serviço de linguagem como IntelliSense, diagnóstico de erros, localizar todas as referências e assim por diante, a vários editores de código que dão suporte a LSP. Tradicionalmente, os serviços de linguagem no Visual Studio podem ser adicionados usando arquivos de gramática de texto para fornecer funcionalidades básicas, como realce de sintaxe ou escrevendo serviços de linguagem personalizados que usam o conjunto completo de APIs de extensibilidade do Visual Studio para fornecer dados mais ricos. Com o suporte do Visual Studio para LSP, há uma terceira opção.

![serviço de protocolo de servidor de linguagem no Visual Studio](media/lsp-service-in-VS.png)

## <a name="language-server-protocol"></a>Language Server Protocol

![implementação do protocolo de servidor de idioma](media/lsp-implementation.png)

Este artigo descreve como criar uma extensão do Visual Studio que usa um servidor de linguagem baseado em LSP. Ele pressupõe que você já desenvolveu um servidor de linguagem baseado em LSP e deseja apenas integrá-lo ao Visual Studio.

Para obter suporte no Visual Studio, os servidores de linguagem podem se comunicar com o cliente (Visual Studio) por meio de qualquer mecanismo de transmissão baseado em fluxo, por exemplo:

* Fluxos de entrada/saída padrão
* Pipes nomeados
* Soquetes (somente TCP)

A intenção do LSP e do suporte para ele no Visual Studio é integrar os serviços de linguagem que não fazem parte do produto Visual Studio. Não se destina a estender os serviços de linguagem existentes (como C#) no Visual Studio. Para estender os idiomas existentes, consulte o guia de extensibilidade do serviço de linguagem (por exemplo, o [.net Compiler Platform "Roslyn"](../extensibility/dotnet-compiler-platform-roslyn-extensibility.md)) ou consulte [estender os serviços de editor e linguagem](../extensibility/extending-the-editor-and-language-services.md).

Para obter mais informações sobre o próprio protocolo, consulte a documentação [aqui](https://github.com/Microsoft/language-server-protocol).

Para obter mais informações sobre como criar um servidor de idioma de exemplo ou como integrar um servidor de idioma existente ao Visual Studio Code, consulte a documentação [aqui](https://code.visualstudio.com/docs/extensions/example-language-server).

## <a name="language-server-protocol-supported-features"></a>Recursos com suporte do protocolo de servidor de linguagem

As tabelas a seguir mostram quais recursos de LSP têm suporte no Visual Studio:

Mensagem | Tem suporte no Visual Studio
--- | ---
inicializar | sim
inicializado | sim
shutdown | sim
exit | sim
US $/cancelRequest | sim
janela/mensagem | sim
janela/showMessageRequest | sim
janela/logMessage | sim
telemetria/evento |
cliente/registerCapability |
cliente/unregisterCapability |
espaço de trabalho/didChangeConfiguration | sim
espaço de trabalho/didChangeWatchedFiles | sim
espaço de trabalho/símbolo | sim
espaço de trabalho/executeCommand | sim
espaço de trabalho/applyEdit | sim
textDocument/publishDiagnostics | sim
textDocument/didOpen | sim
textDocument/didChange | sim
textDocument/willSave |
textDocument/willSaveWaitUntil |
textDocument/didSave | sim
textDocument/didClose | sim
textDocument/conclusão | sim
conclusão/resolução | sim
textDocument/focalizar | sim
textDocument/signatureHelp | sim
textDocument/referências | sim
textDocument/documentHighlight | sim
textDocument/documentSymbol | sim
textDocument/formatação | sim
textDocument/rangeFormatting | sim
textDocument/onTypeFormatting |
textDocument/definição | sim
textDocument/códigoaction | sim
textDocument/codeLens |
codeLens/resolver |
textDocument/documentLink |
documentLink/resolver |
textDocument/renomear | sim

## <a name="get-started"></a>Introdução

> [!NOTE]
> A partir do Visual Studio 2017 versão 15,8, o suporte para o protocolo Common Language Server é incorporado ao Visual Studio. Se você tiver criado extensões LSP usando a versão do [VSIX do cliente do servidor de linguagem](https://marketplace.visualstudio.com/items?itemName=vsext.LanguageServerClientPreview) de visualização, elas deixarão de funcionar quando você atualizar para a versão 15,8 ou superior. Você precisará fazer o seguinte para colocar suas extensões LSP funcionando novamente:
>
> 1. Desinstale o VSIX de visualização do protocolo de servidor do Microsoft Visual Studio Language.
>
>    A partir da versão 15,8, cada vez que você executar uma atualização no Visual Studio, o VSIX de visualização será detectado e removido automaticamente.
>
> 2. Atualize a referência do NuGet para a versão mais recente sem visualização para [pacotes LSP](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client).
>
> 3. Remova a dependência do VSIX do protocolo de servidor do Microsoft Visual Studio Language no seu manifesto do VSIX.
>
> 4. Verifique se seu VSIX especifica o Visual Studio 2017 versão 15,8 Preview 3 como o limite inferior para o destino de instalação.
>
> 5. Recompilar e reimplantar.

### <a name="create-a-vsix-project"></a>Criar um projeto VSIX

Para criar uma extensão de serviço de idioma usando um servidor de linguagem baseado em LSP, primeiro verifique se você tem a carga de trabalho de **desenvolvimento de extensão do Visual Studio** instalada para sua instância do vs.

Em seguida, crie um novo projeto VSIX navegando até **arquivo**  >  **novo projeto** projeto  >  VSIX de extensibilidade do **Visual C#**  >    >  :

![Criar projeto VSIX](media/lsp-vsix-project.png)

### <a name="language-server-and-runtime-installation"></a>Servidor de idiomas e instalação em tempo de execução

Por padrão, as extensões criadas para dar suporte a servidores de linguagem baseados em LSP no Visual Studio não contêm os próprios servidores de linguagem ou os tempos de execução necessários para executá-los. Os desenvolvedores de extensão são responsáveis por distribuir os servidores de idiomas e os tempos de execução necessários. Há várias maneiras de fazer isso:

* Os servidores de idiomas podem ser inseridos no VSIX como arquivos de conteúdo.
* Crie um MSI para instalar o servidor de idioma e/ou tempos de execução necessários.
* Forneça instruções no Marketplace informando aos usuários como obter tempos de execução e servidores de idioma.

### <a name="textmate-grammar-files"></a>Arquivos de gramática de TextMate

O LSP não inclui especificações sobre como fornecer a colorização de texto para idiomas. Para fornecer a colorização personalizada para idiomas no Visual Studio, os desenvolvedores de extensão podem usar um arquivo de gramática TextMate. Para adicionar arquivos de gramática ou de tema personalizados, siga estas etapas:

1. Crie uma pasta denominada "gramáticas" dentro de sua extensão (ou pode ser qualquer nome que você escolher).

2. Dentro da pasta *gramáticas* , inclua quaisquer arquivos *\* . tmlanguage*, *\* . plist*, *\* . tmtheme* ou *\* . JSON* que você gostaria que forneçam a colorização personalizada.

   > [!TIP]
   > Um arquivo *. tmtheme* define como os escopos são mapeados para classificações do Visual Studio (chaves de cores nomeadas). Para obter orientação, você pode fazer referência ao arquivo global *. tmtheme* no diretório *% ProgramFiles (x86)% \ Microsoft Visual Studio \\ \<version> \\ \<SKU> \Common7\IDE\CommonExtensions\Microsoft\TextMate\Starterkit\Themesg* .

3. Crie um arquivo *. pkgdef* e adicione uma linha semelhante a esta:

    ```
    [$RootKey$\TextMate\Repositories]
    "MyLang"="$PackageFolder$\Grammars"
    ```

4. Clique com o botão direito do mouse nos arquivos e selecione **Propriedades**. Altere a ação de **compilação** para **conteúdo** e altere a propriedade **include in VSIX** para **true**.

Depois de concluir as etapas anteriores, uma pasta de *gramáticas* é adicionada ao diretório de instalação do pacote como uma fonte de repositório chamada "mylang" ("mylang" é apenas um nome para ambiguidade e pode ser qualquer cadeia de caracteres exclusiva). Todas as gramáticas (arquivos *. tmlanguage* ) e os arquivos de tema (arquivos *. tmtheme* ) nesse diretório são captados como possíveis e substituem as gramáticas internas fornecidas com TextMate. Se as extensões declaradas do arquivo de gramática corresponderem à extensão do arquivo que está sendo aberto, o TextMate entrará em.

## <a name="create-a-simple-language-client"></a>Criar um cliente de linguagem simples

### <a name="main-interface---ilanguageclient"></a>Interface principal- [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017&preserve-view=true)

Depois de criar seu projeto VSIX, adicione os seguintes pacotes NuGet ao seu projeto:

* [Microsoft. VisualStudio. LanguageServer. Client](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)

> [!NOTE]
> Quando você assume uma dependência do pacote NuGet depois de concluir as etapas anteriores, os pacotes Newtonsoft.Jse StreamJsonRpc são adicionados ao seu projeto também. Não **atualize esses pacotes, a menos que você tenha certeza de que essas novas versões serão instaladas na versão do Visual Studio que sua extensão tem como destino**. Os assemblies não serão incluídos em seu VSIX; em vez disso, eles serão selecionados no diretório de instalação do Visual Studio. Se você estiver fazendo referência a uma versão mais recente dos assemblies do que o que está instalado no computador de um usuário, sua extensão não funcionará.

Em seguida, você pode criar uma nova classe que implementa a interface [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017&preserve-view=true) , que é a interface principal necessária para os clientes de idioma que se conectam a um servidor de linguagem baseado em LSP.

Veja o exemplo a seguir:

```csharp
namespace MockLanguageExtension
{
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
        public string Name => "Bar Language Extension";

        public IEnumerable<string> ConfigurationSections => null;

        public object InitializationOptions => null;

        public IEnumerable<string> FilesToWatch => null;

        public event AsyncEventHandler<EventArgs> StartAsync;
        public event AsyncEventHandler<EventArgs> StopAsync;

        public async Task<Connection> ActivateAsync(CancellationToken token)
        {
            await Task.Yield();

            ProcessStartInfo info = new ProcessStartInfo();
            info.FileName = Path.Combine(Path.GetDirectoryName(Assembly.GetExecutingAssembly().Location), "Server", @"MockLanguageServer.exe");
            info.Arguments = "bar";
            info.RedirectStandardInput = true;
            info.RedirectStandardOutput = true;
            info.UseShellExecute = false;
            info.CreateNoWindow = true;

            Process process = new Process();
            process.StartInfo = info;

            if (process.Start())
            {
                return new Connection(process.StandardOutput.BaseStream, process.StandardInput.BaseStream);
            }

            return null;
        }

        public async Task OnLoadedAsync()
        {
            await StartAsync.InvokeAsync(this, EventArgs.Empty);
        }

        public Task OnServerInitializeFailedAsync(Exception e)
        {
            return Task.CompletedTask;
        }

        public Task OnServerInitializedAsync()
        {
            return Task.CompletedTask;
        }
    }
}
```

Os principais métodos que precisam ser implementados são [OnLoadedAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017&preserve-view=true) e [ActivateAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017&preserve-view=true). [OnLoadedAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017&preserve-view=true) é chamado quando o Visual Studio carregou sua extensão e seu servidor de idioma está pronto para ser iniciado. Nesse método, você pode invocar o delegado [StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017&preserve-view=true) imediatamente para sinalizar que o servidor de idioma deve ser iniciado ou pode fazer uma lógica adicional e invocar o [StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017&preserve-view=true) mais tarde. **Para ativar o servidor de idioma, você deve chamar StartAsync em algum momento.**

[ActivateAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017&preserve-view=true) é o método eventualmente invocado chamando o delegado [StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017&preserve-view=true) . Ele contém a lógica para iniciar o servidor de idioma e estabelecer conexão com ele. Um objeto de conexão que contém fluxos para gravação no servidor e leitura do servidor deve ser retornado. Todas as exceções geradas aqui são capturadas e exibidas para o usuário por meio de uma mensagem de barra de exibição no Visual Studio.

### <a name="activation"></a>Ativação

Depois que a sua classe de cliente de idioma for implementada, você precisará definir dois atributos para que ele defina como ele será carregado no Visual Studio e ativado:

```csharp
  [Export(typeof(ILanguageClient))]
  [ContentType("bar")]
```

### <a name="mef"></a>MEF

O Visual Studio usa [MEF](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md) (Managed Extensibility Framework) para gerenciar seus pontos de extensibilidade. O atributo de [exportação](/dotnet/api/system.componentmodel.composition.exportattribute) indica ao Visual Studio que essa classe deve ser coletada como um ponto de extensão e carregada no momento apropriado.

Para usar o MEF, você também deve definir o MEF como um ativo no manifesto do VSIX.

Abra seu designer de manifesto do VSIX e navegue até a guia **ativos** :

![Adicionar ativo de MEF](media/lsp-add-asset.png)

Clique em **novo** para criar um novo ativo:

![definir ativo de MEF](media/lsp-define-asset.png)

* **Tipo**: Microsoft. VisualStudio. MefComponent
* **Origem**: um projeto na solução atual
* **Projeto**: [seu projeto]

### <a name="content-type-definition"></a>Definição de tipo de conteúdo

Atualmente, a única maneira de carregar sua extensão de servidor de linguagem baseada em LSP é por tipo de conteúdo de arquivo. Ou seja, ao definir sua classe de cliente de idioma (que implementa [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017&preserve-view=true)), você precisará definir os tipos de arquivos que, quando abertos, farão com que sua extensão seja carregada. Se nenhum arquivo que corresponda ao tipo de conteúdo definido for aberto, a extensão não será carregada.

Isso é feito por meio da definição de uma ou mais `ContentTypeDefinition` classes:

```csharp
namespace MockLanguageExtension
{
    public class BarContentDefinition
    {
        [Export]
        [Name("bar")]
        [BaseDefinition(CodeRemoteContentDefinition.CodeRemoteContentTypeName)]
        internal static ContentTypeDefinition BarContentTypeDefinition;

        [Export]
        [FileExtension(".bar")]
        [ContentType("bar")]
        internal static FileExtensionToContentTypeDefinition BarFileExtensionDefinition;
    }
}
```

No exemplo anterior, uma definição de tipo de conteúdo é criada para arquivos que terminam na extensão de arquivo *. bar* . A definição de tipo de conteúdo recebe o nome "bar" e deve derivar de [CodeRemoteContentTypeName](/dotnet/api/microsoft.visualstudio.languageserver.client.coderemotecontentdefinition.coderemotecontenttypename?view=visualstudiosdk-2017&preserve-view=true).

Depois de adicionar uma definição de tipo de conteúdo, você pode definir quando carregar sua extensão de cliente de idioma na classe de cliente de idioma:

```csharp
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
    }
```

Adicionar suporte a servidores de idioma LSP não exige que você implemente seu próprio sistema de projeto no Visual Studio. Os clientes podem abrir um único arquivo ou uma pasta no Visual Studio para começar a usar seu serviço de linguagem. Na verdade, o suporte para servidores de idioma LSP foi projetado para funcionar apenas em cenários de arquivo/pasta abertos. Se um sistema de projeto personalizado for implementado, alguns recursos (como configurações) não funcionarão.

## <a name="advanced-features"></a>Recursos avançados

### <a name="settings"></a>Configurações

O suporte para configurações específicas do servidor de idioma personalizado está disponível, mas ainda está no processo de melhoria. As configurações são específicas ao que o servidor de linguagem dá suporte e geralmente controlam como o servidor de linguagem emite dados. Por exemplo, um servidor de idioma pode ter uma configuração para o número máximo de erros relatados. Os autores de extensão definem um valor padrão, que pode ser alterado por usuários para projetos específicos.

Siga estas etapas abaixo para adicionar suporte para configurações para sua extensão de serviço de idioma LSP:

1. Adicione um arquivo JSON (por exemplo, *MockLanguageExtensionSettings.js*) ao seu projeto que contém as configurações e seus valores padrão. Por exemplo:

    ```json
    {
        "foo.maxNumberOfProblems": -1
    }
    ```

2. Clique com o botão direito do mouse no arquivo JSON e selecione **Propriedades**. Altere a ação de **compilação** para "conteúdo" e a propriedade "incluir no VSIX" como **true**.

3. Implemente ConfigurationSections e retorne a lista de prefixos para as configurações definidas no arquivo JSON (em Visual Studio Code, isso mapearia para o nome da seção de configuração em package.jsem):

    ```csharp
    public IEnumerable<string> ConfigurationSections
    {
        get
        {
            yield return "foo";
        }
    }
    ```

4. Adicione um arquivo. pkgdef ao projeto (adicione um novo arquivo de texto e altere a extensão de arquivo para. pkgdef). O arquivo pkgdef deve conter estas informações:

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\[settings-name]]
    @="$PackageFolder$\[settings-file-name].json"
    ```

    Exemplo:

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\MockLanguageExtension]
    @="$PackageFolder$\MockLanguageExtensionSettings.json"
    ```

5. Clique com o botão direito do mouse no arquivo. pkgdef e selecione **Propriedades**. Altere a ação de **Build** para **conteúdo** e a propriedade **include in VSIX** como **true**.

6. Abra o arquivo *Source. Extension. vsixmanifest* e adicione um ativo na guia **ativo** :

   ![editar ativo VSPackage](media/lsp-add-vspackage-asset.png)

   * **Tipo**: Microsoft. VisualStudio. VSPackage
   * **Origem**: arquivo no sistema de arquivos
   * **Caminho**: [caminho para o arquivo *. pkgdef* ]

### <a name="user-editing-of-settings-for-a-workspace"></a>Edição do usuário de configurações para um espaço de trabalho

1. O usuário abre um espaço de trabalho que contém os arquivos que o servidor possui.
2. O usuário adiciona um arquivo na pasta *. vs* chamada *VSWorkspaceSettings.jsno*.
3. O usuário adiciona uma linha à *VSWorkspaceSettings.jsno* arquivo para uma configuração que o servidor fornece. Por exemplo:

    ```json
    {
        "foo.maxNumberOfProblems": 10
    }
    ```

### <a name="enable-diagnostics-tracing"></a>Habilitar o rastreamento de diagnóstico

O rastreamento de diagnóstico pode ser habilitado para gerar todas as mensagens entre o cliente e o servidor, o que pode ser útil ao depurar problemas. Para habilitar o rastreamento de diagnóstico, faça o seguinte:

1. Abra ou crie o arquivo de configurações de espaço de trabalho *VSWorkspaceSettings.jsem* (consulte "edição de usuário das configurações para um espaço de trabalho").
2. Adicione a seguinte linha no arquivo de configurações JSON:

```json
{
    "foo.trace.server": "Off"
}
```

Há três valores possíveis para o detalhamento de rastreamento:

* "Off": rastreamento desativado completamente
* "Messages": o rastreamento está ativado, mas apenas o nome do método e a ID da resposta são rastreados.
* "Verbose": rastreamento ativado; a mensagem RPC inteira é rastreada.

Quando o rastreamento é ativado, o conteúdo é gravado em um arquivo no diretório *%Temp%\VisualStudio\LSP* . O log segue o formato de nomenclatura *[LanguageClientName]-[carimbo de data/hora]. log*. Atualmente, o rastreamento só pode ser habilitado para cenários de pasta aberta. Abrir um único arquivo para ativar um servidor de idioma não tem suporte para rastreamento de diagnóstico.

### <a name="custom-messages"></a>Mensagens personalizadas

Há APIs em vigor para facilitar a passagem de mensagens e o recebimento de mensagens do servidor de idiomas que não fazem parte do protocolo de servidor de idioma padrão. Para lidar com mensagens personalizadas, implemente a interface [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true) em sua classe de cliente de idioma. A biblioteca [vs-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) é usada para transmitir mensagens personalizadas entre o cliente de idioma e o servidor de idioma. Como sua extensão de cliente de idioma LSP é assim como qualquer outra extensão do Visual Studio, você pode optar por adicionar recursos adicionais (que não têm suporte pelo LSP) ao Visual Studio (usando outras APIs do Visual Studio) em sua extensão por meio de mensagens personalizadas.

#### <a name="receive-custom-messages"></a>Receber mensagens personalizadas

Para receber mensagens personalizadas do servidor de idioma, implemente a propriedade [CustomMessageTarget](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.custommessagetarget?view=visualstudiosdk-2017&preserve-view=true) em [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true) e retorne um objeto que saiba como lidar com suas mensagens personalizadas. Exemplo abaixo:

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public object CustomMessageTarget
    {
        get;
        set;
    }

    public class CustomTarget
    {
        public void OnCustomNotification(JToken arg)
        {
            // Provide logic on what happens OnCustomNotification is called from the language server
        }

        public string OnCustomRequest(string test)
        {
            // Provide logic on what happens OnCustomRequest is called from the language server
        }
    }
}
```

#### <a name="send-custom-messages"></a>Enviar mensagens personalizadas

Para enviar mensagens personalizadas para o servidor de idioma, implemente o método [AttachForCustomMessageAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.attachforcustommessageasync?view=visualstudiosdk-2017&preserve-view=true) em [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true). Esse método é invocado quando o servidor de idioma é iniciado e está pronto para receber mensagens. Um objeto [JsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/src/StreamJsonRpc/JsonRpc.cs) é passado como um parâmetro, que você pode então manter para enviar mensagens para o servidor de idioma usando APIs do [vs-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) . Exemplo abaixo:

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public async Task AttachForCustomMessageAsync(JsonRpc rpc)
    {
        await Task.Yield();

        this.customMessageRpc = rpc;
    }

    public async Task SendServerCustomNotification(object arg)
    {
        await this.customMessageRpc.NotifyWithParameterObjectAsync("OnCustomNotification", arg);
    }

    public async Task<string> SendServerCustomMessage(string test)
    {
        return await this.customMessageRpc.InvokeAsync<string>("OnCustomRequest", test);
    }
}
```

### <a name="middle-layer"></a>Camada intermediária

Às vezes, um desenvolvedor de extensão pode querer interceptar mensagens de LSP enviadas e recebidas do servidor de idioma. Por exemplo, um desenvolvedor de extensão pode querer alterar o parâmetro de mensagem enviado para uma mensagem LSP específica ou modificar os resultados retornados do servidor de idioma para um recurso de LSP (por exemplo, conclusões). Quando isso for necessário, os desenvolvedores de extensão poderão usar a API MiddleLayer para interceptar mensagens LSP.

Cada mensagem LSP tem sua própria interface de camada intermediária para interceptação. Para interceptar uma mensagem específica, crie uma classe que implemente a interface de camada intermediária para essa mensagem. Em seguida, implemente a interface [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true) em sua classe de cliente de linguagem e retorne uma instância de seu objeto na propriedade [MiddleLayer](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.middlelayer?view=visualstudiosdk-2017&preserve-view=true) . Exemplo abaixo:

```csharp
public class MockLanguageClient: ILanguageClient, ILanguageClientCustomMessage
{
    public object MiddleLayer => MiddleLayerProvider.Instance;

    private class MiddleLayerProvider : ILanguageClientWorkspaceSymbolProvider
    {
        internal readonly static MiddleLayerProvider Instance = new MiddleLayerProvider();

        private MiddleLayerProvider()
        {
        }

        public async Task<SymbolInformation[]> RequestWorkspaceSymbols(WorkspaceSymbolParams param, Func<WorkspaceSymbolParams, Task<SymbolInformation[]>> sendRequest)
        {
            // Send along the request as given
            SymbolInformation[] symbols = await sendRequest(param);

            // Only return symbols that are "files"
            return symbols.Where(sym => string.Equals(new Uri(sym.Location.Uri).Scheme, "file", StringComparison.OrdinalIgnoreCase)).ToArray();
        }
    }
}
```

O recurso de camada intermediária ainda está em desenvolvimento e ainda não é abrangente.

## <a name="sample-lsp-language-server-extension"></a>Extensão de servidor de idioma LSP de exemplo

Para ver o código-fonte de uma extensão de exemplo usando a API de cliente LSP no Visual Studio, consulte exemplo de [LSP](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/LanguageServerProtocol)VSSDK-Extensibility-Samples.

## <a name="faq"></a>Perguntas frequentes

**Gostaria de criar um sistema de projeto personalizado para complementar meu servidor de linguagem LSP para oferecer suporte mais avançado a recursos no Visual Studio, como posso fazer isso?**

O suporte para servidores de linguagem baseados em LSP no Visual Studio depende do [recurso abrir pasta](https://devblogs.microsoft.com/visualstudio/open-any-folder-with-visual-studio-15-preview/) e foi projetado para não exigir um sistema de projeto personalizado. Você pode criar seu próprio sistema de projeto personalizado seguindo as instruções [aqui](https://github.com/Microsoft/VSProjectSystem), mas alguns recursos, como configurações, podem não funcionar. A lógica de inicialização padrão para servidores de idioma LSP é passar o local da pasta raiz da pasta que está sendo aberta no momento, portanto, se você usar um sistema de projeto personalizado, talvez seja necessário fornecer uma lógica personalizada durante a inicialização para garantir que o servidor de linguagem possa ser iniciado corretamente.

**Como fazer adicionar suporte a depurador?**

Forneceremos suporte para o protocolo de [depuração comum](https://code.visualstudio.com/docs/extensionAPI/api-debugging) em uma versão futura.

**Se já houver um serviço de linguagem com suporte do VS instalado (por exemplo, JavaScript), ainda poderei instalar uma extensão de servidor de idioma LSP que oferece recursos adicionais (como resumir)?**

Sim, mas nem todos os recursos funcionarão corretamente. O objetivo final das extensões de servidor de linguagem LSP é habilitar os serviços de linguagem não suportados nativamente pelo Visual Studio. Você pode criar extensões que oferecem suporte adicional usando servidores de idioma LSP, mas alguns recursos (como o IntelliSense) não serão uma experiência tranqüila. Em geral, é recomendável que as extensões de servidor de idioma LSP sejam usadas para fornecer novas experiências de linguagem, não estendendo aquelas existentes.

**Onde publicar meu VSIX do servidor de idioma LSP concluído?**

Consulte as instruções do Marketplace [aqui](walkthrough-publishing-a-visual-studio-extension.md).

## <a name="see-also"></a>Confira também

- [Adicionar suporte para outras linguagens ao editor do Visual Studio](../ide/adding-visual-studio-editor-support-for-other-languages.md)
