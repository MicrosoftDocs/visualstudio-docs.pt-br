---
description: O empacotamento de aplicativos como um MSI geralmente é realizado usando a extensão de projetos Instalador do Visual Studio.
title: Projetos de Instalador do Visual Studio e .NET Core 3,1
titleSuffix: ''
ms.date: 08/18/2020
ms.topic: conceptual
helpviewer_keywords:
- installer projects
- installer projects, .NETCore
author: MSLukeWest
ms.author: lukewest
manager: MSLukeWest
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 5a78c1cf4f7b1562408e0a3fb598075f2c114fc0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102171234"
---
# <a name="visual-studio-installer-projects-extension-and-net-core-31"></a>Extensão de Projetos do Instalador do Visual Studio e .NET Core 3.1

O empacotamento de aplicativos como um MSI geralmente é realizado usando a extensão de projetos Instalador do Visual Studio.

Você pode baixar a extensão aqui: [instalador do Visual Studio projetos](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2017InstallerProjects)

## <a name="update-for-net-core"></a>Atualização para o .NET Core
O .NET Core tem dois modelos diferentes para publicação.

- Implantações dependentes da estrutura

- Os aplicativos independentes incluem o tempo de execução.

Para saber mais sobre essas estratégias de implantação, consulte [visão geral da publicação de aplicativos do .NET Core](/dotnet/core/deploying/).

### <a name="workflow-changes-for-net-core-31"></a>Alterações de fluxo de trabalho para o .NET Core 3,1

1. Selecione **publicar itens** em vez da **saída primária** para obter a saída correta para projetos do .NET Core 3,1.  Para exibir essa caixa de diálogo, selecione **Adicionar**  >  **saída do projeto...** no menu de contexto do projeto.

    ![O grupo de saída publicar itens na caixa de diálogo Adicionar grupo de saída do projeto](../deployment/media/installer-projects-net-core-publish-items-output.png "Escolher publicar itens")

2. Para criar um instalador independente, defina a propriedade **PublishProfilePath** no nó **publicar itens** no projeto de instalação, usando o caminho relativo de um perfil de publicação com as propriedades corretas definidas.

    ![Definindo o perfil de publicação no item de saída do projeto publicar itens](../deployment/media/installer-projects-net-core-publish-profile.png "Definir perfil de publicação")

### <a name="prerequisites-for-net-core-31"></a>Pré-requisitos para o .NET Core 3,1

Se você quiser que seu instalador possa instalar o tempo de execução necessário para um aplicativo .NET Core 3,1 dependente de estrutura, você pode fazer isso usando os [pré-requisitos](../deployment/application-deployment-prerequisites.md).  Na caixa de diálogo Propriedades do seu projeto do instalador, abra a caixa de diálogo **pré-requisitos...** e você verá as seguintes entradas:

![Itens do .NET Core na caixa de diálogo pré-requisitos](../deployment/media/installer-projects-net-core-prerequisites.png "Pré-requisitos do .NET Core")

A opção **.NET Core Runtime...** deve ser selecionada para aplicativos de console, **tempo de execução do .net desktop..** . deve ser selecionado para aplicativos WPF/WinForms.

>[!NOTE]
>Esses itens estão presentes a partir da versão do Visual Studio 2019 atualização 7.

## <a name="see-also"></a>Confira também

- [Caixa de diálogo Pré-requisitos](../ide/reference/prerequisites-dialog-box.md)
- [Pré-requisitos de implantação de aplicativo](../deployment/application-deployment-prerequisites.md)
