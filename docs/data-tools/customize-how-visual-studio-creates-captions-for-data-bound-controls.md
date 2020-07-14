---
title: Personalizar legendas para controles vinculados a dados
ms.date: 11/03/2017
ms.topic: how-to
helpviewer_keywords:
- Label captions, Data Sources window
- smart captions
- captions, data-bound
- Data Sources Window, label captions
ms.assetid: 6d4d15f8-4d78-42fd-af64-779ae98d62c8
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 085542f912cc5747c2012adb05e6097b5891ed60
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282573"
---
# <a name="customize-how-visual-studio-creates-captions-for-data-bound-controls"></a>Personalizar como o Visual Studio cria legendas para controles associados a dados

Quando você arrasta itens da [janela fontes de dados](add-new-data-sources.md#data-sources-window) para um designer, uma consideração especial entra em cena: os nomes de coluna nos rótulos de legenda são reformatados em uma cadeia de caracteres mais legível quando duas ou mais palavras são encontradas para serem concatenadas juntas.

::: moniker range="vs-2017"

Você pode personalizar a maneira como esses rótulos são criados definindo os valores **SmartCaptionExpression**, **SmartCaptionReplacement**e **SmartCaptionSuffix** na chave de registro **HKEY_CURRENT_USER designers do \software\microsoft\visualstudio\15.0\data** .

::: moniker-end

::: moniker range=">=vs-2019"

Você pode personalizar a maneira como esses rótulos são criados definindo os valores **SmartCaptionExpression**, **SmartCaptionReplacement**e **SmartCaptionSuffix** na chave de registro **HKEY_CURRENT_USER designers do \software\microsoft\visualstudio\16.0\data** .

::: moniker-end

> [!NOTE]
> Essa chave do registro não existe até que você a crie.

A legenda inteligente é controlada pela expressão regular inserida no valor do valor **SmartCaptionExpression** . A adição da chave do registro dos **Data designers** substitui a expressão regular padrão que controla os rótulos de legenda. Para obter mais informações sobre expressões regulares, consulte [usando expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).

A tabela a seguir descreve os valores de registro que controlam os rótulos de legenda.

|Item do registro|Descrição|
|-------------------|-----------------|
|**SmartCaptionExpression**|A expressão regular que você usa para corresponder aos padrões.|
|**SmartCaptionReplacement**|O formato para exibir todos os grupos correspondentes na **SmartCaptionExpression**.|
|**SmartCaptionSuffix**|Uma cadeia de caracteres opcional a ser acrescentada ao final da legenda.|

A tabela a seguir lista as configurações padrão internas para esses valores de registro.

|Item do registro|Valor padrão|Explicação|
|-------------------|-------------------|-----------------|
|**SmartCaptionExpression**|**( \\ \p{ll}) ( \\ \p{Lu}) &#124;_ +**|Corresponde a um caractere minúsculo seguido por um caractere maiúsculo ou um sublinhado.|
|**SmartCaptionReplacement**|**$1 $2**|O **$1** representa os caracteres correspondentes nos primeiros parênteses da expressão, e o **$2** representa os caracteres correspondidos no segundo parênteses. A substituição é a primeira correspondência, um espaço e a segunda correspondência.|
|**SmartCaptionSuffix**|**:**|Representa um caractere acrescentado à cadeia de caracteres retornada. Por exemplo, se a legenda for `Company Name` , o sufixo a tornará`Company Name:`|

> [!CAUTION]
> Tenha cuidado ao fazer qualquer coisa no editor do registro. Faça backup do registro antes de editá-lo. Se você usar o editor do registro incorretamente, poderá causar sérios problemas que podem exigir a reinstalação do sistema operacional. A Microsoft não garante que os problemas que você causa usando o editor do registro incorretamente possam ser resolvidos. Use o Editor de Registro por sua conta e risco.
>
> Para obter informações sobre como fazer backup, editar e restaurar o registro, consulte [informações de registro do Windows para usuários avançados](https://support.microsoft.com/help/256986/windows-registry-information-for-advanced-users).

## <a name="modify-the-smart-captioning-behavior-of-the-data-sources-window"></a>Modificar o comportamento de legenda inteligente da janela fontes de dados

1. Abra uma janela de comando clicando em **Iniciar** e em **executar**.

2. Digite `regedit` na caixa de diálogo **executar** e clique em **OK**.

3. Expanda o nó **HKEY_CURRENT_USER**  >  **software**  >  **Microsoft**  >  **VisualStudio** .

::: moniker range="vs-2017"

4. Clique com o botão direito do mouse no nó **15,0** e crie uma nova **chave** chamada `Data Designers` .

::: moniker-end

::: moniker range=">=vs-2019"

4. Clique com o botão direito do mouse no nó **16,0** e crie uma nova **chave** chamada `Data Designers` .

::: moniker-end

5. Clique com o botão direito do mouse no nó **Data designers** e crie três novos valores de cadeia de caracteres:

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. Clique com o botão direito do mouse no valor de **SmartCaptionExpression** e selecione **Modificar**.

7. Insira a expressão regular que você deseja que a janela **fontes de dados** use.

8. Clique com o botão direito do mouse no valor **SmartCaptionReplacement** e selecione **Modificar**.

9. Insira a cadeia de caracteres de substituição formatada da maneira que você deseja exibir os padrões correspondentes em sua expressão regular.

10. Clique com o botão direito do mouse no valor **SmartCaptionSuffix** e selecione **Modificar**.

11. Insira os caracteres que você deseja que apareçam no final da legenda.

    Na próxima vez que você arrastar itens da janela **fontes de dados** , os rótulos de legenda serão criados usando os novos valores de registro fornecidos.

## <a name="turn-off-the-smart-captioning-feature"></a>Desativar o recurso de legenda inteligente

1. Abra uma janela de comando clicando em **Iniciar** e em **executar**.

2. Digite `regedit` na caixa de diálogo **executar** e clique em **OK**.

3. Expanda o nó **HKEY_CURRENT_USER**  >  **software**  >  **Microsoft**  >  **VisualStudio** .

::: moniker range="vs-2017"

4. Clique com o botão direito do mouse no nó **15,0** e crie uma nova **chave** chamada `Data Designers` .

::: moniker-end

::: moniker range=">=vs-2019"

4. Clique com o botão direito do mouse no nó **16,0** e crie uma nova **chave** chamada `Data Designers` .

::: moniker-end

5. Clique com o botão direito do mouse no nó **Data designers** e crie três novos valores de cadeia de caracteres:

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. Clique com o botão direito do mouse no item **SmartCaptionExpression** e selecione **Modificar**.

7. Insira `(.*)` para o valor. Isso corresponderá à cadeia de caracteres inteira.

8. Clique com o botão direito do mouse no item **SmartCaptionReplacement** e selecione **Modificar**.

9. Insira `$1` para o valor. Isso substitui a cadeia de caracteres pelo valor correspondente, que é a cadeia de caracteres inteira para que ela permaneça inalterada.

    Na próxima vez que você arrastar itens da janela **fontes de dados** , os rótulos de legenda serão criados com legendas não modificadas.

## <a name="see-also"></a>Veja também

- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
