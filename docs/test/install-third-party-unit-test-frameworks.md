---
title: Instalar estruturas de teste de unidade de terceiros
ms.date: 06/07/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: ffd6b8c66f0575ec07e66ea2a138f2761b20cc7a
ms.sourcegitcommit: 495bba1d8029646653f99ad20df2f80faad8d58b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39379632"
---
# <a name="install-third-party-unit-test-frameworks"></a>Instalar estruturas de teste de unidade de terceiros

O Gerenciador de Testes do Visual Studio pode executar qualquer estrutura de teste de unidade que desenvolveu uma interface de adaptador para o Gerenciador. O programa de instalação da estrutura instala os binários e adiciona modelos de projeto do Visual Studio para os idiomas que ele dá suporte. Quando você cria um projeto com o modelo, a estrutura é registrada com o Gerenciador de Testes. Uma solução do Visual Studio pode conter projetos de teste de unidade que usam diferentes estruturas e que são direcionados em diferentes idiomas. O Gerenciador de Testes executa todos eles.

## <a name="acquire-third-party-frameworks"></a>Adquirir estruturas de terceiros

Você pode baixar e instalar diversas estruturas de teste de unidade de terceiros usando o Gerenciador de Extensões do Visual Studio ou o Visual Studio Marketplace. Estruturas também podem ser baixadas de outros sites, como o site da estrutura.

### <a name="install-from-visual-studio"></a>Instalar do Visual Studio

1. Escolha **Ferramentas** no menu padrão e, em seguida, selecione **Extensões e atualizações**.

2. Expanda **Online** > **Visual Studio Marketplace** > **Ferramentas**. Escolha **Teste**.

3. Navegue pela lista para localizar a estrutura.

4. Selecione a estrutura e escolha **Download**.

Para obter mais informações, confira [Localizar e usar extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md).

### <a name="install-from-the-web"></a>Instalação da Web

Se você souber a estrutura em que você está interessado:

1. Abra [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs).

2. Digite o nome da estrutura na caixa **Localizar**.

3. Escolha a estrutura na lista de resultados para navegar para a página do **Visual Studio Marketplace** da ferramenta.

Para procurar uma lista de estruturas juntamente com outras ferramentas de teste:

1. Abra [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs).

2. Em **Filtrar por categoria/coleção**, escolha **Ver tudo**.

3. Na lista **Categoria** (rotulada como **Mostrando**), expanda o nó **Ferramentas** e, em seguida, escolha **Teste**.

4. Escolha uma estrutura na lista de resultados para navegar para uma página do **Visual Studio Marketplace** da ferramenta.

## <a name="update-to-the-latest-test-adapters"></a>Atualizar para os adaptadores de teste mais recentes

Atualização para o adaptador de teste estável mais recente para aproveitar melhor a detecção e a execução de teste. Para saber mais sobre atualizações para adaptadores de teste MSTest, NUnit e xUnit, veja o [blog do Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2017/11/16/test-experience-improvements/).

### <a name="to-update-to-the-latest-stable-test-adapter-version"></a>Para atualizar para a versão estável mais recente do adaptador de teste

1. Abra o Gerenciador de Pacotes Nuget da solução navegando até **Ferramentas** > **Gerenciador de Pacotes NuGet** > **Gerenciar Pacotes NuGet da Solução**.

2. Clique na guia **Atualizações** e procurar os adaptadores de teste NUnit ou xUnit que estão instalados.

3. Selecione cada adaptador de teste e, em seguida, selecione a última versão estável no menu suspenso.

4. Escolha o botão **Instalar**.

   ![Atualizar adaptador de teste](media/install-adapter-upgrade.png)

## <a name="see-also"></a>Consulte também

- [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)
