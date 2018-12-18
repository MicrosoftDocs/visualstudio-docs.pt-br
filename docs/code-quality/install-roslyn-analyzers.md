---
title: Instalar analisadores do Roslyn
ms.date: 08/03/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: aa0805b3cffe5a44ae2c6198c6ca2682ceca9f95
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49865395"
---
# <a name="install-net-compiler-platform-analyzers"></a>Instalar analisadores do .NET Compiler Platform

Visual Studio 2017 inclui um conjunto principal de plataforma do compilador .NET (*Roslyn*) analisadores. Esses analisadores estão sempre ativados. Você pode instalar outros analisadores como pacotes NuGet ou como extensões do Visual Studio no *VSIX* arquivos.

## <a name="to-install-nuget-analyzer-packages"></a>Para instalar os pacotes do NuGet analyzer

1. Localize o pacote de analisador que você deseja instalar em www.nuget.org. Por exemplo, você talvez queira [instalar os analisadores FxCop Microsoft](install-fxcop-analyzers.md#to-install-fxcop-analyzers-as-a-nuget-package) para verificar seu código para problemas de segurança e desempenho, entre outros.

2. Instale o pacote no Visual Studio, usando o [Package Manager Console](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console) ou o [UI Gerenciador de pacotes](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console).

   > [!NOTE]
   > A página www.nuget.org para cada pacote de analisador mostra o comando Colar na **Package Manager Console**. Há até mesmo um botão útil para copiar o texto na área de transferência.
   > 
   > ![Página de NuGet.org mostrando o comando do Console do Gerenciador de pacotes](media/nuget-install-command.png)

   Os assemblies do analisador são instalados e aparecem na **Gerenciador de soluções** sob **referências** > **analisadores**.

## <a name="to-install-vsix-analyzers"></a>Para instalar analisadores VSIX

1. No Visual Studio, selecione **ferramentas** > **extensões e atualizações**.

   A caixa de diálogo **Extensões e Atualizações** é aberta.

   > [!NOTE]
   > Como alternativa, você pode localizar e baixar a extensão de analisador diretamente a partir [Visual Studio Marketplace](https://marketplace.visualstudio.com).

2. Expandir **Online** no painel esquerdo e, em seguida, selecione **Visual Studio Marketplace**.

3. Na caixa de pesquisa, digite o nome da extensão do analisador que você deseja instalar. Por exemplo, você talvez queira [instalar os analisadores FxCop Microsoft](install-fxcop-analyzers.md#to-install-fxcop-analyzers-as-a-vsix) para verificar seu código para problemas de segurança e desempenho, entre outros.

4. Selecione **baixar**.

   A extensão é baixada.

5. Selecione **Okey** para fechar a caixa de diálogo e, em seguida, feche todas as instâncias do Visual Studio para iniciar o **instalador do VSIX**.

   O **instalador do VSIX** caixa de diálogo é aberta.

   ![Instalador do VSIX para análise de código da Microsoft](media/vsix-installer-code-analysis.png)

6. Selecione **modificar** para iniciar a instalação.

7. Depois de um ou dois minutos, a instalação for concluída. Selecione **fechar**.

8. Abra o Visual Studio novamente.

Se você deseja verificar se a extensão é instalada, selecione **ferramentas** > **extensões e atualizações**. No **extensões e atualizações** caixa de diálogo, selecione o **instalado** categoria à esquerda e, em seguida, pesquise a extensão pelo nome.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Usar os analisadores de Roslyn no Visual Studio](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>Consulte também

- [Visão geral dos analisadores de Roslyn no Visual Studio](../code-quality/roslyn-analyzers-overview.md)
- [Instalar analisadores FxCop](../code-quality/install-fxcop-analyzers.md)