---
title: Usando o Visual Studio em uma máquina virtual do Azure
titleSuffix: ''
description: Saiba como usar o Visual Studio de uma máquina virtual do Azure
ms.date: 12/06/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- azure services
- virtual machine
- installation
- visual studio
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 8daf933292c521bb50d294dff2a380b130a4f2ce
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2020
ms.locfileid: "76113808"
---
# <a name="visual-studio-images-on-azure"></a><a id="top"> </a> Imagens do Visual Studio no Azure

Usar o Visual Studio executando em uma máquina virtual (VM) do Azure pré-configurada é a maneira mais fácil e rápida de partir do nada para um ambiente de desenvolvimento atualizado. As imagens do sistema com diferentes configurações do Visual Studio estão disponíveis no [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/compute?filters=virtual-machine-images%3Bmicrosoft%3Bwindows&page=1&subcategories=application-infrastructure).

Você é novo no Azure? [Crie uma conta gratuita do Azure](https://azure.microsoft.com/free).

## <a name="what-configurations-and-versions-are-available"></a>Quais configurações e versões estão disponíveis?

As imagens para as versões principais mais recentes, Visual Studio 2019, Visual Studio 2017 e Visual Studio 2015, podem ser encontradas no Azure Marketplace.  Para cada versão principal lançada, você verá a versão RTW (lançada originalmente para a Web) e as últimas versões atualizadas.  Cada uma dessas versões oferece as edições do Visual Studio Enterprise e Visual Studio Community.  Essas imagens são atualizadas pelo menos uma vez por mês para incluir as atualizações mais recentes do Visual Studio e do Windows.  Embora os nomes das imagens permaneçam os mesmos, a descrição de cada imagem inclui a versão do produto instalada e a data inicial da imagem.

| Versão de lançamento                                                                                                                                          | Edições              |    Versão do produto    |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------:|:-----------------------:|
| [Visual Studio 2019: Mais recente (Versão 16.4)](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio2019latest?tab=Overview) | Enterprise, Community | Versão 16.4.0    |
| [Visual Studio 2019: RTW](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio2019?tab=Overview)                         | Enterprise            | Versão 16.0.9    |
| [Visual Studio 2017: Versão mais recente (versão 15,9)](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio?tab=Overview)           | Enterprise, Community | Versão 15.9.17   |
| [Visual Studio 2017: RTW](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio?tab=Overview)                             | Enterprise, Community | Versão 15.0.27   |
| [Visual Studio 2015: Última (Atualização 3)](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio?tab=Overview)               | Enterprise, Community | Versão 14.0.25431.01 |

> [!NOTE]
> De acordo com a política de atendimento da Microsoft, a versão original (RTW) do Visual Studio 2015 expirou para manutenção. O Visual Studio 2015 Atualização 3 é a única versão restante oferecida para a linha de produtos Visual Studio 2015.

Para obter mais informações, consulte a [Política de Atendimento do Visual Studio](/visualstudio/productinfo/vs-servicing-vs).

## <a name="what-features-are-installed"></a>Quais recursos são instalados?

Cada imagem contém o conjunto de recursos recomendado para essa edição do Visual Studio. Geralmente, a instalação inclui:

* Todas as cargas de trabalho disponíveis, incluindo cada componente opcional recomendado da carga de trabalho
* .NET 4.6.2 e .NET 4.7 SDKs, Pacotes de Destino, e Ferramentas para Desenvolvedores
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

Se as imagens não incluírem um recurso do Visual Studio que você precise, envie um comentário pela ferramenta de comentários no canto superior direito da página.

## <a name="what-size-vm-should-i-choose"></a>Qual tamanho de VM devo escolher?

O Azure oferece uma gama completa de tamanhos de máquina virtual. Uma vez que o Visual Studio é um aplicativo multi-thread avançado, você quer um tamanho de VM que inclua pelo menos dois processadores e 7 GB de memória. Estes são os tamanhos de VM recomendados para as imagens do Visual Studio:

* Standard_D2_v3
* Standard_D2s_v3
* Standard_D4_v3
* Standard_D4s_v3
* Standard_D2_v2
* Standard_D2S_v2
* Standard_D3_v2

Para obter mais informações sobre os tamanhos das máquinas mais recentes, consulte [Tamanhos das máquinas virtuais do Windows no Azure](/azure/virtual-machines/windows/sizes).

Com o Azure, é possível reequilibrar sua escolha inicial redimensionando a VM. É possível fornecer uma nova VM com um tamanho mais apropriado ou redimensionar sua VM existente para hardware subjacente diferente. Para obter mais informações, consulte [Redimensionar uma VM do Windows](/azure/virtual-machines/windows/resize-vm).

## <a name="after-the-vm-is-running-whats-next"></a>Depois que a VM estiver em execução, o que vem a seguir?

O Visual Studio acompanha o modelo "traga sua própria licença" no Azure. De forma semelhante a uma instalação em hardware proprietário, uma das primeiras etapas é o licenciamento da instalação do Visual Studio. Para desbloquear o Visual Studio:
- Entrar com uma conta da Microsoft associada a uma assinatura do Visual Studio
- Desbloquear o Visual Studio com a chave do produto que acompanha a compra inicial

Para obter mais informações, consulte [Conectar-se ao Visual Studio](../ide/signing-in-to-visual-studio.md) e [Como desbloquear o Visual Studio](../ide/how-to-unlock-visual-studio.md).

## <a name="how-do-i-save-the-development-vm-for-future-or-team-use"></a>Como posso salvar a VM de desenvolvimento para uso futuro ou da equipe?

O espectro de ambientes de desenvolvimento é imenso e há custos reais associados à compilação de ambientes mais complexos. Independentemente da configuração do seu ambiente, você pode salvar ou capturar sua VM configurada como uma "imagem base" para uso futuro ou para outros membros da sua equipe. A seguir, ao inicializar uma nova VM, provisione-a a partir da imagem base e não da imagem do Marketplace do Azure.

Um resumo rápido: Utilize a ferramenta de Preparação do Sistema (Sysprep) e desligue a VM em execução, a seguir, capture *(Figura 1)* a VM como uma imagem através da Interface do Usuário no portal do Azure. O Azure salva o arquivo `.vhd` que contém a imagem, na conta de armazenamento de sua escolha. A nova imagem aparecerá como um recurso de imagem na lista de recursos da sua assinatura.

![Capturar uma imagem por meio da interface do usuário do portal do Azure](media/capture-vm.png)

*(Figura 1) Capturar uma imagem através da interface do usuário do Portal do Azure.*

Para obter mais informações, consulte [Criar uma imagem gerenciada de uma VM generalizada no Azure](/azure/virtual-machines/windows/capture-image-resource).

> [!IMPORTANT]
> Não se esqueça de usar o Sysprep para preparar a máquina virtual. Se essa etapa for ignorada, o Azure não poderá fornecer uma VM da imagem.

> [!NOTE]
> Você ainda tem algum custo para o armazenamento das imagens, mas esse custo incremental pode ser insignificante em comparação aos custos de despesas gerais para reconstruir a VM a partir do zero para cada membro da equipe que precise de uma. Por exemplo, há o custo de alguns dólares para criar e armazenar uma imagem de 127 GB por um mês que é reutilizável por todos os membros de sua equipe. No entanto, esses custos são insignificantes em comparação com as horas que cada funcionário investe para compilar e validar um desenvolvimento de caixa devidamente configurado para o uso individual.

Além disso, suas tarefas ou tecnologias de desenvolvimento podem precisar de mais escala, como variedades de configurações de desenvolvimento e múltiplas configurações de computadores. Você pode usar o Azure DevTest Labs para criar _receitas_ que automatizam a construção de sua "imagem dourada". Você também pode usar o DevTest Labs para gerenciar políticas para as VMS em execução da sua equipe. [Usar Azure DevTest Labs para desenvolvedores](/azure/devtest-lab/devtest-lab-developer-lab) é a melhor fonte para obter mais informações sobre DevTest Labs.

## <a name="next-steps"></a>Próximas etapas

Agora que você conhece as imagens pré-configuradas do Visual Studio, a próxima etapa é criar uma nova VM:

* [Criar uma VM através do Portal do Azure](/azure/virtual-machines/windows/quick-create-portal)
* [Visão geral de Máquinas Virtuais do Windows](/azure/virtual-machines/windows/overview)
