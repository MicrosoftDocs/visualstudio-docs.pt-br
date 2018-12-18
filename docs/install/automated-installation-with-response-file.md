---
title: Automatizar a instalação do Visual Studio com um arquivo de resposta
description: Saiba como criar um arquivo de resposta JSON que ajuda a automatizar a instalação do Visual Studio
ms.date: 08/14/2017
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- response file
- automate
- installation
- command-line
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6d9dbcb5c033469db3e92bd4cde931257ece9ab1
ms.sourcegitcommit: 6b092e7d466377f06913d49d183dbbdca16730f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2018
ms.locfileid: "43138443"
---
# <a name="how-to-define-settings-in-a-response-file"></a>Como definir as configurações em um arquivo de resposta

Os administradores que implantam o Visual Studio podem especificar um arquivo de resposta usando o parâmetro `--in`, assim como no exemplo a seguir:

```cmd
vs_enterprise.exe --in customInstall.json
```

Os arquivos de resposta são arquivos [JSON](http://json-schema.org/) cujo conteúdo espelha os argumentos de linha de comando.  Em geral, se um parâmetro de linha de comando não usa nenhum argumento (por exemplo, `--quiet`, `--passive`, etc.), o valor no arquivo de resposta deve ser verdadeiro/falso.  Se for necessário um argumento (por exemplo, `--installPath <dir>`), o valor no arquivo de resposta deverá ser uma cadeia de caracteres.  Se for necessário um argumento e ele puder aparecer mais de uma vez na linha de comando (por exemplo, `--add <id>`), deverá ser uma matriz de cadeias de caracteres.

Parâmetros que são especificados nas configurações de substituição de linha de comando do arquivo de resposta, exceto quando os parâmetros recebem várias entradas (por exemplo, `--add`). Quando você tiver várias entradas, as entradas fornecidas na linha de comando serão mescladas com as configurações do arquivo de resposta.

## <a name="setting-a-default-configuration-for-visual-studio"></a>Definir uma configuração padrão para o Visual Studio

Se você tiver criado um cache de layout de rede com o `--layout`, um arquivo `response.json` inicial será criado no layout. Se você criar um layout parcial, esse arquivo de resposta incluirá as cargas de trabalho e idiomas incluídos no layout.  Executar a instalação deste layout usa automaticamente esse arquivo response.json, que seleciona as cargas de trabalho e os componentes incluídos no layout.  Os usuários ainda podem selecionar ou desmarcar todas as cargas de trabalho na interface do usuário de configuração antes de instalar o Visual Studio.

Os administradores que criam um layout podem modificar o arquivo `response.json` no layout para controlar as configurações padrão que os usuários veem quando instalam o Visual Studio do layout.  Por exemplo, se um administrador quiser que cargas de trabalho e componentes específicos sejam instalados por padrão, poderá configurar o arquivo `response.json` para adicioná-los.

Quando a instalação do Visual Studio for executada em uma pasta de layout, ela usará _automaticamente_ o arquivo de resposta na pasta do layout.  Você não precisa usar a opção `--in`.

Você pode atualizar o arquivo `response.json` criado em uma pasta de layout offline para definir a configuração padrão para usuários que instalam com base nesse layout.

> [!WARNING]
> É fundamental que você deixe as propriedades existentes que foram definidas quando o layout foi criado.

O arquivo `response.json` base em um layout deve ser semelhante ao exemplo a seguir, exceto que ele inclui o valor para o produto e o canal que você deseja instalar:

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/15/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.15.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```

Quando você cria ou atualiza um layout, um arquivo response.template.json também é criado.  Esse arquivo contém todas as IDs de carga de trabalho, de componente e de idioma que podem ser usadas.  Esse arquivo é fornecido como um modelo para o qual todas poderiam ser incluídas em uma instalação personalizada.  Os administradores podem usar esse arquivo como um ponto de partida para um arquivo de resposta personalizado.  Basta remover as IDs para os itens que você não deseja instalar e salvá-las em seu próprio arquivo de resposta.  Não personalize o arquivo response.template.json, caso contrário, as alterações serão perdidas sempre que o layout for atualizado.

## <a name="example-layout-response-file-content"></a>Conteúdo de arquivo de resposta de layout de exemplo

O exemplo a seguir instalará o Visual Studio Enterprise com seis cargas de trabalho e componentes comuns e com os idiomas inglês e francês da interface do usuário. Você pode esse exemplo como um modelo; apenas altere as cargas de trabalho e os componentes para aqueles que você deseja instalar:

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/15/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.15.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise",

  "installPath": "C:\\VS2017",
  "quiet": false,
  "passive": false,
  "includeRecommended": true,
  "norestart": false,

  "addProductLang": [
    "en-US",
    "fr-FR"
    ],

    "add": [
        "Microsoft.VisualStudio.Workload.ManagedDesktop",
        "Microsoft.VisualStudio.Workload.Data",
        "Microsoft.VisualStudio.Workload.NativeDesktop",
        "Microsoft.VisualStudio.Workload.NetWeb",
        "Microsoft.VisualStudio.Workload.Office",
        "Microsoft.VisualStudio.Workload.Universal",
        "Component.GitHub.VisualStudio"
    ]
}
```

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [IDs de carga de trabalho e de componente do Visual Studio 2017](workload-and-component-ids.md)
