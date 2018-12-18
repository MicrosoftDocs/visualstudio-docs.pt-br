---
title: Instalar analisadores do FxCop
ms.date: 08/03/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- fxcop analyzers
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 7690d1c67797c3a13dc22364d93d8af686e4f90c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49892045"
---
# <a name="install-fxcop-analyzers-in-visual-studio"></a>Instalar analisadores FxCop no Visual Studio

A Microsoft criou um conjunto de analisadores, chamado [fxcopanalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers), que contém as regras de "FxCop" mais importante da análise de código estático, convertido em Analisadores de Roslyn. Esses analisadores Verifique seu código de segurança, desempenho e problemas de design, entre outros.

Você pode instalar esses analisadores FxCop como um pacote do NuGet ou como uma extensão do VSIX para Visual Studio. Para saber mais sobre os prós e contras de cada um, consulte [vs de pacote do NuGet. Extensão do VSIX](roslyn-analyzers-overview.md#nuget-package-versus-vsix-extension).

## <a name="to-install-fxcop-analyzers-as-a-nuget-package"></a>Para instalar analisadores FxCop como um pacote do NuGet

1. [Determinar qual versão do pacote de analisador](#fxcopanalyzers-package-versions) instalar, com base em sua versão do Visual Studio.

2. Instale o pacote no Visual Studio, usando o [Package Manager Console](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console) ou o [UI Gerenciador de pacotes](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console).

   > [!NOTE]
   > A página de nuget.org para cada pacote de analisador mostra o comando para colar o **Package Manager Console**. Há até mesmo um botão útil para copiar o texto na área de transferência.
   >
   > ![Página de NuGet.org mostrando o comando do Console do Gerenciador de pacotes](media/nuget-package-manager-command.png)

   Os assemblies do analisador são instalados e eles aparecem no **Gerenciador de soluções** sob **referências** > **analisadores**.

   ![Nó de analisadores no Gerenciador de soluções](media/solution-explorer-analyzers-node.png)

### <a name="fxcopanalyzers-package-versions"></a>Versões do pacote FxCopAnalyzers

Use as diretrizes a seguir para determinar qual versão do pacote de analisadores FxCop para instalar o para sua versão do Visual Studio:

| Versão do Visual Studio | Versão do pacote de analisador de FxCop |
| - | - |
| Visual Studio 2017 versão 15.5 e posterior | 2.6.2, por exemplo https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.6.2 |
| Visual Studio 2017 versão 15.3 para 15.4 | 2.3.0-Beta1, por exemplo https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.3.0-beta1 |
| Visual Studio 2017 versão 15.0 para 15.2 | 2.0.0-Beta2, por exemplo https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.0.0-beta2 |
| Visual Studio 2015 atualização 2 e 3 | Versão 1.2.0-beta2, por exemplo https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.2.0-beta2 |
| Visual Studio 2015 Atualização 1 | A versão 1.1.0, por exemplo https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.1. |
| Visual Studio 2015 RTW | Versão 1.0.1, por exemplo https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.0.1 |

## <a name="to-install-fxcop-analyzers-as-a-vsix"></a>Para instalar analisadores FxCop como um VSIX

No Visual Studio 2017 versão 15.5 e posteriores, você pode instalar o [2017 de análise de código Microsoft](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017) extensão que contém todos os analisadores FxCop para projetos gerenciados.

1. No Visual Studio, selecione **ferramentas** > **extensões e atualizações**.

   A caixa de diálogo **Extensões e Atualizações** é aberta.

   > [!NOTE]
   > Como alternativa, baixe a extensão diretamente [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017).

1. Expandir **Online** no painel esquerdo e, em seguida, selecione **Visual Studio Marketplace**.

1. Na caixa de pesquisa, digite "análise de código" e procure o **2017 de análise de código Microsoft** extensão.

   ![Extensão de análise de código da Microsoft](media/extensions-and-updates-code-analysis.png)

1. Selecione **baixar**.

   A extensão é baixada.

1. Selecione **Okey** para fechar a caixa de diálogo e, em seguida, feche todas as instâncias do Visual Studio para iniciar o **instalador do VSIX**.

   O **instalador do VSIX** caixa de diálogo é aberta.

   ![Instalador do VSIX para análise de código da Microsoft](media/vsix-installer-code-analysis.png)

1. Selecione **modificar** para iniciar a instalação.

1. Depois de um ou dois minutos, a instalação for concluída. Selecione **fechar**.

1. Abra o Visual Studio novamente.

Se você deseja verificar se a extensão é instalada, selecione **ferramentas** > **extensões e atualizações**. No **extensões e atualizações** caixa de diálogo, selecione o **instalado** categoria à esquerda e, em seguida, pesquise a extensão pelo nome.

## <a name="see-also"></a>Consulte também

- [Visão geral dos analisadores de Roslyn no Visual Studio](../code-quality/roslyn-analyzers-overview.md)
- [Usar os analisadores de Roslyn no Visual Studio](../code-quality/use-roslyn-analyzers.md)
- [Migrar do FxCop para analisadores de Roslyn](../code-quality/fxcop-analyzers.yml)