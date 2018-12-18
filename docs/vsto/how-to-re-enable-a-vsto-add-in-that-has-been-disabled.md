---
title: 'Como: habilitar novamente um suplemento VSTO que tenha sido desabilitado'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VST.Warning.DisabledAddIn
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disabled add-ins
- add-ins [Office development in Visual Studio], disabled
- add-ins [Office development in Visual Studio], enabling
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c81e44b548f4d1139810780731741a489e624047
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670189"
---
# <a name="how-to-re-enable-a-vsto-add-in-that-has-been-disabled"></a>Como: habilitar novamente um suplemento VSTO que tenha sido desabilitado
  Aplicativos do Microsoft Office podem desabilitar suplementos do VSTO que tenha um comportamento inesperado. Se um aplicativo não carrega o suplemento do VSTO quando você tenta depurá-lo, o aplicativo pode ter desabilitado rígido ou flexível desabilitado o suplemento do VSTO.  
  
 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]  
  
## <a name="hard-disabled-vsto-add-ins"></a>Suplementos do VSTO do disco rígido desabilitado  
 Desabilitando duro pode ocorrer quando um suplemento do VSTO faz com que o aplicativo seja encerrado inesperadamente. Também podem ocorrer no computador de desenvolvimento se você parar o depurador enquanto o <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos no seu suplemento do VSTO está em execução.  
  
### <a name="to-re-enable-a-vsto-add-in"></a>Para reabilitar um suplemento do VSTO  
  
1.  No aplicativo, clique no **arquivo** guia.  
  
2.  Clique o *ApplicationName* **opções** botão.  
  
3.  No painel de categorias, clique em **Add-ins**.  
  
4.  No painel de detalhes, verifique se o suplemento do VSTO aparece na **suplementos de aplicativo desabilitado** lista.  
  
     O **nome** coluna especifica o nome do assembly e o **local** coluna especifica o caminho completo do manifesto do aplicativo.  
  
5.  No **Manage** , clique em **itens desabilitados**e, em seguida, clique em **vá**.  
  
6.  Selecione o suplemento do VSTO e clique em **habilitar**.  
  
7.  Clique em **Fechar**.  
  
## <a name="soft-disabled-vsto-add-ins"></a>Suplementos do VSTO do soft-desabilitado  
 Desabilitando reversível pode ocorrer quando um suplemento do VSTO produz um erro que não faz com que o aplicativo fechar inesperadamente. Por exemplo, um aplicativo flexível pode desativar um suplemento do VSTO se ele lançar uma exceção sem tratamento ao <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos está em execução.  
  
> [!NOTE]  
>  Quando você reabilitar um suplemento do VSTO do soft-desabilitado, o aplicativo imediatamente tenta carregar o suplemento do VSTO. Se não tiver sido corrigido o problema que causou inicialmente o aplicativo reversível desabilitar o suplemento do VSTO, o aplicativo de forma reversível desabilitará o suplemento do VSTO novamente.  
  
### <a name="to-re-enable-a-vsto-add-in"></a>Para reabilitar um suplemento do VSTO  
  
1.  No aplicativo, clique no **arquivo** guia.  
  
2.  Clique o *ApplicationName* **opções** botão.  
  
3.  No painel de categorias, clique em **Add-ins**.  
  
4.  No painel de detalhes, verifique se o suplemento do VSTO aparece na **Add-ins de aplicativos inativo** lista.  
  
     O **nome** coluna especifica o nome do assembly e o **local** coluna especifica o caminho completo do manifesto do aplicativo.  
  
5.  No **Manage** , clique em **suplementos COM**e, em seguida, clique em **vá**.  
  
6.  No **suplementos COM** caixa de diálogo, selecione a caixa de seleção ao lado de desabilitado suplemento VSTO.  
  
7.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Compilar soluções do Office](../vsto/building-office-solutions.md)   
 [Depurar projetos do Office](../vsto/debugging-office-projects.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)  
  
  