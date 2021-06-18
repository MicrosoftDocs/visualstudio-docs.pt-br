---
title: Destino Visual Studio 2019 ao criar uma extensão no Visual Studio 2022 Preview
description: Saiba como fazer com que sua extensão Visual Studio funcione com o Visual Studio 2019 se você criar o projeto com o Visual Studio 2022 Preview.
ms.date: 06/08/2021
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: dcf556e271e6a805110eac0c978a845f2195e28f
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308674"
---
# <a name="target-a-previous-version-when-creating-an-extension-in-visual-studio-2022-preview"></a>Direcionar uma versão anterior ao criar uma extensão no Visual Studio Versão Prévia 2022

[!INCLUDE [preview-note](../includes/preview-note.md)]

Quando você cria um novo projeto VSIX usando o Visual Studio Versão Prévia 2022, o projeto é criado com um modelo destinado ao Visual Studio 2022. Se você quiser direcionar Visual Studio 2019 ou uma versão anterior, modifique o projeto criado.

Considere usar [projetos compartilhados](update-visual-studio-extension.md#use-shared-projects-for-multi-targeting) para direcionar Visual Studio 2019 e Visual Studio 2022 enquanto compartilha a maior parte ou todo o código em sua extensão.

Siga estas etapas no projeto VSIX que deve ser Visual Studio 2019:

1. Edite `source.extension.vsixmanifest` o arquivo para remover o elemento e o intervalo de `ProductArchitecture` versão:

    ```diff
    -<InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
    +<InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[16.0,17.0)">
    -  <ProductArchitecture>amd64</ProductArchitecture>
     </InstallationTarget>
    ```

   Atualize também o pré-requisito:

    ```diff
    -<Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[17.0,18.0)" DisplayName="Visual Studio core editor" />
    +<Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[16.0,17.0)" DisplayName="Visual Studio core editor" />
    ```

    Revise o arquivo para ver se há outras atualizações que possam ser necessárias.

1. Altere as versões dos pacotes do SDK do VS que você referencia no arquivo de projeto:

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    ```
