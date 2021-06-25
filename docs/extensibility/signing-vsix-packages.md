---
title: Assinando pacotes VSIX | Microsoft Docs
description: Saiba mais sobre como assinar assemblies de extensão. O instalador do VSIX exibe uma mensagem informando que um VSIX está assinado e informações sobre a assinatura em si.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: d481c75754c7bc49369987d4bf6dc3aa33e96fdc
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899154"
---
# <a name="signing-vsix-packages"></a>Assinando pacotes VSIX
Os assemblies de extensão não precisam ser assinados antes que possam ser executados no Visual Studio, mas é uma boa prática fazer isso.

 Se você quiser proteger sua extensão e certificar-se de que ela não foi violada, você pode adicionar uma assinatura digital a um pacote VSIX. Quando um VSIX é assinado, o instalador do VSIX exibirá uma mensagem indicando que ele está assinado, além de mais informações sobre a assinatura em si. Se o conteúdo do VSIX tiver sido modificado e o VSIX não tiver sido assinado novamente, o instalador do VSIX mostrará que a assinatura não é válida. A instalação não é interrompida, mas o usuário é avisado.

> [!IMPORTANT]
> A partir do Visual Studio 2015, os pacotes VSIX assinados usando qualquer coisa diferente da criptografia SHA256 serão identificados como tendo uma assinatura inválida. A instalação do VSIX não está bloqueada, mas o usuário será avisado.

## <a name="signing-a-vsix-with-vsixsigntool"></a>Assinando um VSIX com VSIXSignTool
 Há uma ferramenta de assinatura de criptografia SHA256 disponível em [VisualStudioExtetool](https://www.nuget.org/profiles/VisualStudioExtensibility) no nuget.org [vsixSignTool.](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool)

#### <a name="to-use-the-vsixsigntool"></a>Para usar o VSIXSignTool

1. Adicione o VSIX a um projeto.

2. Clique com o botão direito do mouse no nó do projeto Gerenciador de Soluções, **selecionando Adicionar &#124; Gerenciar Pacotes NuGet**.  Para obter mais informações sobre o NuGet e adicionar pacotes NuGet, consulte a documentação do [NuGet](/NuGet) [e Gerenciador de Pacotes da interface](/NuGet/Tools/Package-Manager-UI) do usuário.

3. Pesquise VSIXSignTool em VisualStudioExtetool e instale o pacote NuGet.

4. Agora você pode executar o VSIXSignTool no local de pacotes locais do projeto. Consulte a ajuda de linha de comando da ferramenta para seu cenário de assinatura (VSIXSignTool.exe /?).

   Por exemplo, para assinar com um arquivo de certificado protegido por senha:

   VSIXSignTool.exe /f \<certfile> /p \<password>\<VSIXfile>

## <a name="see-also"></a>Confira também
- [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)
