---
title: Personalizar como o Visual Studio cria legendas para controles ligados a dados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- Label captions, Data Sources window
- smart captions
- captions, data-bound
- Data Sources Window, label captions
ms.assetid: 6d4d15f8-4d78-42fd-af64-779ae98d62c8
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b6906e68c74bbb718f9bfc041ab35075b3f9b0aa
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220169"
---
# <a name="customize-how-visual-studio-creates-captions-for-data-bound-controls"></a>Personalizar como o Visual Studio cria legendas para controles associados a dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Quando você arrasta itens dos [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) para o Designer de formulários do Windows, uma consideração especial entra em ação: os nomes de coluna nos rótulos de legenda são reformatados para uma cadeia de caracteres mais legível quando duas ou mais palavras são encontrado para ser concatenados. Você pode personalizar a maneira na qual esses rótulos são criados, definindo o **SmartCaptionExpression**, **SmartCaptionReplacement**, e **SmartCaptionSuffix** valores em o **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Data Designers** chave do registro.  
  
> [!NOTE]
>  Essa chave do registro não existe até que você criá-lo.  
  
 Títulos inteligentes são controlados pela expressão regular inserida no valor da **SmartCaptionExpression** valor. Adicionando o **Designers de dados** chave do Registro substitui a expressão regular padrão que controla os rótulos de legenda. Para obter mais informações sobre expressões regulares, consulte [usando expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).  
  
 A tabela a seguir descreve os valores do registro que controlam os rótulos de legenda.  
  
|Item do registro|Descrição|  
|-------------------|-----------------|  
|**SmartCaptionExpression**|A expressão regular usada para corresponder aos seus padrões.|  
|**SmartCaptionReplacement**|O formato para exibir quaisquer grupos correspondidos na **SmartCaptionExpression**.|  
|**SmartCaptionSuffix**|Uma cadeia de caracteres opcional para acrescentar ao final da legenda.|  
  
 A tabela a seguir lista as configurações padrão interno para esses valores do registro.  
  
|Item do registro|Valor padrão|Explicação|  
|-------------------|-------------------|-----------------|  
|**SmartCaptionExpression**|(\\\p{Ll}) (\\\p{Lu})&#124;_ +|Corresponde a um caractere minúsculo seguido por um caractere maiusculo ou um sublinhado.|  
|**SmartCaptionReplacement**|$1 $2|$1 representa quaisquer caracteres correspondidos no primeiro parênteses da expressão e US $2 representa quaisquer caracteres correspondidos no segundo parênteses. A substituição é a primeira correspondência, um espaço e, em seguida, a segunda correspondência.|  
|**SmartCaptionSuffix**|:|Representa um caractere acrescentado à cadeia de caracteres retornada. Por exemplo, se a legenda for `Company Name`, o sufixo torna `Company Name:`|  
  
> [!CAUTION]
>  Você deve ser muito cuidado ao fazer qualquer coisa no Editor do registro. Faça backup do registro antes de editá-lo. Se você usar o Editor do Registro incorretamente, você pode causar sérios problemas que talvez exijam a reinstalação do sistema operacional. A Microsoft não garante que os problemas que causam usando o Editor do Registro incorretamente podem ser resolvidos. Use o Editor do Registro por sua conta e risco.  
>   
>  O seguinte artigo da Base de conhecimento contém instruções para fazer backup, edição e a restauração do registro: [descrição do registro do Microsoft Windows](http://support.microsoft.com/default.aspx?scid=kb;en-us;256986) (http://support.microsoft.com/default.aspx?scid=kb; en-us; 256986)  
  
### <a name="to-modify-the-smart-captioning-behavior-of-the-data-sources-window"></a>Para modificar o comportamento de Legendagem oculta inteligente da janela fontes de dados  
  
1.  Abra uma janela de comando clicando **inicie** e, em seguida **executar**.  
  
2.  Tipo de `regedit` no **execute** caixa de diálogo e clique em **Okey**.  
  
3.  Expanda o **HKEY_CURRENT_USER** nó.  
  
4.  Expanda o **Software** nó.  
  
5.  Expanda o **Microsoft** nó.  
  
6.  Expanda o **VisualStudio** nó.  
  
7.  Clique com botão direito do **10.0** nó e crie um novo **chave** chamado `Data Designers`.  
  
8.  Com o botão direito do **Designers de dados** nó e crie um novo **valor de cadeia de caracteres** chamado `SmartCaptionExpression`.  
  
9. Com o botão direito do **Designers de dados** nó e crie um novo **valor de cadeia de caracteres** chamado `SmartCaptionReplacement`.  
  
10. Com o botão direito do **Designers de dados** nó e crie um novo **valor de cadeia de caracteres** chamado `SmartCaptionSuffix`.  
  
11. Clique com botão direito do **SmartCaptionExpression** item e, em seguida, selecione **modificar**.  
  
12. Insira a expressão regular que você deseja que o **fontes de dados** janela a ser usado.  
  
13. Clique com botão direito do **SmartCaptionReplacement** item e, em seguida, selecione **modificar**.  
  
14. Insira a substituição de cadeia de caracteres formatada da maneira que você deseja exibir os padrões de correspondência em sua expressão regular.  
  
15. Clique com botão direito do **SmartCaptionSuffix** item e, em seguida, selecione **modificar**.  
  
16. Insira qualquer caractere que você deseja que apareça no final da legenda.  
  
     Na próxima vez que você arrasta itens dos **fontes de dados** janela, os rótulos de legenda são criados usando os novos valores de registro fornecidos.  
  
### <a name="to-turn-off-the-smart-captioning-feature"></a>Para desativar o recurso de Legendagem oculta inteligente  
  
1.  Abra uma janela de comando clicando **inicie** e, em seguida **executar**.  
  
2.  Tipo de `regedit` no **execute** caixa de diálogo e clique em **Okey**.  
  
3.  Expanda o **HKEY_CURRENT_USER** nó.  
  
4.  Expanda o **Software** nó.  
  
5.  Expanda o **Microsoft** nó.  
  
6.  Expanda o **VisualStudio** nó.  
  
7.  Clique com botão direito do **10.0** nó e crie um novo **chave** chamado `Data Designers`.  
  
8.  Com o botão direito do **Designers de dados** nó e crie um novo **valor de cadeia de caracteres** chamado `SmartCaptionExpression`.  
  
9. Com o botão direito do **Designers de dados** nó e crie um novo **valor de cadeia de caracteres** chamado `SmartCaptionReplacement`.  
  
10. Com o botão direito do **Designers de dados** nó e crie um novo **valor de cadeia de caracteres** chamado `SmartCaptionSuffix`.  
  
11. Clique com botão direito do **SmartCaptionExpression** item e, em seguida, selecione **modificar**.  
  
12. Insira `(.*)` para o valor. Isso corresponderá à cadeia de caracteres inteira.  
  
13. Clique com botão direito do **SmartCaptionReplacement** item e, em seguida, selecione **modificar**.  
  
14. Insira `$1` para o valor. Isso substitui a cadeia de caracteres com o valor correspondente, que é a cadeia de caracteres inteira para que ela permanecerá inalterada.  
  
     Na próxima vez que você arrasta itens dos **fontes de dados** janela, os rótulos de legenda são criados com legendas não modificadas.  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)

