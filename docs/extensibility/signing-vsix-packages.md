---
title: Assinando pacotes VSIX | Microsoft Docs
description: Saiba mais sobre assemblies de extensão de assinatura. O instalador do VSIX exibe uma mensagem informando que um VSIX está assinado e informações sobre a própria assinatura.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- signature
- signing
- authenticode
- vsix
- packages
ms.assetid: e34cfc2c-361c-44f8-9cfe-9f2be229d248
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c2a2c9703eb41c1a3e5baa023d8240b56ccbb13b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056357"
---
# <a name="signing-vsix-packages"></a>Assinando pacotes VSIX
Os assemblies de extensão não precisam ser assinados antes que possam ser executados no Visual Studio, mas é uma boa prática fazer isso.

 Se você quiser proteger sua extensão e verificar se ela não foi violada, você pode adicionar uma assinatura digital a um pacote VSIX. Quando um VSIX é assinado, o instalador do VSIX exibirá uma mensagem indicando que ela está assinada, além de mais informações sobre a própria assinatura. Se o conteúdo do VSIX tiver sido modificado e o VSIX não tiver sido assinado novamente, o instalador do VSIX mostrará que a assinatura não é válida. A instalação não é interrompida, mas o usuário é avisado.

> [!IMPORTANT]
> A partir do Visual Studio 2015, os pacotes VSIX assinados usando algo diferente da criptografia SHA256 serão identificados como tendo uma assinatura inválida. A instalação do VSIX não está bloqueada, mas o usuário será avisado.

## <a name="signing-a-vsix-with-vsixsigntool"></a>Assinando um VSIX com o VSIXSignTool
 Há uma ferramenta de assinatura de criptografia SHA256 disponível em [VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility) em NuGet.org em [VsixSignTool](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool).

#### <a name="to-use-the-vsixsigntool"></a>Para usar o VSIXSignTool

1. Adicione seu VSIX a um projeto.

2. Clique com o botão direito do mouse no nó do projeto em Gerenciador de Soluções, selecionando **adicionar &#124; gerenciar pacotes NuGet**.  Para obter mais informações sobre o NuGet e adicionar pacotes NuGet, consulte a [documentação do NuGet](/NuGet) e os tópicos de [interface do usuário do Gerenciador de pacotes](/NuGet/Tools/Package-Manager-UI) .

3. Procure VSIXSignTool de VisualStudioExtensibility e instale o pacote NuGet.

4. Agora você pode executar o VSIXSignTool no local de pacotes locais do projeto. Consulte a ajuda de linha de comando da ferramenta para seu cenário de assinatura (VSIXSignTool.exe/?).

   Por exemplo, para assinar um arquivo de certificado protegido por senha:

   Sinal de VSIXSignTool.exe/f \<certfile> /p \<password>\<VSIXfile>

## <a name="see-also"></a>Confira também
- [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)
