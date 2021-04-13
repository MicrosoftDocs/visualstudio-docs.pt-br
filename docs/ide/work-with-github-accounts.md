---
title: Trabalhar com contas do GitHub no Visual Studio
ms.date: 11/16/2020
ms.custom: ''
ms.topic: conceptual
description: Saiba como usar o Visual Studio com contas do GitHub.
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 9f55a233cc2550cd452851edc9092b4b2f4f2411
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296359"
---
# <a name="work-with-github-accounts-in-visual-studio"></a>Trabalhar com contas do GitHub no Visual Studio

Se você tiver uma conta pública do GitHub ou do GitHub, poderá adicioná-la ao seu conjunto de chaves do Visual Studio. Depois de adicionar sua conta, você poderá aproveitar a integração da plataforma acessando e criando repositórios do GitHub, diretamente do Visual Studio.

## <a name="adding-public-github-accounts"></a>Adicionando contas públicas do GitHub

Você pode adicionar sua conta do GitHub público se já tiver entrado no Visual Studio com um conta Microsoft ou uma conta corporativa ou de estudante.

1. Selecione o ícone com suas iniciais no canto superior direito do ambiente do Visual Studio. Em seguida, selecione **configurações de conta...** para gerenciar suas contas. Você também pode abrir a caixa de diálogo Configurações de conta acessando **arquivo**  >  **configurações de conta**.

    :::image type="content" source="../ide/media/account-picker.png" alt-text="Configurações de conta":::

2. No submenu **todas as contas** , selecione o sinal de adição para adicionar uma conta e selecione **GitHub**.

    :::image type="content" source="../ide/media/sign-in-add-github.png" alt-text="Selecione Adicionar conta do GitHub":::

3. Você será redirecionado para o navegador, no qual você pode entrar com suas credenciais do GitHub. Depois de entrar, você obterá uma janela de êxito no navegador e poderá retornar ao Visual Studio.

    :::image type="content" source="../ide/media/github-success-signin.png" alt-text="Janela de êxito no navegador":::

4. Você terá ambas as contas presentes no submenu **todas as contas** .

    :::image type="content" source="../ide/media/show-both-accounts.png" alt-text="Ambas as contas que mostram":::

Se você ainda não tiver entrado no Visual Studio com uma conta diferente, selecione o link **entrar** no canto superior direito do ambiente do Visual Studio. Você também pode abrir a caixa de diálogo Configurações de conta acessando **arquivo**  >  **configurações de conta**. Em seguida, siga as instruções acima para adicionar sua conta do GitHub.

![Usuário não conectado](../ide/media/vs2019_usernotsignedin.png)

## <a name="adding-github-enterprise-accounts"></a>Adicionando contas corporativas do GitHub

Por padrão, o Visual Studio tem apenas contas públicas do GitHub habilitadas.

1. Para habilitar as contas do GitHub Enterprise, vá para **ferramentas**  >  **Opções** e procure as opções de **contas** .

    :::image type="content" source="../ide/media/accounts-options.png" alt-text="Menu de opções de contas":::

2. Em seguida, marque a caixa para **incluir contas do GitHub Enterprise Server**. Na próxima vez em que você acessar **as configurações de conta** e tentar adicionar uma conta do GitHub, você verá opções para o GitHub e o GitHub Enterprise.

    :::image type="content" source="../ide/media/github-enterprise-endpoint-signin.png" alt-text="Entrar com o GitHub Enterprise":::

3. Depois de inserir o endereço do GitHub Enterprise Server, selecione **entrar com seu navegador**. Lá, você pode entrar usando suas credenciais de empresa do GitHub.

## <a name="see-also"></a>Confira também

- [Trabalhar com várias contas de usuário](work-with-multiple-user-accounts.md)
- [Entrar no Visual Studio](signing-in-to-visual-studio.md)
