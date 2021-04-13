---
title: Estender uma versão de avaliação ou atualizar uma licença
description: Saiba como estender uma avaliação gratuita do Visual Studio, usar uma assinatura online ou uma chave do produto (Product Key) para desbloquear o Visual Studio e atualizar uma licença obsoleta ou expirada.
ms.date: 12/18/2019
ms.topic: conceptual
ms.assetid: ffb580a1-8b5d-48f5-b811-87f8036f50ea
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: b78db14b149b094550ce025ab3750742401fddbe
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107295462"
---
# <a name="extend-a-trial-version-or-update-a-license"></a>Estender uma versão de avaliação ou atualizar uma licença

Você pode avaliar uma avaliação gratuita de [Visual Studio Professional ou Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/compare/) por 30 dias. E, se você entrar, poderá estender o período de avaliação para 90 dias. (A Comunidade do Visual Studio é gratuita sem um período de avaliação. No entanto, você deve [entrar](signing-in-to-visual-studio.md) periodicamente para manter sua [licença atualizada](#update-a-stale-license).)

Para continuar usando o Visual Studio após o término de um período de avaliação, desbloqueie-o com uma [assinatura online](#use-an-online-subscription) ou uma [chave do produto (Product Key](#enter-a-product-key)).

## <a name="use-an-online-subscription"></a>Usar uma assinatura online

1. Escolha o botão **entrar** no canto superior direito do IDE (ou vá para **arquivo**  >  **configurações de conta** para abrir a caixa de diálogo **configurações de conta** e, em seguida, escolha o botão **entrar** ).

1. Insira as credenciais para uma conta da Microsoft ou uma conta corporativa ou de estudante. O Visual Studio encontrará uma Assinatura do Visual Studio ou uma organização do Azure DevOps associada à sua conta.

> [!IMPORTANT]
> O Visual Studio procura automaticamente assinaturas online associadas quando você se conecta a uma organização do Azure DevOps na janela de ferramentas do **Team Explorer**. Quando se conecta a uma organização do Azure DevOps, você pode entrar usando contas da Microsoft e corporativas ou de estudante. Se houver uma assinatura online para aquela conta de usuário, o Visual Studio automaticamente desbloqueará o IDE para você.

Para obter mais informações sobre as assinaturas do Visual Studio e como elas funcionam, consulte a página de [perguntas frequentes de suporte a assinaturas](https://visualstudio.microsoft.com/subscriptions/support/) .

## <a name="enter-a-product-key"></a>Inserir uma chave do produto

1. Selecione   >  **configurações de conta** de arquivo para abrir a caixa de diálogo **configurações de conta** e escolha a **licença com um link de chave do produto (Product Key** ).

1. Insira a chave do produto (Product Key) no espaço fornecido.

> [!TIP]
> As versões de pré-lançamento do Visual Studio não têm chaves de produto. Você deve entrar no IDE para usar as versões de pré-lançamento.

Para obter mais informações sobre as chaves de produto do Visual Studio para o Visual Studio e como obtê-las, consulte a página [usando as chaves do produto no Visual Studio subscriptions](/visualstudio/subscriptions/product-keys) .

## <a name="update-a-stale-license"></a>Atualizar uma licença obsoleta

Você pode ver uma mensagem no Visual Studio que diz "sua licença ficou obsoleta e deve ser atualizada".

![Mensagem de licença obsoleta do Visual Studio](../ide/media/vs2017_stale-license.png)

Essa mensagem indica que, embora sua assinatura ainda possa ser válida, o token de licença que o Visual Studio usa para manter sua assinatura atualizado ainda não foi atualizado. O Visual Studio relata que a licença está obsoleta devido a um dos seguintes motivos:

* Você não usou o Visual Studio ou não se conectou à Internet por um longo período de tempo.
* Você saiu do Visual Studio.

Antes de o token de licença ficar obsoleto, o Visual Studio mostrará primeiro uma mensagem de aviso que solicita que você insira suas credenciais novamente.

Se você não inserir novamente suas credenciais, o token começará a ficar obsoleto e a caixa de diálogo **configurações de conta** informará quantos dias você deixou antes que o token expire. Depois que o token expirar, será preciso digitar novamente suas credenciais de conta para continuar usando o Visual Studio.

> [!Important]
> Se estiver usando o Visual Studio por longos períodos em ambientes com acesso limitado ou sem acesso à Internet, você deverá usar uma chave do produto (Product Key) para desbloquear o Visual Studio a fim de evitar uma interrupção.

## <a name="update-an-expired-license"></a>Atualizar uma licença expirada

Se sua assinatura tiver expirado e você não tiver mais direitos de acesso ao Visual Studio, você deverá renovar sua assinatura ou adicionar outra conta que tenha uma assinatura. Para ver mais informações sobre a licença que você está usando, acesse **arquivo**  >  **configurações de conta** e examine as informações de licença no lado direito da caixa de diálogo. Se você tiver outra assinatura associada a uma conta diferente, adicione essa conta à lista **todas as contas** no lado esquerdo da caixa de diálogo selecionando o link **Adicionar uma conta** .

## <a name="get-support"></a>Obter suporte

Às vezes, as coisas dão errado. Se você tiver um problema, aqui estão algumas opções de suporte:

* Relate problemas do produto usando o [relatório uma ferramenta problemática](how-to-report-a-problem-with-visual-studio.md) .
* Encontre respostas para perguntas sobre assinaturas, contas e cobrança nas [perguntas frequentes de suporte às assinaturas](https://visualstudio.microsoft.com/subscriptions/support/).

## <a name="see-also"></a>Confira também

* [Entrar no Visual Studio](../ide/signing-in-to-visual-studio.md)
* [Compare as edições do Visual Studio](https://visualstudio.microsoft.com/vs/compare/)
* [Saiba mais sobre as assinaturas do Visual Studio](/visualstudio/subscriptions/)
