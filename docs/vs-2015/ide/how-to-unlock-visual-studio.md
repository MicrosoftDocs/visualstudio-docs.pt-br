---
title: Desbloquear o Visual Studio 2015 | Microsoft Docs"
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: ffb580a1-8b5d-48f5-b811-87f8036f50ea
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: e7f78371faf472a390c0644bea790687bf12809e
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53065821"
---
# <a name="how-to-unlock-visual-studio"></a>Como desbloquear o Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode avaliar o Visual Studio gratuitamente por até 30 dias. Ao entrar no IDE, você pode estender o período de teste por 90 dias. Para continuar usando o Visual Studio, você pode desbloquear o IDE

1.  usando uma assinatura online.

2.  inserindo uma chave do produto (Product Key).

## <a name="to-unlock-visual-studio-using-an-online-subscription"></a>Para desbloquear o Visual Studio usando uma assinatura online
 Para desbloquear o Visual Studio usando uma assinatura online do MSDN ou do Visual Studio associada a uma conta da Microsoft ou uma conta corporativa ou de estudante:

1.  Clique no botão "Entrar" no canto superior direito do IDE (ou vá para Arquivo > Configurações de Conta para abrir a caixa de diálogo Configurações de Conta e clique no botão "Entrar".)

2.  Insira as credenciais para uma conta da Microsoft ou uma conta corporativa ou de estudante. O Visual Studio encontrará uma assinatura do MSDN ou uma assinatura do Visual Studio Team Services associada à sua conta.

> [!IMPORTANT]
>  O Visual Studio procura automaticamente assinaturas online associadas ao se conectar a uma conta do Visual Studio Team Services pela janela de ferramentas do Team Explorer. Quando você se conecta a uma conta do Visual Studio Team Services, pode entrar usando contas da Microsoft ou corporativas ou de estudante. Se houver uma assinatura online para aquela conta de usuário, o Visual Studio automaticamente desbloqueará o IDE para você.

## <a name="to-unlock-visual-studio-with-a-product-key"></a>Para desbloquear o Visual Studio com uma chave do produto (Product Key)

1.  Selecione **Arquivo > Configurações de Conta** para abrir a caixa de diálogo Configurações de Conta e clique no link "**Licenciar com uma Chave do Produto (Product Key)**".

2.  Insira a chave do produto (Product Key) no espaço fornecido.

> [!TIP]
>  Versões de pré-lançamento do Visual Studio não têm chaves do produto (Product Keys). Você deve entrar no IDE para usar versões de pré-lançamento.

## <a name="addressing-license-problem-states"></a>Endereçamento de estados de problema de licença

### <a name="updating-stale-licenses"></a>Atualizar licenças obsoletas
 Talvez você tenha visto a mensagem abaixo indicando que sua licença ficará obsoleta no Visual Studio.

 ![Caixa de diálogo de informações de usuário do Visual Studio](../ide/media/vs2013-userinfo.png "VS2013_UserInfo")

 Essa mensagem indica que embora sua assinatura ainda possa ser válida, o token de licença que o Visual Studio usa para manter sua assinatura atualizada ainda não foi atualizado e se tornou obsoleto devido a um dos motivos a seguir:

1. Você não usou o Visual Studio ou não teve uma conexão com a Internet por um longo período.

2. Você saiu do Visual Studio.

   Antes de o token de licença se tornar obsoleto, o Visual Studio mostrará primeiro uma mensagem de aviso solicitando que você insira suas credenciais novamente.

   Se você não inserir suas credenciais novamente, o token começará a se tornar obsoleto. Quando isso acontece, a caixa de diálogo Configurações de Conta informa os dias restantes antes de seu token expirar completamente. Depois que o token expirar, você precisará inserir novamente suas credenciais para esta conta ou licença com outro método acima para poder continuar usando o Visual Studio.

> [!IMPORTANT]
>  Se estiver usando o Visual Studio por longos períodos em ambientes com acesso limitado ou sem acesso à Internet, você deverá usar uma chave do produto (Product Key) para desbloquear o Visual Studio para evitar a interrupção.

### <a name="updating-expired-licenses"></a>Atualizar licenças expiradas
 Se sua assinatura tiver expirado completamente e você não tiver mais direitos de acesso ao Visual Studio, você precisará:

1.  Renovar sua assinatura. Para obter mais informações sobre a licença que você está usando, acesse a caixa de diálogo Arquivo > Configurações de Conta e procure as informações de licença no lado direito da caixa de diálogo.

2.  Se você tiver outra assinatura associada a uma conta diferente, adicione essa conta à lista Todas as Contas no lado esquerdo da caixa de diálogo Arquivo > Configurações de Conta clicando no link “Adicionar uma conta...” .

## <a name="see-also"></a>Consulte também
 [Signing in to Visual Studio](../ide/signing-in-to-visual-studio.md) (Entrando no Visual Studio)
