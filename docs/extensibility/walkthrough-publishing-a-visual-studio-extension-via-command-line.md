---
title: 'Passo a passo: Publicando uma extensão do Visual Studio por meio da linha de comando | Microsoft Docs'
ms.custom: ''
ms.date: 07/12/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- publishing extensions
- extension, publishing
ms.assetid: 6ff9efc4-919d-4071-a80d-6dbdd2ceb2f8
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8d95e2fbe36a73074b97f47f6714f1fc4aa8228c
ms.sourcegitcommit: 12d6398c02e818de4fbcb4371bae9e5db6cf9509
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050177"
---
# <a name="walkthrough-publishing-a-visual-studio-extension-via-command-line"></a>Passo a passo: Publicando uma extensão do Visual Studio por meio da linha de comando

Este passo a passo mostra como publicar uma extensão do Visual Studio no Visual Studio Marketplace usando a linha de comando. Quando você adiciona sua extensão no Marketplace, os desenvolvedores podem usar o [ **extensões e atualizações** ](../ide/finding-and-using-visual-studio-extensions.md) caixa de diálogo para procurar novas e atualizadas extensões lá.

VsixPublisher.exe é a ferramenta de linha de comando para extensões do Visual Studio publicação no Marketplace. Ele pode ser acessado de ${VSInstallDir}\VSSDK\VisualStudioIntegration\Tools\Bin\VsixPublisher.exe. Os comandos disponíveis nessa ferramenta são: **publique**, **createPublisher**, **deletePublisher**, **deleteExtension**,  **login**, **logout**.

## <a name="commands"></a>Comandos

### <a name="publish"></a>publicar

Publica uma extensão no Marketplace. A extensão pode ser um vsix, um arquivo exe/msi ou um link. Se a extensão já existe com a mesma versão, ele substituirá a extensão. Se a extensão não existir, ele criará uma nova extensão.

|Opções de comando |Descrição |
|---------|---------|
|carga (obrigatória) | Um caminho para a carga para publicar ou um link a ser usada como a "URL de informações adicionais". |
|publishManifest (obrigatório) | Caminho para a publicação do manifesto arquivo a ser usado. |
|ignoreWarnings | Lista de avisos a serem ignorados ao publicar uma extensão. Esses avisos são mostrados como mensagens de linha de comando ao publicar uma extensão. (por exemplo, "VSIXValidatorWarning01, VSIXValidatorWarning02")  
|personalAccessToken | Pessoal acesso PAT (Token) que é usado para autenticar o publicador. Se não for fornecido, o PAT é obtido dos usuários conectados. |

```
VsixPublisher.exe publish -payload "{path to vsix}" -publishManifest "{path to vs-publish.json}" -ignoreWarnings "VSIXValidatorWarning01,VSIXValidatorWarning02"
```

### <a name="createpublisher"></a>createPublisher

Cria um publicador no Marketplace. Também registra o publicador na máquina para ações futuras (por exemplo, uma extensão de exclusão/publicação).

|Opções de comando |Descrição |
|---------|---------|
|displayName (obrigatório) | Nome de exibição do publicador. |
|publisherName (obrigatório) | O nome do publicador (por exemplo, o identificador). |
|personalAccessToken (obrigatório) | Token de acesso pessoal que é usado para autenticar o publicador. |
|shortDescription | Uma breve descrição do Editor (não um arquivo). |
|longDescription | Uma descrição longa do publicador (não um arquivo). |

```
VsixPublisher.exe createPublisher -publisherName "{Publisher Name}" -displayName "{Publisher Display Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deletepublisher"></a>deletePublisher

Exclui um publicador no Marketplace.

|Opções de comando |Descrição |
|---------|---------|
|publisherName (obrigatório) | O nome do publicador (por exemplo, o identificador). |
|personalAccessToken (obrigatório) | Token de acesso pessoal que é usado para autenticar o publicador. |

```
VsixPublisher.exe deletePublisher -publisherName "{Publisher Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deleteextension"></a>deleteExtension

