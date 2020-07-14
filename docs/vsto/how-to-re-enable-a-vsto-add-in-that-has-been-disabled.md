---
title: 'Como: reabilitar um suplemento do VSTO que foi desabilitado'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VST.Warning.DisabledAddIn
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disabled add-ins
- add-ins [Office development in Visual Studio], disabled
- add-ins [Office development in Visual Studio], enabling
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3575e119f4da3ca3050a28243104fb4773089cf3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541252"
---
# <a name="how-to-re-enable-a-vsto-add-in-that-has-been-disabled"></a>Como: reabilitar um suplemento do VSTO que foi desabilitado
  Microsoft Office aplicativos podem desabilitar os suplementos do VSTO que se comportam inesperadamente. Se um aplicativo não carregar seu suplemento do VSTO quando você tentar depurá-lo, o aplicativo poderá ter o disco rígido desabilitado ou desabilitado por software do seu suplemento do VSTO.

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="hard-disabled-vsto-add-ins"></a>Suplementos do VSTO desabilitados com hardware
 A desabilitação forçada pode ocorrer quando um suplemento do VSTO faz com que o aplicativo seja fechado inesperadamente. Ele também pode ocorrer em seu computador de desenvolvimento se você parar o depurador enquanto o <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos em seu suplemento do VSTO estiver em execução.

### <a name="to-re-enable-a-vsto-add-in"></a>Para reabilitar um suplemento do VSTO

1. No aplicativo, clique na guia **arquivo** .

2. Clique no botão **Opções** de *ApplicationName* .

3. No painel categorias, clique em **suplementos**.

4. No painel de detalhes, verifique se o suplemento do VSTO é exibido na lista de **suplementos do aplicativo desabilitados** .

     A coluna **nome** especifica o nome do assembly e a coluna **local** especifica o caminho completo do manifesto do aplicativo.

5. Na caixa **gerenciar** , clique em **itens desabilitados**e, em seguida, clique em **ir**.

6. Selecione o suplemento do VSTO e clique em **habilitar**.

7. Clique em **fechar**

## <a name="soft-disabled-vsto-add-ins"></a>Suplementos do VSTO desabilitados por software
 A desabilitação flexível pode ocorrer quando um suplemento do VSTO produz um erro que não faz com que o aplicativo feche inesperadamente. Por exemplo, um aplicativo pode desabilitar um suplemento do VSTO de maneira flexível se ele lançar uma exceção sem tratamento enquanto o <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos estiver em execução.

> [!NOTE]
> Quando você reabilita um suplemento do VSTO desabilitado por software, o aplicativo tenta imediatamente carregar o suplemento do VSTO. Se o problema que inicialmente fez com que o aplicativo desabilite o suplemento do VSTO não tiver sido corrigido, o aplicativo desativará o suplemento do VSTO de forma flexível novamente.

### <a name="to-re-enable-a-vsto-add-in"></a>Para reabilitar um suplemento do VSTO

1. No aplicativo, clique na guia **arquivo** .

2. Clique no botão **Opções** de *ApplicationName* .

3. No painel categorias, clique em **suplementos**.

4. No painel de detalhes, verifique se o suplemento do VSTO aparece na lista de **suplementos de aplicativos inativos** .

     A coluna **nome** especifica o nome do assembly e a coluna **local** especifica o caminho completo do manifesto do aplicativo.

5. Na caixa **gerenciar** , clique em **suplementos de com**e, em seguida, clique em **ir**.

6. Na caixa de diálogo **suplementos de com** , marque a caixa de seleção ao lado do suplemento do VSTO desabilitado.

7. Clique em **OK**.

## <a name="see-also"></a>Consulte também
- [Criar soluções do Office](../vsto/building-office-solutions.md)
- [Depurar projetos do Office](../vsto/debugging-office-projects.md)
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
