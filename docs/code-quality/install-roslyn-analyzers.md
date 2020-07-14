---
title: Instalar analisadores do Roslyn
ms.date: 08/03/2018
ms.topic: how-to
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ce30dd25c43f1ac8254dbdb6b04b747a976f3557
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371749"
---
# <a name="install-net-compiler-platform-code-analyzers"></a>Instalar analisadores de código .NET Compiler Platform

O Visual Studio inclui um conjunto principal de analisadores de .NET Compiler Platform (*Roslyn*). Esses analisadores estão sempre ativados. Você pode instalar analisadores adicionais como pacotes NuGet ou como extensões do Visual Studio em arquivos *VSIX* .

## <a name="to-install-nuget-analyzer-packages"></a>Para instalar pacotes do NuGet Analyzer

1. Localize o pacote do analisador que você deseja instalar no www.nuget.org.

   Por exemplo, talvez você queira [instalar os analisadores do Microsoft FxCop](install-fxcop-analyzers.md#nuget-package) para verificar seu código quanto a problemas de segurança e desempenho, entre outros. Ou instale o [StyleCop. Analyzers](https://www.nuget.org/packages/stylecop.analyzers/) para procurar problemas de estilo em sua base de código.

2. Instale o pacote no Visual Studio usando o console do [Gerenciador de pacotes](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console) ou a [interface do usuário do Gerenciador de pacotes](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console).

   > [!NOTE]
   > A página www.nuget.org para cada pacote do analisador mostra o comando a ser colado no **console do Gerenciador de pacotes**. Há até mesmo um botão útil para copiar o texto na área de transferência.

   Os assemblies do analisador são instalados e exibidos em **Gerenciador de soluções** em **References**  >  **analisadores**de referências.

## <a name="to-install-vsix-analyzers"></a>Para instalar os analisadores VSIX

::: moniker range="vs-2017"

1. No Visual Studio, selecione **ferramentas** > **extensões e atualizações**.

   A caixa de diálogo **Extensões e Atualizações** é aberta.

   > [!NOTE]
   > Como alternativa, você pode encontrar e baixar a extensão do analisador diretamente do [Visual Studio Marketplace](https://marketplace.visualstudio.com).

::: moniker-end

::: moniker range=">=vs-2019"

1. No Visual Studio, selecione **extensões** > **gerenciar extensões**.

   A caixa de diálogo **gerenciar extensões** é aberta.

   > [!NOTE]
   > Como alternativa, você pode encontrar e baixar a extensão do analisador diretamente do [Visual Studio Marketplace](https://marketplace.visualstudio.com).

::: moniker-end

2. Expanda **online** no painel esquerdo e, em seguida, selecione **Visual Studio Marketplace**.

3. Na caixa de pesquisa, digite o nome da extensão do analisador que você deseja instalar. Por exemplo, talvez você queira [instalar os analisadores do Microsoft FxCop](install-fxcop-analyzers.md#vsix) para verificar seu código quanto a problemas de segurança e desempenho, entre outros.

4. Selecione **Baixar**.

   A extensão é baixada.

5. Selecione **OK** para fechar a caixa de diálogo e feche todas as instâncias do Visual Studio para iniciar o **instalador VSIX**.

   A caixa de diálogo **instalador do VSIX** é aberta.

   ![Instalador do VSIX para análise de código da Microsoft](media/vsix-installer-code-analysis.png)

6. Selecione **Modificar** para iniciar a instalação.

7. Após um ou dois minutos, a instalação é concluída. Selecione **Fechar**.

8. Abra o Visual Studio novamente.

::: moniker range="vs-2017"

Se você quiser verificar se a extensão está instalada, selecione **ferramentas**  >  **extensões e atualizações**. Na caixa de diálogo **extensões e atualizações** , selecione a categoria **instalado** à esquerda e, em seguida, procure a extensão por nome.

::: moniker-end

::: moniker range=">=vs-2019"

Se você quiser verificar se a extensão está instalada, selecione **extensões**  >  **gerenciar extensões**. Na caixa de diálogo **gerenciar extensões** , selecione a categoria **instalado** à esquerda e, em seguida, procure a extensão por nome.

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Usar analisadores de código no Visual Studio](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>Veja também

- [Visão geral dos analisadores de código no Visual Studio](../code-quality/roslyn-analyzers-overview.md)
- [Instalar analisadores do FxCop](../code-quality/install-fxcop-analyzers.md)
