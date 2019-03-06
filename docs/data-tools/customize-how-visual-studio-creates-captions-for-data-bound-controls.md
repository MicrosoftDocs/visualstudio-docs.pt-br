---
title: Personalizar legendas para controles ligados a dados
ms.date: 11/03/2017
ms.topic: conceptual
helpviewer_keywords:
- Label captions, Data Sources window
- smart captions
- captions, data-bound
- Data Sources Window, label captions
ms.assetid: 6d4d15f8-4d78-42fd-af64-779ae98d62c8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 1745aef29da9fc8efd49789f0112c903128f6f74
ms.sourcegitcommit: 11337745c1aaef450fd33e150664656d45fe5bc5
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 03/04/2019
ms.locfileid: "57323687"
---
# <a name="customize-how-visual-studio-creates-captions-for-data-bound-controls"></a>Personalizar como o Visual Studio cria legendas para controles associados a dados

Quando você arrasta itens dos [janela fontes de dados](add-new-data-sources.md#data-sources-window) para um designer, uma consideração especial entra em ação: os nomes de coluna nos rótulos de legenda são reformatados para uma cadeia de caracteres mais legível quando duas ou mais palavras são encontradas concatenados.

::: moniker range="vs-2017"

Você pode personalizar a maneira na qual esses rótulos são criados definindo a **SmartCaptionExpression**, **SmartCaptionReplacement**, e **SmartCaptionSuffix** valores em o **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Data Designers** chave do registro.

::: moniker-end

::: moniker range=">=vs-2019"

Você pode personalizar a maneira na qual esses rótulos são criados definindo a **SmartCaptionExpression**, **SmartCaptionReplacement**, e **SmartCaptionSuffix** valores em o **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Data Designers** chave do registro.

::: moniker-end

> [!NOTE]
> Essa chave do registro não existe até que você criá-lo.

Títulos inteligentes são controlados pela expressão regular inserida no valor da **SmartCaptionExpression** valor. Adicionando o **Designers de dados** chave do Registro substitui a expressão regular padrão que controla os rótulos de legenda. Para obter mais informações sobre expressões regulares, consulte [usando expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).

A tabela a seguir descreve os valores do registro que controlam os rótulos de legenda.

|Item do registro|Descrição|
|-------------------|-----------------|
|**SmartCaptionExpression**|A expressão regular, que você pode usar para corresponder aos seus padrões.|
|**SmartCaptionReplacement**|O formato para exibir quaisquer grupos correspondidos na **SmartCaptionExpression**.|
|**SmartCaptionSuffix**|Uma cadeia de caracteres opcional para acrescentar ao final da legenda.|

A tabela a seguir lista as configurações padrão interno para esses valores do registro.

|Item do registro|Valor padrão|Explicação|
|-------------------|-------------------|-----------------|
|**SmartCaptionExpression**|**(\\\p{Ll})(\\\p{Lu})&#124;_+**|Corresponde a um caractere minúsculo seguido por um caractere maiusculo ou um sublinhado.|
|**SmartCaptionReplacement**|**USD 1, USD 2**|O **US $1** representa quaisquer caracteres correspondidos no primeiro parênteses da expressão e o **US $2** representa quaisquer caracteres correspondidos no segundo parênteses. A substituição é a primeira correspondência, um espaço e, em seguida, a segunda correspondência.|
|**SmartCaptionSuffix**|**:**|Representa um caractere acrescentado à cadeia de caracteres retornada. Por exemplo, se a legenda for `Company Name`, o sufixo torna `Company Name:`|

> [!CAUTION]
> Tenha muito cuidado ao fazer qualquer coisa no Editor do registro. Faça backup do registro antes de editá-lo. Se você usar o Editor do Registro incorretamente, você pode causar sérios problemas que talvez exijam a reinstalação do sistema operacional. A Microsoft não garante que os problemas que causam usando o Editor do Registro incorretamente podem ser resolvidos. Use o Editor do Registro por sua conta e risco.
>
> Para obter informações sobre como fazer backup, edição e a restauração do registro, consulte [informações de registro do Windows para usuários avançados](https://support.microsoft.com/help/256986/windows-registry-information-for-advanced-users).

## <a name="modify-the-smart-captioning-behavior-of-the-data-sources-window"></a>Modificar o comportamento de Legendagem oculta inteligente da janela fontes de dados

1. Abra uma janela de comando clicando **inicie** e, em seguida **executar**.

2. Tipo de `regedit` no **execute** caixa de diálogo e clique em **Okey**.

3. Expanda o **HKEY_CURRENT_USER** > **Software** > **Microsoft** > **VisualStudio**nó.

::: moniker range="vs-2017"

4. Clique com botão direito do **15.0** nó e crie um novo **chave** chamado `Data Designers`.

::: moniker-end

::: moniker range=">=vs-2019"

4. Clique com botão direito do **16.0** nó e crie um novo **chave** chamado `Data Designers`.

::: moniker-end

5. Clique com botão direito do **Designers de dados** nó e criar três novos valores de cadeia de caracteres:

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. Clique com botão direito do **SmartCaptionExpression** valor e, em seguida, selecione **modificar**.

7. Insira a expressão regular que você deseja que o **fontes de dados** janela a ser usado.

8. Clique com botão direito do **SmartCaptionReplacement** valor e, em seguida, selecione **modificar**.

9. Insira a substituição de cadeia de caracteres formatada da maneira que você deseja exibir os padrões de correspondência em sua expressão regular.

10. Clique com botão direito do **SmartCaptionSuffix** valor e, em seguida, selecione **modificar**.

11. Insira qualquer caractere que você deseja que apareça no final da legenda.

    Na próxima vez que você arrasta itens dos **fontes de dados** janela, os rótulos de legenda são criados usando os novos valores de registro fornecidos.

## <a name="turn-off-the-smart-captioning-feature"></a>Desativar o recurso de Legendagem oculta inteligente

1. Abra uma janela de comando clicando **inicie** e, em seguida **executar**.

2. Tipo de `regedit` no **execute** caixa de diálogo e clique em **Okey**.

3. Expanda o **HKEY_CURRENT_USER** > **Software** > **Microsoft** > **VisualStudio**nó.

::: moniker range="vs-2017"

4. Clique com botão direito do **15.0** nó e crie um novo **chave** chamado `Data Designers`.

::: moniker-end

::: moniker range=">=vs-2019"

4. Clique com botão direito do **16.0** nó e crie um novo **chave** chamado `Data Designers`.

::: moniker-end

5. Clique com botão direito do **Designers de dados** nó e criar três novos valores de cadeia de caracteres:

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. Clique com botão direito do **SmartCaptionExpression** item e, em seguida, selecione **modificar**.

7. Insira `(.*)` para o valor. Isso corresponderá à cadeia de caracteres inteira.

8. Clique com botão direito do **SmartCaptionReplacement** item e, em seguida, selecione **modificar**.

9. Insira `$1` para o valor. Isso substitui a cadeia de caracteres com o valor correspondente, que é a cadeia de caracteres inteira para que ela permanecerá inalterada.

    Na próxima vez que você arrasta itens dos **fontes de dados** janela, os rótulos de legenda são criados com legendas não modificadas.

## <a name="see-also"></a>Consulte também

- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)