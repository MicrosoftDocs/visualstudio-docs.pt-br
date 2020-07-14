---
title: Como adicionar o arquivo app.config a um projeto
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
helpviewer_keywords:
- app.config files, adding to C# projects
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: fe659979cadf4d9e5752f7bbe85150aae848de08
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770828"
---
# <a name="how-to-add-an-application-configuration-file-to-a-c-project"></a>Como adicionar um arquivo de configuração de aplicativo a um projeto C#

Ao adicionar um arquivo de configuração de aplicativo (arquivo *app.config*) a um projeto C#, você pode personalizar o modo como o Common Language Runtime localiza e carrega arquivos do assembly. Para saber mais sobre arquivos de configuração de aplicativo, veja [Como o runtime localiza assemblies (.NET Framework)](/dotnet/framework/deployment/how-the-runtime-locates-assemblies).

> [!NOTE]
> Os aplicativos da UWP não contêm um arquivo *app.config*.

Quando você cria seu projeto, o ambiente de desenvolvimento copia automaticamente o arquivo *app.config*, altera o nome do arquivo da cópia para corresponder ao executável e, em seguida, move a cópia para o diretório **bin**.

## <a name="to-add-an-application-configuration-file-to-a-c-project"></a>Para adicionar um arquivo de configuração de aplicativo a um projeto C#

1. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

     A caixa de diálogo **Adicionar Novo Item** aparecerá.

1. Expanda **Installed**  >  **itens do Visual C#** instalados e escolha o modelo de **arquivo de configuração de aplicativo** .

1. Na caixa e texto **Nome**, insira um nome e escolha o botão **Adicionar**.

     Um arquivo chamado *app.config* é adicionado ao seu projeto.

## <a name="see-also"></a>Confira também

- [Gerenciar configurações de aplicativo (.NET)](../ide/managing-application-settings-dotnet.md)
- [Esquema do arquivo de configuração (.NET Framework)](/dotnet/framework/configure-apps/file-schema/index)
- [Configurar aplicativos (.NET Framework)](/dotnet/framework/configure-apps/index)
