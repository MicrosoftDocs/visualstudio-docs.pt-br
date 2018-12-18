---
title: Usando o Visual Studio em uma máquina virtual do Azure
description: Saiba como usar o Visual Studio de uma máquina virtual do Azure
ms.date: 09/12/2018
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- azure services
- virtual machine
- installation
- visual studio
author: PhilLee-MSFT
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5d0d51e1c5c3ba94363c2ce0377f3d1a5e22c582
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895836"
---
# <a id="top"> </a> Imagens do visual Studio no Azure

Usar o Visual Studio em uma VM (máquina virtual) do Azure pré-configurada é a maneira mais fácil e rápida de partir do nada para um ambiente de desenvolvimento em execução. Há imagens do sistema com configurações diferentes do Visual Studio disponíveis no [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps?search=%22visual%20studio%202017%22&page=1).

Novo usuário do Azure? [Crie uma conta gratuita do Azure](https://azure.microsoft.com/free).

## <a name="what-configurations-and-versions-are-available"></a>Quais configurações e versões estão disponíveis?

As imagens para as versões principais mais recentes, Visual Studio 2017 e Visual Studio 2015, podem ser encontradas no Azure Marketplace. Para cada versão principal, você pode ver a versão lançada originalmente (RTW) e as versões atualizadas mais recentes. Cada uma dessas versões oferece as edições do Visual Studio Enterprise e do Visual Studio Community. Essas imagens são atualizadas pelo menos uma vez por mês para incluir as atualizações mais recentes do Visual Studio e do Windows. Embora os nomes das imagens permaneçam os mesmos, a descrição de cada imagem inclui a versão instalada do produto e a data "desde" da imagem.

| Versão de lançamento                                              | Edições                     |     Versão do produto      |
|:------------------------------------------------------------:|:----------------------------:|:------------------------:|
|   Visual Studio 2019: versão prévia (Preview 1)                   |           Enterprise         | Versão 16.0.0 Preview 1 |
| Visual Studio 2017: mais recente (versão 15.9)                    |    Enterprise, Community     |      Versão 15.9.0      |
|         Visual Studio 2017: RTW                              |    Enterprise, Community     |      Versão 15.0.18     |
|   Visual Studio 2015 – Mais recente (Atualização 3)                      |    Enterprise, Community     |  Versão 14.0.25431.01   |
|         Visual Studio 2015: RTW                              |             Nenhum             | (Expirado para manutenção)  |

> [!NOTE]
> De acordo com a política de manutenção da Microsoft, a versão lançada originalmente (RTW) do Visual Studio 2015 expirou para manutenção. O Visual Studio 2015 Atualização 3 é a única versão restante oferecida para a linha de produtos do Visual Studio 2015.

Para saber mais, confira [Política de manutenção do Visual Studio](/visualstudio/productinfo/vs-servicing-vs).

## <a name="what-features-are-installed"></a>Quais recursos estão instalados?

Cada imagem contém o recurso recomendado definido para essa edição do Visual Studio. Em geral, a instalação inclui:

* Todas as cargas de trabalho disponíveis, incluindo cada componente opcional recomendado dessa carga de trabalho
* .NET 4.6.2 e .NET 4.7 SDKs, Pacotes de direcionamento e Ferramentas para Desenvolvedores
* Visual F#
* Extensão do GitHub para Visual Studio
* Ferramentas do LINQ to SQL

Usamos a linha de comando a seguir para instalar o Visual Studio ao compilar as imagens:

```shell
    vs_enterprise.exe --allWorkloads --includeRecommended --passive ^
       --add Microsoft.Net.Component.4.7.SDK ^
       --add Microsoft.Net.Component.4.7.TargetingPack ^
       --add Microsoft.Net.Component.4.6.2.SDK ^
       --add Microsoft.Net.Component.4.6.2.TargetingPack ^
       --add Microsoft.Net.ComponentGroup.4.7.DeveloperTools ^
       --add Microsoft.VisualStudio.Component.FSharp ^
       --add Component.GitHub.VisualStudio ^
       --add Microsoft.VisualStudio.Component.LinqToSql
```

Se as imagens não incluírem um recurso do Visual Studio do qual você precisa, forneça comentário por meio da ferramenta de comentários no canto superior direito da página.

## <a name="what-size-vm-should-i-choose"></a>Qual tamanho de VM eu devo escolher?

O Azure oferece uma gama completa de tamanhos de máquina virtual. Como o Visual Studio é um aplicativo multithread poderoso, convém ter um tamanho de VM que inclua pelo menos dois processadores e 7 GB de memória. Recomendamos os seguintes tamanhos de VM para as imagens do Visual Studio:

   * Standard_D2_v3
   * Standard_D2s_v3
   * Standard_D4_v3
   * Standard_D4s_v3
   * Standard_D2_v2
   * Standard_D2S_v2
   * Standard_D3_v2

Para saber mais sobre os tamanhos de máquina mais recentes, veja [Tamanhos de máquinas virtuais do Windows no Azure](/azure/virtual-machines/windows/sizes).

Com o Azure, você pode reequilibrar sua escolha inicial redimensionando a VM. Você pode provisionar uma nova VM com um tamanho mais apropriado, ou redimensionar a VM existente para um hardware subjacente diferente. Para saber mais, confira [Redimensionar uma VM do Windows](/azure/virtual-machines/windows/resize-vm).

## <a name="after-the-vm-is-running-whats-next"></a>Depois que a VM estiver em execução, o que vem a seguir?

O Visual Studio segue o modelo "traga a sua própria licença" no Azure. Assim como em uma instalação em hardware proprietário, uma das primeiras etapas é o licenciamento de sua instalação do Visual Studio. Para desbloquear o Visual Studio:
- Entre com uma conta da Microsoft associada a uma assinatura do Visual Studio
- Desbloqueie o Visual Studio com a chave do produto que acompanha a compra inicial

Para saber mais, confira [Entrar no Visual Studio](../ide/signing-in-to-visual-studio.md) e [Como desbloquear o Visual Studio](../ide/how-to-unlock-visual-studio.md).

## <a name="how-do-i-save-the-development-vm-for-future-or-team-use"></a>Como posso salvar a VM de desenvolvimento para uso futuro ou da equipe?

O espectro de ambientes de desenvolvimento é grande, e não há um custo real associado à compilação de ambientes mais complexos. Independentemente da configuração do seu ambiente, você pode salvar ou capturar sua VM configurada como uma "imagem base" para uso futuro, ou para outros membros da equipe. Em seguida, ao inicializar uma nova VM, provisione-a desde a imagem base em vez de a imagem do Azure Marketplace.

Um resumo rápido: use a ferramenta System Preparation (Sysprep) e desligue a VM em execução, depois capture *(Figura 1)* a VM como uma imagem por meio da interface do usuário no Portal do Azure. O Azure salva o arquivo `.vhd` que contém a imagem na conta de armazenamento de sua escolha. A nova imagem, em seguida, aparecerá como um recurso de imagem na lista de recursos de sua assinatura.

<img src="media/capture-vm.png" alt="Capture an image through the Azure portal’s UI" style="border:3px solid Silver; display: block; margin: auto;"><center>*(Figura 1) Capture uma imagem por meio da interface do usuário do Portal do Azure.*</center>

Para saber mais, veja [Criar uma imagem gerenciada de uma VM generalizada no Azure](/azure/virtual-machines/windows/capture-image-resource).

> [!IMPORTANT]
> Não se esqueça de usar o Sysprep para preparar a máquina virtual. Se você ignorar esta etapa, o Azure não poderá provisionar uma VM a partir da imagem.

> [!NOTE]
> Você ainda incorrerá em custos para o armazenamento das imagens, mas provavelmente esse custo incremental poderá ser insignificante em comparação aos custos de sobrecarga para recompilar a VM desde o início para cada membro da equipe que precisa de uma. Por exemplo, custa apenas alguns dólares criar e armazenar uma imagem de 127 GB por um mês que seja reutilizável por toda a equipe. No entanto, esses custos são insignificantes em comparação com as horas investidas por cada funcionário para compilar e validar uma caixa de desenvolvimento configurada corretamente para o uso individual.

Além disso, talvez as tarefas de desenvolvimento ou as tecnologias precisem de mais escala como variedades de configurações de desenvolvimento e várias configurações de máquina. Você pode usar o Azure DevTest Labs para criar _receitas_ que automatizam a construção de sua "imagem dourada". Você também pode usar o DevTest Labs para gerenciar políticas para as VMs em execução da sua equipe. [O Azure DevTest Labs para desenvolvedores](/azure/devtest-lab/devtest-lab-developer-lab) é a melhor fonte para obter mais informações sobre o DevTest Labs.

## <a name="next-steps"></a>Próximas etapas

Agora que você já conhece as imagens pré-configuradas do Visual Studio, a próxima etapa é criar uma nova VM:

* [Criar uma VM por meio do Portal do Azure](/azure/virtual-machines/windows/quick-create-portal)
* [Visão geral das máquinas virtuais do Windows](/azure/virtual-machines/windows/overview)
