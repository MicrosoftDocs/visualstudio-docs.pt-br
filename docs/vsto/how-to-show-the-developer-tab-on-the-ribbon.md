---
title: 'Como: Mostrar a guia Desenvolvedor na faixa de opções'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- Developer tab [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: edcbcb969e45403d9ca138b259073e3cf4d73be0
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349618"
---
# <a name="how-to-show-the-developer-tab-on-the-ribbon"></a>Como: Mostrar a guia Desenvolvedor na faixa de opções
  Para acessar o **desenvolvedor** guia na faixa de opções de um aplicativo do Office, você deve configurá-lo para mostrar essa guia porque ela não aparece por padrão. Por exemplo, você deve mostrar essa guia se você deseja adicionar um <xref:Microsoft.Office.Tools.Word.GroupContentControl> para uma personalização no nível de documento para Word.  
  
> [!NOTE]  
>  Essa orientação se aplica ao Office 2010 ou posterior apenas a aplicativos. Se você desejar mostrar essa guia no 2007 Microsoft Office System, consulte a seguinte versão deste tópico [como: Mostrar a guia Desenvolvedor na faixa de opções](https://web.archive.org/web/20140303033431/msdn.microsoft.com/library/bb608625(v=vs.90).aspx
).  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
> [!NOTE]  
>  Acesso não tem um **desenvolvedor** guia.  
  
## <a name="to-show-the-developer-tab"></a>Para mostrar a guia do desenvolvedor  
  
1.  Inicie qualquer um dos aplicativos do Office suportados por este tópico. Consulte a **aplica-se a:** Observação no início deste tópico.  
  
2.  Sobre o **arquivo** guia, escolha o **opções** botão.  
  
     A figura a seguir mostra a **arquivo** guia e **opções** botão no Office 2010.  
  
     ![Escolher o arquivo, as opções no Outlook 2010](../vsto/media/vsto-office-file-tab.png "escolhendo o arquivo, as opções no Outlook 2010")  
  
     A figura a seguir mostra a **arquivo** guia no Office 2013.  
  
     ![A guia arquivo no Outlook 2013](../vsto/media/vsto-office2013-filetab.png "guia o arquivo no Outlook 2013")  
  
     A figura a seguir mostra a **opções** botão do Office 2013.  
  
     ![O botão Opções no Outlook 2013 Preview](../vsto/media/vsto-office2013-optionsbutton.png "botão as opções no Outlook 2013 Preview")  
  
3.  No _ApplicationName_**opções** caixa de diálogo, escolha o **personalizar faixa de opções** botão.  
  
     A figura a seguir mostra a **opções** caixa de diálogo e o **personalizar faixa de opções** botão no Excel 2010. O local deste botão é semelhante em todos os outros aplicativos listados na seção "Aplica-se a" próximo à parte superior deste tópico.  
  
     ![O botão Personalizar fita](../vsto/media/vsto-office2010-customizeribbonbutton.png "botão a personalizar faixa de opções")  
  
4.  Na lista de guias principais, selecione a **desenvolvedor** caixa de seleção.  
  
     A figura a seguir mostra a **Developer** caixa de seleção no Word 2010 e [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)]. O local desta caixa de seleção é semelhante em todos os outros aplicativos listados na seção "Aplica-se a" próximo à parte superior deste tópico.  
  
     ![A caixa de seleção na caixa de diálogo Opções do Word Developer](../vsto/media/vsto-office2010-developercheckbox.png "desenvolvedor a caixa de seleção na caixa de diálogo Opções do Word")  
  
5.  Escolha o **Okey** botão para fechar o **opções** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)  
  
  