---
title: Publicar a extensão usando a linha de comando
ms.date: 07/12/2018
ms.topic: how-to
helpviewer_keywords:
- publishing extensions
- extension, publishing
ms.assetid: 6ff9efc4-919d-4071-a80d-6dbdd2ceb2f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5108f4afa382c00376424432d2086f0494e34a03
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904674"
---
# <a name="walkthrough-publishing-a-visual-studio-extension-via-command-line"></a>Walkthrough: publicando uma extensão do Visual Studio via linha de comando

Este tutorial mostra como publicar uma extensão do Visual Studio para o Visual Studio Marketplace usando a linha de comando. Quando você adiciona sua extensão ao Marketplace, os desenvolvedores podem usar a caixa de diálogo [**extensões e atualizações**](../ide/finding-and-using-visual-studio-extensions.md) para procurar por extensões novas e atualizadas.

VsixPublisher.exe é a ferramenta de linha de comando para publicar extensões do Visual Studio no Marketplace. Ele pode ser acessado a partir de $ {VSInstallDir} \VSSDK\VisualStudioIntegration\Tools\Bin\VsixPublisher.exe. Os comandos disponíveis nesta ferramenta são: **Publish**, **createpublicarer**, **deletePublisher**, **deleteExtension**, **login**, **logout**.

## <a name="commands"></a>Comandos

### <a name="publish"></a>Publicar

Publica uma extensão para o Marketplace. A extensão pode ser um VSIX, um arquivo exe/msi ou um link. Se a extensão já existir com a mesma versão, ela substituirá a extensão. Se a extensão ainda não existir, ela criará uma nova extensão.

|Opções de comando |Descrição |
|---------|---------|
|carga (obrigatório) | Um caminho para a carga a ser publicada ou um link a ser usado como "URL mais informações". |
|publishManifest (obrigatório) | Caminho para o arquivo de manifesto de publicação a ser usado. |
|ignoreWarnings | Lista de avisos a serem ignorados ao publicar uma extensão. Esses avisos são mostrados como mensagens de linha de comando ao publicar uma extensão. (por exemplo, "VSIXValidatorWarning01, VSIXValidatorWarning02")
|personalAccessToken | PAT (token de acesso pessoal) usado para autenticar o Publicador. Se não for fornecido, o PAT será adquirido dos usuários conectados. |

```
VsixPublisher.exe publish -payload "{path to vsix}" -publishManifest "{path to vs-publish.json}" -ignoreWarnings "VSIXValidatorWarning01,VSIXValidatorWarning02"
```

### <a name="createpublisher"></a>CreatePublisher

Cria um Publicador no Marketplace. Também registra o Publicador no computador para futuras ações (por exemplo, excluir/publicar uma extensão).

|Opções de comando |Descrição |
|---------|---------|
|displayName (obrigatório) | Nome de exibição do Publicador. |
|PublisherName (obrigatório) | O nome do Publicador (por exemplo, o identificador). |
|personalAccessToken (obrigatório) | Token de acesso pessoal que é usado para autenticar o Publicador. |
|shortDescription | Uma breve descrição do Publicador (não um arquivo). |
|longDescription | Uma descrição longa do Publicador (não um arquivo). |

```
VsixPublisher.exe createPublisher -publisherName "{Publisher Name}" -displayName "{Publisher Display Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deletepublisher"></a>deletePublisher

Exclui um Publicador no Marketplace.

|Opções de comando |Descrição |
|---------|---------|
|PublisherName (obrigatório) | O nome do Publicador (por exemplo, o identificador). |
|personalAccessToken (obrigatório) | Token de acesso pessoal que é usado para autenticar o Publicador. |

```
VsixPublisher.exe deletePublisher -publisherName "{Publisher Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deleteextension"></a>deleteExtension

Exclui uma extensão do Marketplace.

|Opções de comando |Descrição |
|---------|---------|
|ExtensionName (obrigatório) | O nome da extensão a ser excluída. |
|PublisherName (obrigatório) | O nome do Publicador (por exemplo, o identificador). |
|personalAccessToken | Token de acesso pessoal que é usado para autenticar o Publicador. Se não for fornecido, o Pat será adquirido dos usuários conectados. |

```
VsixPublisher.exe deleteExtension -extensionName "{Extension Name}" -publisherName "{Publisher Name}"
```

### <a name="login"></a>login

Registra um Publicador no computador.

