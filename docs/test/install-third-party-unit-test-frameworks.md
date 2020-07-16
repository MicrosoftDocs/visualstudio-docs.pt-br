---
title: Instalar estruturas de teste de unidade de terceiros
ms.date: 07/09/2020
ms.topic: how-to
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: c274f203b9bf2746716c0625c61141aaa332977a
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387181"
---
# <a name="install-unit-test-frameworks"></a>Instalar estruturas de teste de unidade

O Gerenciador de Testes do Visual Studio pode executar testes de qualquer estrutura de teste de unidade que desenvolveu uma interface de adaptador para ele. A instalação da estrutura copia os binários e adiciona modelos de projeto do Visual Studio para os idiomas que ele dá suporte. Quando você cria um projeto com o modelo, a estrutura é registrada com o Gerenciador de Testes.

Uma solução do Visual Studio pode conter projetos de teste de unidade que usam diferentes estruturas e que são direcionados em diferentes idiomas.

::: moniker range=">=vs-2019"
Para .NET, [MSTest, NUnit e xUnit](getting-started-with-unit-testing.md) são as estruturas de teste fornecidas pelo Visual Studio que são instaladas por padrão.
::: moniker-end
::: moniker range="vs-2017"
O [MSTest](getting-started-with-unit-testing.md) é a estrutura de teste fornecida pelo Visual Studio e é instalada por padrão.
::: moniker-end

## <a name="acquire-frameworks"></a>Adquirir estruturas

Instalar estruturas de teste de unidade de terceiros usando o **Gerenciador de Pacotes do NuGet**.

1. Clique com o botão direito do mouse no projeto que conterá o código de teste e selecione **Gerenciar Pacotes do NuGet**.

2. No **Gerenciador de Pacotes do NuGet**, procure a estrutura de teste que você deseja instalar e, em seguida, clique em **Instalar**.

   ![Gerenciador de Pacotes do NuGet no Visual Studio](media/vs-2019/nuget-package-manager.png)

## <a name="update-to-the-latest-test-adapters"></a>Atualizar para os adaptadores de teste mais recentes

Atualização para o adaptador de teste estável mais recente para aproveitar melhor a detecção e a execução de teste. Para saber mais sobre atualizações para adaptadores de teste MSTest, NUnit e xUnit, veja o [blog do Visual Studio](https://devblogs.microsoft.com/visualstudio/test-experience-improvements/).

### <a name="to-update-to-the-latest-stable-test-adapter-version"></a>Para atualizar para a versão estável mais recente do adaptador de teste

1. Abra o Gerenciador de pacotes NuGet para sua solução navegando até **ferramentas**  >  **Gerenciador de pacotes NuGet**  >  **gerenciar pacotes NuGet para solução**.

2. Clique na guia **Atualizações** e pesquise os adaptadores de teste do MSTest, NUnit ou xUnit que estão instalados.

3. Selecione cada adaptador de teste e, em seguida, selecione a última versão estável no menu suspenso.

4. Escolha o botão **Instalar**.

   ![Atualizar adaptador de teste](media/install-adapter-upgrade.png)

## <a name="see-also"></a>Confira também

- [Teste de unidade em seu código](../test/unit-test-your-code.md)
