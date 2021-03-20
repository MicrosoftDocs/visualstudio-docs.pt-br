---
title: Personalizar um codespace (visualização)
description: Saiba mais sobre como personalizar um codespace.
ms.topic: how-to
ms.date: 09/21/2020
author: gregvanl
ms.author: gregvanl
manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: 0e23ca3255761f4d93f89251d00c12c14aecf7b9
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104672345"
---
# <a name="how-to-customize-a-codespace-preview"></a>Como personalizar um codespace (visualização)

> [!Important] 
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Incentivamos você a estar envolvido em nosso [Fórum da comunidade de desenvolvedores](https://developercommunity.visualstudio.com/home) para Visual Studio para obter informações sobre versões futuras e informações de roteiro. 

O GitHub Codespaces fornece um ambiente de desenvolvimento completo na nuvem. Para o desenvolvimento baseado em Windows usando o Visual Studio 2019, as instâncias padrão do GitHub Codespaces fornecem um ótimo ponto de partida, mas você também pode personalizar o ambiente para seu projeto específico.

## <a name="installed-software"></a>Software instalado

O codespaces do Windows vem com muitas estruturas e ferramentas já instaladas para que você possa começar imediatamente. A tabela a seguir lista os aplicativos e recursos disponíveis em todos os ambientes do Windows codespace.

| Aplicativo                                         | Alias do caminho | Versão            |
|---------------------------------------------|------------|--------------------|
| .NET                                        | N/D        | 4.8                |
| Runtime do .NET Core                           | dotnet     | 2,1, 3,1           |
| SDK do .Net Core                               | dotnet     | 2,1, 3.1.3, 3.1.4  |
| CLI do Azure                                   | AZ         | 2.5                |
| Chocolatey                                  | choco      | 0.10.15            |
| CMake                                       | CMake      | 3,17               |
| Git                                         | Git        | 2,26               |
| Build da Microsoft                             | msbuild    | 16,7               |
| Microsoft SQL Server Express Edition 2019   | N/D        | 15.0               |
| Ninja                                       | Ninja      | 1.8.2              |
| Node.js                                     | nó       | 12.16              |
| NPM                                         | npm        | 6.14               |
| Python                                      | python     | 3.7                |
| Gerenciador de pacotes VC                          | vcpkg      | 2020, 2            |
| SDK do Windows                                 | N/D        | 10.0.18362         |

A lista acima não é exaustiva e exclui muitas ferramentas que o Visual Studio instala (por exemplo, IISExpress). Um componente também pode ter uma versão secundária ou de patch diferente daquela mencionada acima.

Detalhes específicos sobre as estruturas e ferramentas pré-instaladas são fornecidos na seção [especificações de software instaladas](#installed-software-specifics) abaixo.

## <a name="modifications-to-a-codespace"></a>Modificações em um codespace
 
Depois de criar um codespace, todas as alterações feitas a esse codespace específico serão persistidas enquanto a instância de codespace estiver disponível no GitHub Codespaces. Você pode clonar repositórios adicionais, instalar ferramentas e geradores de aplicativos e adicionar outros ativos de desenvolvimento e essas modificações serão preservadas mesmo quando o codespace for suspenso. No entanto, se você excluir um codespace, todas as modificações serão feitas.

> [!NOTE]
> Se você excluir um codespace, todas as alterações em um repositório local (pendente ou comprometido) no codespace serão perdidas. Certifique-se de enviar por push as alterações de repositório para um local remoto antes de excluir um codespace.

Enquanto estiver conectado a um codespace com o Visual Studio, você poderá usar o terminal do Visual Studio para executar ferramentas de linha de comando. Você pode usar o PowerShell ou o prompt de comando do Windows, ambos com privilégios elevados sob a conta de administrador local. Para saber mais sobre o terminal do Visual Studio, consulte o [blog anúncio de terminal do Visual Studio](https://devblogs.microsoft.com/visualstudio/say-hello-to-the-new-visual-studio-terminal/).

## <a name="customize-a-codespace"></a>Personalizar um codespace

O valor real do Codespaces do GitHub vem quando você pode criar ambientes de desenvolvimento exclusivos e reproduzíveis na nuvem sob medida para seu próprio trabalho, bem como para a sua equipe. Ao criar uma instância de Codespaces do GitHub padrão, você pode personalizar o que está instalado e configurado quando você cria um novo codespace.

As seções a seguir descrevem dois métodos *de configuração do* codespace usando.devcontainer.jse *.devinit.jsem* arquivos. Esses arquivos permitem que você configure as estruturas e ferramentas de instalação para um codespace e quando adicionadas ao seu repositório, qualquer pessoa que criar um codespace com base em seu repositório terá o mesmo ambiente de desenvolvimento remoto.

## <a name="customize-with-devcontainerjson"></a>Personalizar com devcontainer.jsem

Quando um codespace é criado, o GitHub Codespaces procura um [*devcontainers.jsno*](https://code.visualstudio.com/docs/remote/devcontainerjson-reference) arquivo na raiz do seu repositório e usa as configurações no para personalizar o codespace ou as instâncias de cliente conectando-se a ele (editor-base de navegador, Visual Studio ou Visual Studio Code). A maioria dos *devcontainer.jsem* configurações se aplicam a codespaces baseados em Linux ou a dois outros clientes, mas alguns estão disponíveis para o Windows codespaces e o Visual Studio.

O *devcontainer.jsno* arquivo pode ser colocado em um dos dois locais em um repositório:

1. *{repositório-raiz}/.devcontainer.jsem*
2. *{Repository-root}/.devcontainer/devcontainer.jsem*

O GitHub Codespaces dá suporte aos seguintes *devcontainer.jsem* Propriedades. Definir Visual Studio Code propriedades específicas será útil se você pretende se conectar ao seu codespace com os outros clientes além do Visual Studio. 

* `extensions` -Uma matriz de extensões do [Marketplace Visual Studio Code](https://marketplace.visualstudio.com/vscode) que deve ser instalada.
* `settings`  -Um conjunto de [configurações de Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings) a ser aplicado.
* `forwardPorts`-Uma porta ou matriz de portas que devem ser automaticamente encaminhadas localmente quando o codespace estiver em execução.
* `postCreateCommand` -Uma cadeia de caracteres de comando ou uma lista de argumentos de comando a serem executados após a criação de codespace.

> [!NOTE]
> **devcontainer.jsem** arquivos também são usados para dar suporte ao [desenvolvimento Visual Studio Code remoto](https://code.visualstudio.com/docs/remote/remote-overview)e têm propriedades adicionais não abordadas neste documento. Essas propriedades adicionais são seguras para adicionar ao arquivo, mas serão ignoradas por Codespaces. Para obter mais informações, consulte a [devcontainer.jsem referência](https://code.visualstudio.com/docs/remote/devcontainerjson-reference) em code.VisualStudio.com.

## <a name="customize-with-devinit"></a>Personalizar com devinit

o [devinit](../../devinit/getting-started-with-devinit.md) é uma ferramenta de linha de comando incluída no Windows codespaces que permite que você instale estruturas e ferramentas em seu ambiente. Ele pode ser executado manualmente de um prompt de comando ( `devinit run -t require-dotnetcoresdk` ), mas seu potencial real vem da criação de um [ *.devinit.jspersonalizado no*](../../devinit/devinit-json.md) arquivo para configurar uniformemente um codespace sempre que você criar um.

`devinit` inclui um conjunto de ferramentas para a instalação de itens específicos, como SQL Server e o CLI do Azure, e também a execução de gerenciadores de pacotes gerais, como Chocolatey, NPM e vcpkg. Você pode encontrar a lista completa de `devinit` ferramentas na documentação de [ferramentas disponíveis](../../devinit/devinit-tool-list.md) .

### <a name="devinitjson"></a>devinit.jsem

Embora você possa executar a `devinit` linha de comando diretamente, é recomendável criar [*devinit.jsem*](../../devinit/devinit-json.md) arquivos de configuração, que descrevem o conjunto de `devinit` ferramentas a serem executadas. 

Por exemplo, para instalar o [SDK do .NET Core](/dotnet/core/sdk), um *.devinit.js* deve ser semelhante a:

```json
{
    "run": [
        {
            "comments": "We need the .NET Core SDK."
            "tool": "require-dotnetcoresdk"
        }
    ]
}
```

Quando você cria um *.devinit.jsno* arquivo na raiz do seu projeto, ele será usado quando você executar o `devinit init` . Por padrão, `devinit.exe` o procura o arquivo nos seguintes locais:

1. *{diretório atual} \\.devinit.jsem*
2. *{diretório atual} \\.devinit\devinit.jsem*

### <a name="running-devinit-when-creating-a-codespace"></a>Executando devinit ao criar um codespace

Você pode instruir o GitHub Codespaces a ser executado `devinit` depois que um codespace é criado usando a `postCreateCommand` propriedade em um *devcontainers.jsno* arquivo. Conforme mencionado acima, o GitHub Codespaces procurará um *devcontainer.jsno* arquivo no repositório clonado para personalizar a instância do codespace ou do cliente e executará quaisquer comandos descritos na `postCreateCommand` propriedade.

Ao especificar `devinit init` , `devinit` será executado usando seu *devinit.jsna* configuração.

```json
{
  "postCreateCommand": "devinit init"
}
```

### <a name="an-example"></a>Um exemplo

Veja um exemplo simples instalando o .NET Core Entity Framework ferramenta de linha de comando, `dotnet-ef` .

**devcontainer.json**

Conteúdo da *.devcontainer.jsno* arquivo na raiz do repositório. 

```json
{
  "postCreateCommand": "devinit init"
}
```

**devinit.jsem**

Conteúdo do *.devinit.jsno* arquivo. Esse arquivo precisa estar na mesma pasta que *.devcontainer.jsem*.

```json
{
    "run": [
        {
            "comments": "Install the Entity Framework tools",
            "tool": "dotnet-toolinstall",
            "input": "dotnet-ef",
        }
     ]
}
```

Você pode encontrar mais `devinit` exemplos na `devinit` [lista de exemplos](../../devinit/sample-readme.md).

## <a name="port-forwarding"></a>Encaminhamento de porta

O GitHub Codespaces fornece acesso aos aplicativos e serviços em execução nos ambientes remotos por meio de encaminhamento de porta. Por padrão, nenhuma porta é encaminhada por questões de segurança. No entanto, você pode especificar determinadas portas para abrir em um codespace.

### <a name="configure-port-forwarding"></a>Configurar o encaminhamento de porta

Se houver uma ou mais portas que devem ser encaminhadas por padrão para um determinado repositório, isso pode ser configurado no *devcontainer.js* com a `forwardPorts` propriedade.

* `forwardPorts` -Uma porta ou matriz de portas que devem ser automaticamente encaminhadas localmente quando o ambiente estiver em execução.

## <a name="installed-software-specifics"></a>Especificações de software instaladas

### <a name="microsoft-sql-server"></a>Microsoft SQL Server

Microsoft SQL Server 2019 Express Edition está disponível e em execução como um serviço local (LocalDB) no ambiente do Windows codespace. O usuário atual, para o qual seu aplicativo e o terminal do Visual Studio são executados, tem direitos de administrador do SQL para o SQL Server. Para administrar o servidor, você precisará usar o PowerShell no terminal do Visual Studio ou outras ferramentas de linha de comando, como `dotnet-ef` . Atualmente SQL Server Management Studio e outras ferramentas de administração remota não estão disponíveis.

#### <a name="example-connection-string"></a>Exemplo de cadeia de conexão

Abaixo está um exemplo de uma cadeia de conexão para se conectar ao MS SQL Server local.

```csharp
"Server=(LocalDB);Integrated Security=true;"
```

### <a name="azure-cli"></a>CLI do Azure

O CLI do Azure é instalado em todos os ambientes do Windows codespace e está disponível no caminho como `az` .

#### <a name="using-azure-resources"></a>Usando recursos do Azure

Se você estiver usando uma identidade de Azure Active Directory para autenticar seu aplicativo em relação aos recursos do Azure, será necessário primeiro entrar no Azure por meio do terminal do Visual Studio. Para entrar, use o comando CLI do Azure `login` com o fluxo de entrada do dispositivo (conforme mostrado no exemplo abaixo). Depois de conectado, seu aplicativo e a sessão de terminal devem ser capazes de usar essa identidade.

```powershell
> az login --use-device-code
```

Você pode saber mais sobre o `az login` comando na [documentação](/cli/azure/reference-index#az_login)do CLI do Azure.

## <a name="see-also"></a>Veja também

- [O que é o GitHub Codespaces?](codespaces-overview.md)
- [Como usar o Visual Studio com um codespace](use-visual-studio-with-codespaces.md)