Exclui uma extensão do Marketplace.

|Opções de comando |Descrição |
|---------|---------|
|extensionName (obrigatório) | O nome da extensão a excluir. |
|publisherName (obrigatório) | O nome do publicador (por exemplo, o identificador). |
|personalAccessToken | Token de acesso pessoal que é usado para autenticar o publicador. Se não for fornecido, o pat é obtido dos usuários conectados. |

```
VsixPublisher.exe deleteExtension -extensionName "{Extension Name}" -publisherName "{Publisher Name}"
```

### <a name="login"></a>Logon

Registra um publicador na máquina.

|Opções de comando |Descrição |
|---------|---------|
|personalAccessToken (obrigatório | Token de acesso pessoal que é usado para autenticar o publicador. |
|publisherName (obrigatório) | O nome do publicador (por exemplo, o identificador). |
|Substituir | Especifica que qualquer publicador existente deve ser substituído com o novo token de acesso pessoal. |

```
VsixPublisher.exe login -personalAccessToken "{Personal Access Token}" -publisherName "{Publisher Name}"
```

### <a name="logout"></a>logoff

Registra um editor fora do computador.

|Opções de comando |Descrição |
|---------|---------|
|publisherName (obrigatório) | O nome do publicador (por exemplo, o identificador). |
|ignoreMissingPublisher | Especifica que a ferramenta de não erro se o publicador especificado não é já fizeram logon. |

```
VsixPublisher.exe logout -publisherName "{Publisher Name}"
```

## <a name="publishmanifest-file"></a>arquivo publishManifest

Um arquivo publishManifest é usado pelas **publicar** comando. Ele representa todos os metadados sobre a extensão de que precisa saber o Marketplace. Se a extensão que está sendo carregada for de uma extensão do VSIX, a propriedade "identity" só deve ter o "internalName" definido. Isso ocorre porque o restante das propriedades de "identidade" pode ser gerado no arquivo vsixmanifest. Se a extensão é um msi /. exe ou uma extensão de link, o usuário deve fornecer os campos obrigatórios na propriedade "identity". O restante do manifesto contém informações específicas para o Marketplace (por exemplo, categorias, se p e r está habilitado, etc.).

Exemplo de arquivo de publishManifest de extensão VSIX:

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

Exemplo de arquivo de publishManifest MSI/EXE ou LINK:

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

Arquivos de ativo podem ser fornecidos para a inserção de coisas como imagens no arquivo Leiame. Por exemplo, se uma extensão tem o documento de Markdown "Visão geral" seguintes:

```markdown
TestExtension
...
This is test extension.
![Test logo](images/testlogo.png "Test logo")
```

Para resolver o "images/testlogo.png" no exemplo anterior, um usuário pode fornecer "assetFiles" em sua publicação manifesto, como abaixo:

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

## <a name="publishing-walkthrough"></a>Instruções passo a passo publicação

### <a name="prerequisites"></a>Pré-requisitos

Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

### <a name="create-a-visual-studio-extension"></a>Criar uma extensão do Visual Studio

Nesse caso, usaremos uma extensão de VSPackage padrão, mas as mesmas etapas são válidas para cada tipo de extensão.

1. Crie um VSPackage no c#, chamado "TestPublish" que tem um comando de menu. Para obter mais informações, consulte [criando sua primeira extensão: Olá, mundo](../extensibility/extensibility-hello-world.md).

### <a name="package-your-extension"></a>Empacotar sua extensão

1. Atualize a extensão vsixmanifest com as informações corretas sobre o nome do produto, autor e versão.

   ![atualizar a extensão vsixmanifest](media/update-extension-vsixmanifest.png)

2. Compile sua extensão **versão** modo. Agora sua extensão será empacotada como um VSIX na pasta \bin\Release.

3. Você pode clicar duas vezes o VSIX para verificar a instalação.

### <a name="test-the-extension"></a>A extensão de teste

 Antes de distribuir a extensão, compilar e testar para verificar se que ele está instalado corretamente na instância experimental do Visual Studio.

1. No Visual Studio, inicie a depuração. Para abrir uma instância experimental do Visual Studio.

2. Na instância experimental, vá para o **ferramentas** menu e clique em **extensões e atualizações...** . A extensão TestPublish deve aparecer no painel central e ser habilitada.

3. Sobre o **ferramentas** menu, verifique se você vir o comando de teste.

### <a name="publish-the-extension-to-the-marketplace-via-command-line"></a>Publicar a extensão no Marketplace por meio da linha de comando

1. Certifique-se de que você criou a versão de lançamento da sua extensão e que ela seja atualizada.

2. Verifique se que você criou arquivos publishmanifest.json e overview.md.

3. Abra a linha de comando e navegue até o diretório de \VSSDK\VisualStudioIntegration\Tools\Bin\ de ${VSInstallDir}.

4. Para criar um novo publicador, use o seguinte comando:

   ```
   VsixPublisher.exe createPublisher -publisherName "TestVSIXPublisher" -displayName "Test VSIX Publisher" -personalAccessToken "{Personal Access Token that is used to authenticate the publisher. If not provided, the pat is acquired from the logged-in users.}"
   ```

5. A criação bem-sucedida do publicador, você verá a seguinte mensagem de linha de comando:

   ```
   Added 'Test VSIX Publisher' as a publisher on the Marketplace.
   ```

6. Você pode verificar o novo publicador que você criou, navegando até [Visual Studio Marketplace](https://marketplace.visualstudio.com/manage/publishers)

7. Para publicar uma nova extensão, use o seguinte comando:

   ```
   VsixPublisher.exe publish -payload "{Path to vsix file}"  -publishManifest "{path to publishManifest file}"
   ```

8. A criação bem-sucedida do publicador, você verá a seguinte mensagem de linha de comando:

   ```
   Uploaded 'MyVsixExtension' to the Marketplace.
   ```

9. Você pode verificar a nova extensão que você publicou, navegando até [Visual Studio Marketplace](https://marketplace.visualstudio.com/)

### <a name="install-the-extension-from-the-visual-studio-marketplace"></a>Instalar a extensão do Visual Studio Marketplace

Agora que a extensão for publicada, instalá-lo no Visual Studio e testá-lo lá.

1. No Visual Studio, sobre o **ferramentas** menu, clique em **extensões e atualizações...** .

2. Clique em **Online** e, em seguida, pesquise por TestPublish.

3. Clique em **Baixar**. A extensão, em seguida, será agendada para instalação.

4. Para concluir a instalação, feche todas as instâncias do Visual Studio.

## <a name="remove-the-extension"></a>Remover a extensão

Você pode remover a extensão do Visual Studio Marketplace e do seu computador.

### <a name="to-remove-the-extension-from-the-marketplace-via-command-line"></a>Para remover a extensão do Marketplace por meio da linha de comando

1. Se você quiser remover uma extensão, use o seguinte comando:

   ```
   VsixPublisher.exe deleteExtension -publisherName "TestVSIXPublisher" -extensionName "MyVsixExtension"
   ```

2. Na exclusão com êxito da extensão, você verá a seguinte mensagem de linha de comando:

   ```
   Removed 'MyVsixExtension' from the Marketplace.
   ```

### <a name="to-remove-the-extension-from-your-computer"></a>Para remover a extensão do seu computador

1. No Visual Studio, sobre o **ferramentas** menu, clique em **extensões e atualizações...** .

2. Selecione "MyVsixExtension" e, em seguida, clique em **desinstalação**. Em seguida, a extensão será agendada para desinstalação.

3. Para concluir a desinstalação, feche todas as instâncias do Visual Studio.