|Opções de comando |Descrição |
|---------|---------|
|personalAccessToken (obrigatório | Token de acesso pessoal que é usado para autenticar o Publicador. |
|PublisherName (obrigatório) | O nome do Publicador (por exemplo, o identificador). |
|substituir | Especifica que qualquer Publicador existente deve ser substituído pelo novo token de acesso pessoal. |

```
VsixPublisher.exe login -personalAccessToken "{Personal Access Token}" -publisherName "{Publisher Name}"
```

### <a name="logout"></a>logout

Registra um Publicador fora do computador.

|Opções de comando |Descrição |
|---------|---------|
|PublisherName (obrigatório) | O nome do Publicador (por exemplo, o identificador). |
|ignoreMissingPublisher | Especifica que a ferramenta não deve ser erro se o Publicador especificado ainda não estiver conectado. |

```
VsixPublisher.exe logout -publisherName "{Publisher Name}"
```

## <a name="publishmanifest-file"></a>arquivo publishManifest

Um arquivo publishManifest é usado pelo comando **Publish** . Ele representa todos os metadados sobre a extensão que o Marketplace precisa saber. Se a extensão que está sendo carregada for de uma extensão do VSIX, a propriedade "Identity" só deverá ter o conjunto "internalName". Isso ocorre porque o restante das propriedades de "identidade" pode ser gerado a partir do arquivo vsixmanifest. Se a extensão for uma MSI/exe ou uma extensão de link, o usuário deverá fornecer os campos obrigatórios na propriedade "Identity". O restante do manifesto contém informações específicas para o Marketplace (por exemplo, categorias, se Q&A está habilitada, etc.).

Exemplo de arquivo publishManifest de extensão do VSIX:

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],  // The categories of the extension. Between 1 and 3 categories are required.
    "identity": {
        "internalName": "MyVsixExtension" // If not specified, we try to generate the name from the display name of the extension in the vsixmanifest file.
                                            // Required if the display name is not the actual name of the extension.
    },
    "overview": "overview.md",            // Path to the "readme" file that gets uploaded to the Marketplace. Required.
    "priceCategory": "free",              // Either "free", "trial", or "paid". Defaults to "free".
    "publisher": "MyPublisherName",       // The name of the publisher. Required.
    "private": false,                     // Specifies whether or not the extension should be public when uploaded. Defaults to false.
    "qna": true,                          // Specifies whether or not the extension should have a Q&A section. Defaults to true.
    "repo": "https://github.com/MyPublisherName/MyVsixExtension" // Not required.
}
```

Exemplo de arquivo MSI/EXE ou LINK publishManifest:

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],
    "identity": {
        "description": "My extension.", // The description of the extension. Required for non-vsix extensions.
        "displayName": "My Extension",  // The display name of the extension. Required for non-vsix extensions.
        "icon": "\\path\\to\\icon.ico", // The path to an icon file (can be relative to the json file location). Required for non-vsix extensions.
        "installTargets": [             // The installation targets for the extension. Required for non-vsix extensions.
            {
                "sku": "Microsoft.VisualStudio.Community",
                "version": "[10.0, 16.0)"
            }
        ],
        "internalName": "MyExtension",
        "language": "en-US",            // The default language id of the extension. Can be in the "1033" or "en-US" format. Required for non-vsix extensions.
        "tags": [ "tag1", "tag2" ],     // The tags for the extension. Not required.
        "version": "3.7.0",             // The version of the extension. Required for non-vsix extensions.
        "vsixId": "MyExtension",        // The vsix id of the extension. Not required but useful for showing updates to installed extensions.
    },
    "overview": "overview.md",
    "priceCategory": "free",
    "publisher": "MyPublisherName",
    "private": false,
    "qna": true,
    "repo": "https://github.com/MyPublisherName/MyVsixExtension"
}
```

## <a name="asset-files"></a>Arquivos de ativo

Os arquivos de ativo podem ser fornecidos para a inserção de coisas como imagens no arquivo Leiame. Por exemplo, se uma extensão tiver o seguinte documento de redução de "visão geral":

```markdown
TestExtension
...
This is test extension.
![Test logo](images/testlogo.png "Test logo")
```

Para resolver "imagens/testlogo.png" no exemplo anterior, um usuário pode fornecer "assetFiles" em seu manifesto de publicação, como abaixo:

```json
{
    "assetFiles": [
        {
            "pathOnDisk": "\\path\\to\\logo.png",
            "targetPath": "images/logo.png"
        }
    ],
    // other required fields
}
```

## <a name="publishing-walkthrough"></a>Orientações de publicação

### <a name="prerequisites"></a>Pré-requisitos

Para seguir este passo a passos, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

### <a name="create-a-visual-studio-extension"></a>Criar uma extensão do Visual Studio

