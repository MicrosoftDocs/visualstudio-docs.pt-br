---
title: Adicionando uma extensão do protocolo de idioma do servidor | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 52f12785-1c51-4c2c-8228-c8e10316cd83
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7f2710693c7dae7c4238f9f31fbe8065d6864a19
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672958"
---
# <a name="add-a-language-server-protocol-extension"></a>Adicionar uma extensão de protocolo de idioma do servidor

A linguagem servidor protocolo LSP () é um protocolo comum, na forma de v 2.0 RPC de JSON, usada para fornecer recursos de serviço para vários editores de código de idioma. Usando o protocolo, os desenvolvedores podem escrever um servidor único idioma para fornecer recursos de serviço como o IntelliSense, diagnósticos de erros de linguagem, localizar todas as referências, etc., para vários editores de código que dão suporte ao LSP. Tradicionalmente, os serviços de linguagem no Visual Studio podem ser adicionados pelo usando arquivos de gramática TextMate para fornecer funcionalidades básicas, como realce de sintaxe, ou escrevendo em serviços de linguagem personalizados usando o conjunto completo de APIs de extensibilidade do Visual Studio para Fornece dados mais avançados. Agora, o suporte para o LSP que oferece uma terceira opção.

![serviço de protocolo de servidor de linguagem no Visual Studio](media/lsp-service-in-VS.png)

## <a name="language-server-protocol"></a>Language Server Protocol

![implementação de protocolo do servidor de linguagem](media/lsp-implementation.png)

Este artigo descreve como criar uma extensão do Visual Studio que usa um servidor de linguagem baseada em LSP. Ele pressupõe que você já tenha desenvolvido um servidor de linguagem baseada em LSP e quiser integrá-la no Visual Studio.

Para obter suporte no Visual Studio, servidores de idioma podem se comunicar com o cliente (Visual Studio) por meio de qualquer mecanismo de transmissão de fluxo com base, por exemplo:

* Fluxos de entrada/saída padrão
* Pipes nomeados
* Soquetes (TCP somente)

