---
title: Instalar um | Microsoft Docs
description: Entenda como instalar um visualizador para que ele estará disponível para uso de depuração em Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 07/02/2021
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, visualizers
- visualizers, installing
ms.assetid: 3310ef43-515c-4d97-b0f9-51047247d3da
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 611347acfe48e561653d644097d56d029b6a4fa6
ms.sourcegitcommit: 4cd3eb514e9fa48e586279e38fe7c2e111ebb304
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2021
ms.locfileid: "113298251"
---
# <a name="how-to-install-a-visualizer"></a>Como instalar um visualizador
Após ter criado um visualizador, você deverá instalar o visualizador de modo que esteja disponível em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Instalar um visualizador é um processo simples.

> [!NOTE]
> Em aplicativos UWP, há suporte apenas para visualizadores de texto padrão, HTML, XML e JSON. Não há suporte para visualizadores personalizados (criados pelo usuário).

::: moniker range=">=vs-2019"
### <a name="to-install-a-visualizer-for-visual-studio-2019"></a>Para instalar um visualizador do Visual Studio 2019

1. Localize a DLL que contém o visualizador que você criou.

   Normalmente, é melhor que a DLL do lado do depurador e a DLL do lado do depurador especifiquem Qualquer **CPU** como a plataforma de destino. A DLL do lado do depurador deve ser **Qualquer CPU** ou **32 bits.** A plataforma de destino para a DLL do lado do rodo de depuração deve corresponder ao processo de depuração.

   >[!NOTE]
   > O visualizador do lado do depurador é carregado no processo Visual Studio, portanto, ele deve ser um .NET Framework DLL. O lado de depuração pode ser .NET Framework ou .NET Standard dependendo de qual processo está sendo depurado Visual Studio.

2. Copie a DLL [lateral](create-custom-visualizers-of-data.md#to-create-the-debugger-side) do depurador (e as DLLs das que ela depende) para um dos seguintes locais:

    - *VisualStudioInstallPath* `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` *VisualStudioVersion* `\Visualizers`

3. Copie a [DLL do lado de depuração](create-custom-visualizers-of-data.md#to-create-the-visualizer-object-source-for-the-debuggee-side) para qualquer um dos seguintes locais:

    - *VisualStudioInstallPath* `\Common7\Packages\Debugger\Visualizers\` *Estrutura*

    - `My Documents\`*VisualStudioVersion* `\Visualizers\` *Estrutura*

    em *que Framework* é:
    - `net2.0` para depuração que executa o `.NET Framework` runtime.
    - `netstandard2.0` para depuração usando um runtime que dá suporte `netstandard 2.0` a ( `.NET Framework v4.6.1+` ou `.NET Core 2.0+` ).
    - `netcoreapp` para depuração que executa o `.NET Core` runtime. (dá suporte `.NET Core 2.0+` a )

   Uma DLL do lado do rodo de depuração será necessária se você quiser criar um visualizador autônomo. Essa DLL contém código para o objeto de dados, que pode implementar métodos de <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> .

   Se você estiver direcionando para vários destinos o código do lado do rodo de depuração, a DLL do lado do rodo de depuração deverá ser colocada na pasta para o TFM com suporte mínimo.

4. Reinicie a sessão de depuração.

> [!NOTE]
> O procedimento é diferente no Visual Studio 2017 e mais antigo. Consulte a [versão anterior](how-to-install-a-visualizer.md?view=vs-2017&preserve-view=true) deste artigo.
::: moniker-end

::: moniker range="vs-2017"
### <a name="to-install-a-visualizer-for-visual-studio-2017-and-older"></a>Para instalar um visualizador do Visual Studio 2017 e mais antigo

> [!IMPORTANT]
> Somente .NET Framework visualizadores têm suporte no Visual Studio 2017 e versões mais antigas.

1. Localize a DLL que contém o visualizador que você criou.

2. Copie a DLL para qualquer um dos seguintes locais:

    - *VisualStudioInstallPath* `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` *VisualStudioVersion* `\Visualizers`

3. Reinicie a sessão de depuração.

> [!NOTE]
> Se você quiser usar um visualizador gerenciado para a depuração remota, copie a DLL no mesmo caminho no computador remoto.
::: moniker-end

## <a name="see-also"></a>Confira também
- [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)
- [Como escrever um visualizador](create-custom-visualizers-of-data.md)
