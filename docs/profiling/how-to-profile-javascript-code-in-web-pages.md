---
title: Como criar o perfil de código JavaScript em páginas da Web | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- JavaScript performance profiling
- Profiling Tools,JavaScript
- web site performance profiling
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 9c0af520502a0d6bb67d17786ab18fba920fcbbb
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328887"
---
# <a name="how-to-profile-javascript-code-in-web-pages"></a>Como criar perfil de código JavaScript em páginas da Web

As Ferramentas de Criação de Perfil do Visual Studio podem coletar dados de desempenho do código JavaScript que é executado em um aplicativo Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], em uma página da Web arbitrária ou em um aplicativo JavaScript usando o método de criação de perfil por instrumentação. Exige o Internet Explorer 8 ou posterior.

> [!WARNING]
> Para analisar JavaScript em aplicativos UWP, consulte [Memória de JavaScript](../profiling/javascript-memory.md)

Você pode usar o Assistente de Criação de Perfil para criar uma sessão de desempenho. Especifique o método de instrumentação e, em seguida, especifique a opção de criação de perfil JavaScript na página de Instrumentação da caixa de diálogo de propriedades da sessão de desempenho.

Ao especificar criação de perfil JavaScript, o código JavaScript que é executado no navegador e o código do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] que é executado no servidor serão analisados.

- Para um aplicativo Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], é criado um perfil do código JavaScript que é executado no navegador e do código do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] que é executado no servidor.

- Para uma página da Web arbitrária, é criado o perfil do código JavaScript que é executado no navegador.

## <a name="to-profile-javascript-in-an-aspnet-web-application-project"></a>Para criar perfil do JavaScript em um projeto de aplicativo Web ASP.NET

1. Abra o projeto Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] no Visual Studio.

2. No menu **Analisar**, clique em **Iniciar o Assistente de Desempenho**.

3. Na primeira página do Assistente de Desempenho, especifique o método de criação de perfil **Instrumentação** e, em seguida, clique em **Avançar**.

4. Na segunda página do assistente, verifique se o projeto atual está selecionado na lista de destinos e, em seguida, clique em **Avançar.**

5. Na terceira página do assistente, selecione a caixa de seleção **Perfil JavaScript** e, em seguida, clique em **Avançar**.

6. Na quarta página do assistente, clique em **Concluir** para iniciar o aplicativo Web no navegador.

7. Execute a funcionalidade que você deseja analisar.

8. Para encerrar a sessão de criação de perfil, feche o navegador.

### <a name="to-profile-javascript-in-individual-web-pages-or-a-javascript-applications"></a>Para criar o perfil do JavaScript em páginas da Web ou em aplicativos JavaScript individuais

1. Abra o Visual Studio.

2. No menu **Analisar**, clique em **Iniciar o Assistente de Desempenho**.

3. Na primeira página do Assistente de Desempenho, especifique o método de criação de perfil **Instrumentação** e, em seguida, clique em **Avançar**.

4. Na segunda página do assistente, clique em um aplicativo ASP.NET ou JavaScript e, em seguida, clique em **Avançar.**

5. Na terceira página do assistente:

    1. Digite a URL da página na caixa **Qual URL ou caminho executará seu aplicativo**.

    2. Selecione a caixa de seleção **Perfil JavaScript** e, em seguida, clique em **Avançar**.

6. Na quarta página do assistente, clique em **Concluir** para iniciar a página da Web no navegador.

7. Execute a funcionalidade que você deseja analisar.

8. Para encerrar a sessão de criação de perfil, feche o navegador.