Nesse caso, usaremos uma extensão VSPackage padrão, mas as mesmas etapas são válidas para cada tipo de extensão.

1. Crie um VSPackage em C# chamado "TestPublish" que tenha um comando de menu. Para obter mais informações, consulte [criando sua primeira extensão: Olá, mundo](../extensibility/extensibility-hello-world.md).

### <a name="package-your-extension"></a>Empacotar sua extensão

1. Atualize a extensão vsixmanifest com as informações corretas sobre o nome do produto, o autor e a versão.

   ![atualizar vsixmanifest de extensão](media/update-extension-vsixmanifest.png)

2. Crie sua extensão no modo de **versão** . Agora, sua extensão será empacotada como um VSIX na pasta \bin\Release.

3. Você pode clicar duas vezes no VSIX para verificar a instalação.

### <a name="test-the-extension"></a>Testar a extensão

 Antes de distribuir a extensão, compile e teste-a para verificar se ela está instalada corretamente na instância experimental do Visual Studio.

1. No Visual Studio, inicie a depuração. para abrir uma instância experimental do Visual Studio.

2. Na instância experimental, vá para o menu **ferramentas** e clique em **extensões e atualizações...**. A extensão TestPublish deve aparecer no painel central e ser habilitada.

3. No menu **ferramentas** , verifique se você vê o comando de teste.

### <a name="publish-the-extension-to-the-marketplace-via-command-line"></a>Publicar a extensão para o Marketplace por meio da linha de comando

1. Certifique-se de que você criou a versão de lançamento da extensão e que ela está atualizada.

2. Certifique-se de ter criado publishmanifest.jsem arquivos e overview.md.

3. Abra a linha de comando e navegue até o diretório $ {VSInstallDir} \VSSDK\VisualStudioIntegration\Tools\Bin\.

4. Para criar um novo Publicador, use o seguinte comando:

   ```
   VsixPublisher.exe createPublisher -publisherName "TestVSIXPublisher" -displayName "Test VSIX Publisher" -personalAccessToken "{Personal Access Token that is used to authenticate the publisher. If not provided, the pat is acquired from the logged-in users.}"
   ```

5. Após a criação bem-sucedida do Publicador, você verá a seguinte mensagem de linha de comando:

   ```
   Added 'Test VSIX Publisher' as a publisher on the Marketplace.
   ```

6. Você pode verificar o novo Publicador criado navegando até [Visual Studio Marketplace](https://marketplace.visualstudio.com/manage/publishers)

7. Para publicar uma nova extensão, use o seguinte comando:

   ```
   VsixPublisher.exe publish -payload "{Path to vsix file}"  -publishManifest "{path to publishManifest file}"
   ```

8. Após a criação bem-sucedida do Publicador, você verá a seguinte mensagem de linha de comando:

   ```
   Uploaded 'MyVsixExtension' to the Marketplace.
   ```

9. Você pode verificar a nova extensão que você publicou navegando até [Visual Studio Marketplace](https://marketplace.visualstudio.com/)

### <a name="install-the-extension-from-the-visual-studio-marketplace"></a>Instalar a extensão do Visual Studio Marketplace

Agora que a extensão foi publicada, instale-a no Visual Studio e teste-a lá.

1. No Visual Studio, no menu **ferramentas** , clique em **extensões e atualizações...**.

2. Clique em **online** e procure por TestPublish.

3. Clique em **Download**. A extensão será então agendada para instalação.

4. Para concluir a instalação, feche todas as instâncias do Visual Studio.

## <a name="remove-the-extension"></a>Remover a extensão

Você pode remover a extensão da Visual Studio Marketplace e do seu computador.

### <a name="to-remove-the-extension-from-the-marketplace-via-command-line"></a>Para remover a extensão do Marketplace por meio da linha de comando

1. Se você quiser remover uma extensão, use o seguinte comando:

   ```
   VsixPublisher.exe deleteExtension -publisherName "TestVSIXPublisher" -extensionName "MyVsixExtension"
   ```

2. Após a exclusão bem-sucedida da extensão, você verá a seguinte mensagem de linha de comando:

   ```
   Removed 'MyVsixExtension' from the Marketplace.
   ```

### <a name="to-remove-the-extension-from-your-computer"></a>Para remover a extensão do seu computador

1. No Visual Studio, no menu **ferramentas** , clique em **extensões e atualizações**.

2. Selecione "MyVsixExtension" e clique em **desinstalar**. A extensão será então agendada para desinstalação.

3. Para concluir a desinstalação, feche todas as instâncias do Visual Studio.