Serviços de linguagem integrado que não fazem parte do produto do Visual Studio é a intenção da LSP e suporte para ele no Visual Studio. Ele não se destina para estender os serviços de linguagem existentes (como c#) no Visual Studio. Para estender idiomas existentes, consulte o guia de extensibilidade do serviço de linguagem (por exemplo, o [plataforma do compilador .NET "Roslyn"](../extensibility/dotnet-compiler-platform-roslyn-extensibility.md)).

Para obter mais informações sobre o protocolo em si, consulte a documentação [aqui](https://github.com/Microsoft/language-server-protocol).

Para obter mais informações sobre como criar um servidor de linguagem de exemplo ou como integrar um servidor existente de linguagem no Visual Studio Code, consulte a documentação [aqui](https://code.visualstudio.com/docs/extensions/example-language-server).

## <a name="language-server-protocol-features-supported"></a>Recursos de protocolo do servidor de idioma com suporte

Os seguintes recursos LSP até agora têm suporte no Visual Studio:

Mensagem | Tem suporte no Visual Studio
--- | ---
inicializar | sim
inicializado | sim
desligamento | sim
sair | sim
$/ cancelRequest | sim
janela/showMessage | sim
window/showMessageRequest | sim
janela/logMessage | sim
/ evento de telemetria |
cliente/registerCapability |
cliente/unregisterCapability |
workspace/didChangeConfiguration | sim
workspace/didChangeWatchedFiles | sim
espaço de trabalho/símbolo | sim
workspace/executeCommand | sim
espaço de trabalho/applyEdit | sim
textDocument/publishDiagnostics | sim
textDocument/didOpen | sim
textDocument/didChange | sim
textDocument/willSave |
textDocument/willSaveWaitUntil |
textDocument/didSave | sim
textDocument/didClose | sim
textDocument/conclusão | sim
conclusão/resolver | sim
Passe o mouse/textDocument | sim
textDocument/signatureHelp | sim
textDocument/referências | sim
textDocument/documentHighlight | sim
textDocument/documentSymbol | sim
textDocument/formatação | sim
textDocument/rangeFormatting | sim
textDocument/onTypeFormatting |
textDocument/definição | sim
textDocument/codeAction | sim
textDocument/codeLens |
codeLens/resolve |
textDocument/documentLink |
documentLink/resolve |
textDocument/rename | sim

## <a name="getting-started"></a>Introdução

> [!NOTE]
> Começando com o Visual Studio 15.8 Preview 3, suporte para o protocolo de servidor de linguagem comum é incorporada ao Visual Studio.  Se você compilou usando nossa visualização de extensões LSP [VSIX de cliente do servidor de linguagem](https://marketplace.visualstudio.com/items?itemName=vsext.LanguageServerClientPreview) versão, eles deixarão de funcionar depois que a que você tiver atualizado para 15,8 Preview 3 ou superior.  Você precisará fazer o seguinte para obter suas extensões LSP volte a funcionar:
>
> 1. Desinstale o Microsoft Visual Studio Language Server protocolo Preview VSIX.  Começando com 15,8 visualização 4, toda vez que você executa uma atualização no Visual Studio, podemos detectará automaticamente e remover a visualização VSIX para você durante o processo de atualização.
>
> 2. Atualize sua referência Nuget para a última versão de não-preview para [pacotes LSP](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client).
>
> 3. Remova a dependência para o Microsoft Language servidor protocolo visualização VSIX do Visual Studio em seu manifesto do VSIX.
>
> 4. Verifique se que seu VSIX Especifica 3 do Visual Studio 15.8 Preview como um limite inferior para o destino de instalação.
>
> 5. Recompile e implante novamente.

### <a name="create-a-vsix-project"></a>Crie um projeto VSIX

Para criar uma extensão de serviço de linguagem usando um servidor de linguagem baseada em LSP, primeiro verifique se você tem o **desenvolvimento de extensões do Visual Studio** carga de trabalho instalada para sua instância do VS.

Em seguida, crie um novo VSIXProject em branco, navegando até **arquivo** > **novo projeto** > **Visual c#**  >   **Extensibilidade** > **projeto VSIX**:

![criar um projeto vsix](media/lsp-vsix-project.png)

### <a name="language-server-and-runtime-installation"></a>Instalação de servidor e o tempo de execução de idioma

Por padrão, as extensões criadas para oferecer suporte a servidores de linguagem baseada em LSP no Visual Studio não conterá os servidores de linguagem propriamente ditos ou os tempos de execução necessários para executá-los. Os desenvolvedores de extensão serão responsáveis por distribuir os servidores de linguagem e os tempos de execução necessários. Há várias maneiras de fazer isso:

* Servidores de idioma podem ser inseridos no VSIX como arquivos de conteúdo.
* Criar um MSI para instalar o servidor de linguagem e/ou necessárias tempos de execução.
* Fornecem instruções sobre usuários do Marketplace informando como obter tempos de execução e linguagem de servidores.

### <a name="textmate-grammar-files"></a>Arquivos de gramática TextMate

O LSP não inclui a especificação sobre como fornecer a colorização do texto para idiomas. Para fornecer personalizada colorização para linguagens no Visual Studio, os desenvolvedores de extensão podem usar um arquivo de gramática TextMate. Para adicionar arquivos de tema ou gramática TextMate personalizados, siga estas etapas:

1. Crie uma pasta chamada "Gramáticas" dentro de sua extensão (ou pode ser qualquer nome que você escolhe).

2. Dentro de *gramáticas* pasta, incluir qualquer  *\*.tmlanguage*,  *\*. plist*,  *\*. tmtheme*, ou  *\*. JSON* arquivos que você gostaria que fornece a colorização personalizada.

3. Clique com botão direito nos arquivos e selecione **propriedades**. Alterar o **construir** ação a ser **conteúdo** e o **incluir em VSIX** propriedade como true.

4. Criar uma *pkgdef* arquivo e adicione uma linha semelhante a esta:

   ```xml
   [$RootKey$\TextMate\Repositories]
   "MyLang"="$PackageFolder$\Grammars"
   ```

5. Clique com botão direito nos arquivos e selecione **propriedades**. Alterar o **construir** ação a ser **conteúdo** e o **incluir em VSIX** propriedade como true.

Depois de concluir as etapas anteriores, uma *gramáticas* pasta foi adicionada à instalação do pacote diretório como uma fonte de repositório chamado 'MyLang' ('MyLang' é apenas um nome para a desambiguação e pode ser qualquer cadeia de caracteres exclusiva). Todas as gramáticas (*.tmlanguage* arquivos) e arquivos de tema (*. tmtheme* arquivos) nesse diretório são escolhidas como potenciais e substituem as gramáticas internos fornecidas com TextMate. Se as extensões declarado do arquivo de gramática corresponde à extensão do arquivo que está sendo aberto, TextMate será etapa.

## <a name="create-a-simple-language-client"></a>Criar um cliente de uma linguagem simples

### <a name="main-interface---ilanguageclientdotnetapimicrosoftvisualstudiolanguageserverclientilanguageclientviewvisualstudiosdk-2017"></a>Interface principal - [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)

Depois de criar seu projeto VSIX, adicione os seguintes pacotes NuGet ao seu projeto:

* [Microsoft.VisualStudio.LanguageServer.Client](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)

> [!NOTE]
> Quando você usar uma dependência no pacote NuGet depois de concluir as etapas anteriores, os pacotes do newtonsoft. JSON e StreamJsonRpc são adicionados ao seu projeto também. **Não atualizar esses pacotes, a menos que você tiver certeza de que essas novas versões serão instaladas na versão do Visual Studio que sua extensão é direcionada**. Os assemblies não serão incluídos no seu VSIX – em vez disso, eles serão ser retirados do diretório de instalação do Visual Studio. Se você está fazendo referência a uma versão mais recente dos assemblies que o que é instalado no computador do usuário, a extensão *não funcionará*.

Em seguida, você pode criar uma nova classe que implementa o [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017) interface, a interface principal necessário para clientes de linguagem se conectar ao servidor linguagem baseada em LSP.

A seguir está um exemplo:

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

        public async Task OnServerInitializeFailedAsync(Exception e)
        {
            return Task.CompletedTask;
        }

        public async Task OnServerInitializedAsync()
        {
            return Task.CompletedTask;
        }
    }
}
```

São os principais métodos que precisam ser implementados [OnLoadedAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017) e [ActivateAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017). [OnLoadedAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017) é chamado quando o Visual Studio carregou a sua extensão e o servidor de linguagem está pronto para ser iniciado. Nesse método, você pode invocar o [StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017) delegado imediatamente para sinalizar que o servidor de idioma deve ser iniciado, ou você pode fazer uma lógica adicional e invocar [StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017) mais tarde. **Para ativar o servidor de linguagem, você deve chamar StartAsync em algum momento.**

[ActivateAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017) é o método invocado, eventualmente, chamando o [StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017) delegar; ele contém a lógica para iniciar o servidor de linguagem e estabelecer conexão a ele. Um objeto de conexão que contém fluxos para gravação para o servidor e a leitura do servidor deve ser retornado. Todas as exceções geradas aqui são capturadas e exibidas ao usuário por meio de uma mensagem de barra de informações no Visual Studio.

### <a name="activation"></a>Ativação

Depois que sua classe de cliente de linguagem é implementada, você precisará definir dois atributos para definir como ele será carregado no Visual Studio e ativado:

```csharp
  [Export(typeof(ILanguageClient))]
  [ContentType("bar")]
```

### <a name="mef"></a>MEF

O Visual Studio usa [MEF](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md) (Managed Extensibility Framework) para gerenciar seus pontos de extensibilidade. O [exportar](/dotnet/api/system.componentmodel.composition.exportattribute) atributo indica para o Visual Studio que essa classe deve ser escolhida como um ponto de extensão e carregada no momento apropriado.

Para usar o MEF, você também deve definir o MEF como um ativo no manifesto do VSIX.

Abra o designer de manifesto do VSIX e navegue até a **ativos** guia:

![Adicionar ativo MEF](media/lsp-add-asset.png)

Clique em novo para criar um novo ativo:

![definir o ativo MEF](media/lsp-define-asset.png)

* **Type**: Microsoft.VisualStudio.MefComponent
* **Origem**: um projeto na solução atual
* **Projeto**: [seu projeto]

### <a name="content-type-definition"></a>Definição de tipo de conteúdo

Atualmente, a única maneira de carregar sua extensão de servidor de linguagem baseada em LSP é por tipo de conteúdo do arquivo. Ou seja, ao definir sua classe de cliente de linguagem (que implementa [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)), você precisará definir os tipos de arquivos que, quando aberto, fará com que a sua extensão carregar. Se nenhum arquivo que correspondem ao seu tipo de conteúdo definido é aberto, a sua extensão não será carregada.

Isso é feito por meio da definição de uma ou mais classes de ContentTypeDefinition:

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

No exemplo anterior, uma definição de tipo de conteúdo é criada para arquivos que terminam em *.bar* extensão de arquivo. A definição de tipo de conteúdo é dada a barra"name" e **devem** derivam [CodeRemoteContentTypeName](/dotnet/api/microsoft.visualstudio.languageserver.client.coderemotecontentdefinition.coderemotecontenttypename?view=visualstudiosdk-2017).

Depois de adicionar uma definição de tipo de conteúdo, em seguida, você pode definir quando carregar sua extensão de cliente do idioma na classe de cliente de linguagem:

```csharp
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
    }
```

Adicionar suporte para servidores de linguagem LSP não exige que você implemente seu próprio sistema de projeto no Visual Studio. Os clientes podem abrir um único arquivo ou uma pasta no Visual Studio para começar a usar o serviço de linguagem. Na verdade, o suporte para servidores de linguagem LSP foi projetado para funcionar apenas em cenários de arquivo/pasta aberta. Se um sistema de projeto personalizado for implementado, alguns recursos (como configurações) não funcionará.

## <a name="advanced-features"></a>Recursos avançados

### <a name="settings"></a>Configurações

Suporte para configurações personalizadas do servidor-específico do idioma está disponível, mas ele ainda está sendo aprimorados. Configurações são específicas para o que o servidor de linguagem dá suporte a e geralmente controlam como o servidor de linguagem emite os dados. Por exemplo, um servidor de idioma pode ter uma configuração para o número máximo de erros relatados. Os autores de extensão seriam definir um valor padrão, que pode ser alterado pelos usuários para projetos específicos.

Siga as etapas abaixo para adicionar suporte para as configurações para sua extensão de serviço de linguagem LSP:

1. Adicione um arquivo JSON (por exemplo, *MockLanguageExtensionSettings.json*) em seu projeto que contém as configurações e seus valores padrão. Por exemplo:

   ```json
   {
    "foo.maxNumberOfProblems": -1
   }
   ```
2. Clique com botão direito no arquivo JSON e selecione **propriedades**. Alterar o **Build** ação como "Content" e o "incluir em VSIX' propriedade como true.

3. Implementar ConfigurationSections e retornar a lista de prefixos para as configurações definidas no arquivo JSON (no Visual Studio Code, ele seria mapeado para o nome da seção de configuração em Package. JSON):

   ```csharp
   public IEnumerable<string> ConfigurationSections
   {
      get
      {
          yield return "foo";
      }
   }
   ```
4. Adicionar um arquivo. pkgdef ao projeto (Adicionar novo arquivo de texto e altere a extensão de arquivo para. pkgdef). O arquivo pkgdef deve conter essas informações:

   ```xml
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\[settings-name]]
    @="$PackageFolder$\[settings-file-name].json"
   ```

5. Clique com o botão direito no arquivo. pkgdef e selecione **propriedades**. Alterar o **construir** ação a ser **conteúdo** e o **incluir em VSIX** propriedade como true.

6. Abra o *vsixmanifest* arquivo e adicione um ativo na **ativo** guia:

   ![Editar o ativo de vspackage](media/lsp-add-vspackage-asset.png)

   * **Tipo**: VSPackage
   * **Origem**: o arquivo no sistema de arquivos
   * **Caminho**: [caminho para seu *pkgdef* arquivo]

### <a name="user-editing-of-settings-for-a-workspace"></a>Usuário de edição de configurações para um espaço de trabalho

1. Usuário abre um espaço de trabalho que contém arquivos de que seu servidor possui.
2. Usuário adiciona um arquivo na *. VS* pasta chamada *Vsworkspacesettings*.
3. O usuário adiciona uma linha para o *Vsworkspacesettings* arquivo para uma configuração de servidor fornece. Por exemplo:

   ```json
   {
    "foo.maxNumberOfProblems": 10
   }
   ```
   ### <a name="enabling-diagnostics-tracing"></a>Habilitando o rastreamento de diagnóstico
   Rastreamento de diagnóstico pode ser habilitado para todas as mensagens entre o cliente e servidor, que pode ser útil ao depurar problemas de saída.  Para habilitar o rastreamento de diagnóstico, faça o seguinte:

4. Abra ou crie o arquivo de configurações do espaço de trabalho *Vsworkspacesettings* (consulte "Usuário de edição de configurações para um espaço de trabalho").
5. Adicione a seguinte linha no arquivo de configurações de json:

```json
{
    "foo.trace.server": "Off"
}
```

Há três valores possíveis para o detalhamento do rastreamento:
* "Desativado": o rastreamento seja completamente desativado
* "Messages": rastreamento ativado mas a ID de nome e a resposta do método somente é rastreada.
* "Detalhado": rastreamento ativado; a mensagem inteira de rpc é rastreada.

Quando o rastreamento está ativado o conteúdo é gravado em um arquivo a *%temp%\VisualStudio\LSP* directory.  O log segue o formato de nomenclatura *[LanguageClientName]-. [carimbo de data/hora] log*.  Atualmente, o rastreamento pode ser habilitado somente para cenários de abrir pasta.  Abertura de um único arquivo para ativar um servidor de linguagem não tem suporte de rastreamento de diagnóstico.

### <a name="custom-messages"></a>Mensagens personalizadas

Existem APIs em vigor para facilitar a passagem de mensagens para e receber mensagens do servidor de linguagem que não fazem parte do protocolo do servidor de idioma padrão. Para lidar com mensagens personalizadas, implementar [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017) interface em sua classe de cliente de linguagem. [VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) biblioteca é usada para transmitir mensagens personalizadas entre seu cliente de linguagem e o servidor de linguagem. Como sua extensão do cliente de linguagem LSP é assim como qualquer outra extensão do Visual Studio, você pode decidir adicionar recursos adicionais (que não têm suporte pelo LSP) para o Visual Studio (usando outras APIs do Visual Studio) em sua extensão por meio de mensagens personalizadas.

#### <a name="receiving-custom-messages"></a>Recebendo mensagens personalizadas

Para receber mensagens personalizadas do servidor de linguagem, implementar o [CustomMessageTarget](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.custommessagetarget?view=visualstudiosdk-2017) propriedade [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017) e retornar um objeto que sabe como lidar com suas mensagens personalizadas . Exemplo abaixo:

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

#### <a name="sending-custom-messages"></a>Enviando mensagens personalizadas

Para enviar mensagens personalizadas para o servidor de linguagem, implementar o [AttachForCustomMessageAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.attachforcustommessageasync?view=visualstudiosdk-2017) método [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017). Esse método é invocado quando o servidor de linguagem é iniciado e pronto para receber mensagens. Um [JsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/src/StreamJsonRpc/JsonRpc.cs) objeto é passado como um parâmetro, que, em seguida, você pode manter para enviar mensagens para o servidor de idioma utilizando [StreamJsonRpc VS](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) APIs. Exemplo abaixo:

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

Às vezes, um desenvolvedor de extensão poderá interceptar LSP mensagens enviadas e recebidas do servidor de linguagem. Por exemplo, um desenvolvedor de extensão pode querer alterar o parâmetro da mensagem enviado para uma determinada mensagem LSP ou modificar os resultados retornados do servidor de idioma para um recurso LSP (por exemplo, preenchimentos). Quando isso for necessário, os desenvolvedores de extensão podem usar a API de MiddleLayer para interceptar mensagens LSP.

Cada mensagem LSP tem sua própria interface de camada intermediária para interceptação. Para interceptar uma mensagem específica, crie uma classe que implementa a interface de camada intermediária para a mensagem. Em seguida, implemente a [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017) em sua classe de cliente do idioma da interface e retornar uma instância do seu objeto na [MiddleLayer](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.middlelayer?view=visualstudiosdk-2017) propriedade. Exemplo abaixo:

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

O recurso de camada intermediária está ainda em desenvolvimento e não ainda abrangente.

## <a name="sample-lsp-language-server-extension"></a>Extensão do servidor de linguagem do exemplo LSP

Para ver o código-fonte de uma extensão de exemplo usando a API do cliente LSP no Visual Studio, consulte exemplos de extensibilidade de VSSDK [exemplo LSP](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/LanguageServerProtocol).

## <a name="faq"></a>Perguntas Frequentes

**Eu gostaria de criar um sistema de projeto personalizado para complementar o meu servidor de linguagem LSP para oferecer suporte a recursos mais avançado no Visual Studio, como eu faço para fazer isso?**

Suporte para servidores de linguagem baseada em LSP no Visual Studio depende de [recurso Abrir pasta](https://blogs.msdn.microsoft.com/visualstudio/2016/04/12/open-any-folder-with-visual-studio-15-preview/) e foi projetado especificamente para não exigir um sistema de projeto personalizado. Você pode criar seu próprio sistema de projeto personalizado seguindo as instruções [aqui](https://github.com/Microsoft/VSProjectSystem), mas alguns recursos, como configurações, podem não funcionar. A lógica de inicialização padrão para servidores de linguagem LSP é passar o local da pasta raiz da pasta que está sendo aberto no momento, portanto, se você usar um sistema de projeto personalizado, você precisa fornecer lógica personalizada durante a inicialização para garantir que seu servidor de linguagem pode inicie corretamente.

**Como adicionar suporte do depurador?**

Forneceremos suporte para o [comuns de depuração protocolo](https://code.visualstudio.com/docs/extensionAPI/api-debugging) em uma versão futura.

**Se já houver um VS idioma com suporte serviço instalado (por exemplo, JavaScript), eu ainda poderá instalar uma extensão do servidor de linguagem LSP que oferece recursos adicionais (por exemplo, linting)?**

Sim, mas nem todos os recursos funcionará corretamente. O objetivo final para extensões de servidor de linguagem LSP é habilitar os serviços de linguagem não compatível nativamente com o Visual Studio. Você pode criar extensões que oferecem suporte adicional usando servidores de linguagem LSP, mas alguns recursos (como o IntelliSense) não será uma experiência positiva. Em geral, é aconselhável que as extensões de servidor de linguagem LSP sejam usados para fornecer novas experiências de linguagem, não estender os existentes.

**Onde posso publicar meu servidor de linguagem LSP concluído VSIX?**

Consulte as instruções do Marketplace [aqui](walkthrough-publishing-a-visual-studio-extension.md).
