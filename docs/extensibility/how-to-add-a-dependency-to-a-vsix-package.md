---
title: 'Como: adicionar uma dependência a um pacote VSIX | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- package reference
- package assembly
- package dll
- vsix reference
ms.assetid: 8f20177b-dab9-43a3-b959-81a591b451d6
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 84865bf354bd1822ca872ed5f0df89a4330fb690
ms.sourcegitcommit: 3dd15e019cba7d35dbabc1aa3bf55842a59f5278
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46371037"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>Como: adicionar uma dependência a um pacote VSIX

Você pode configurar uma implantação de pacote VSIX que instala quaisquer dependências que ainda não estão presentes no computador de destino. Para fazer isso, inclua as dependências VSIX para o *vsixmanifest* arquivo.

## <a name="to-add-a-dependency"></a>Para adicionar uma dependência

1. Abra o *vsixmanifest* arquivo na **Design** exibição. Vá para o **dependências** guia e clique em **New**.

2. Para adicionar uma extensão instalada: na **adicionar nova dependência** caixa de diálogo, selecione **extensão instalada** e, em seguida, para o **nome**, selecione uma extensão na lista.

3. Para adicionar outro VSIX que não está instalado: na **adicionar nova dependência** caixa de diálogo, selecione **arquivo no sistema de arquivos** e, em seguida, usar o **procurar** botão para selecionar o VSIX.

## <a name="require-a-specific-visual-studio-release"></a>Exigir uma versão específica do Visual Studio

Se sua extensão requer uma versão específica do Visual Studio 2017, por exemplo, ele depende de um recurso lançado no 15.3, você pode especificar o número de compilação no seu VSIX **InstallationTarget**. Por exemplo, a versão 15.3 tem um número de compilação de '15.0.26730.3'. Você pode ver o mapeamento de lançamentos para números de compilação [aqui](../install/visual-studio-build-numbers-and-release-dates.md). Observe que usando o número de versão '15.3' não funcionará corretamente.

Se sua extensão requer 15.3 ou superior, você poderia declarar o **InstallationTarget versão** como [15.0.26730.3, 16.0):

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```

O VSIXInstaller detectará as versões anteriores do Visual Studio e informar ao usuário que uma atualização posterior é necessária.


## <a name="see-also"></a>Consulte também

 [Referência de esquema 1.0 de extensão do VSIX](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)   
 [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)   
 [Preparar extensões para a implantação do Windows Installer](../extensibility/preparing-extensions-for-windows-installer-deployment.md)
