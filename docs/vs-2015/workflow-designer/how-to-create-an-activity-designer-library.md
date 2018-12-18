---
title: 'Como: criar uma biblioteca do Designer de atividade | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 5b62e092-63b3-462d-9d77-fb112482f45d
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 6802f92f349d15d48935f4e7c3db85abf7c12535
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49258265"
---
# <a name="how-to-create-an-activity-designer-library"></a>Como: Crie uma biblioteca do designer de atividade
Designers personalizados de atividade permitem que você crie uma interface de usuário para uma atividade padrão ou personalizado. Você controla a complexidade da interface do usuário e tem a capacidade de criar mais de um designer de atividade para uma atividade. Este cenário permite que você crie os designers que são personalizados para mais audiências.  
  
### <a name="to-create-an-activity-designer-library"></a>Para criar uma biblioteca do designer de atividade  
  
1.  Inicie o [!INCLUDE[vs2010](../includes/vs2010-md.md)].  
  
2.  Sobre o **arquivo** , aponte para **New**e, em seguida, selecione **projeto...** Para abrir o **novo projeto** caixa de diálogo.  
  
3.  No **tipos de projeto** painel, selecione **fluxo de trabalho** de qualquer um os **Visual c#** ou **Visual Basic** agrupamentos, dependendo de sua preferência idioma.  
  
4.  No **modelos** painel, selecione **biblioteca do Designer de atividade**.  
  
5.  No **nome** , digite um nome descritivo para seu projeto para torná-lo mais fácil identificar.  
  
6.  No **local** , digite o diretório no qual você deseja salvar seu projeto, ou clique em **procurar** para navegar até ele.  
  
7.  No **Solution** caixa, digite um nome descritivo para sua solução e clique **Okey**.  
  
    > [!NOTE]
    >  Se você deseja adicionar um aplicativo de console do fluxo de trabalho a uma solução existente, abra essa solução na [!INCLUDE[vs2010](../includes/vs2010-md.md)], clique com o botão direito na solução no **Gerenciador de soluções**e selecione **Add**, em seguida, **Novo projeto...** Para abrir o **novo projeto** caixa de diálogo. Continuar conforme descrito acima neste procedimento.  
  
8.  O modelo de projeto cria uma definição de designer de atividade em XAML e o arquivo de código de implementação no código-fonte. [!INCLUDE[wfd1](../includes/wfd1-md.md)] abre e exibe a tela para o designer de atividade.  
  
9. Arraste [!INCLUDE[avalon1](../includes/avalon1-md.md)] controla a partir de **caixa de ferramentas** para a superfície de design para usá-los em seu designer personalizado de atividade.  Para obter um exemplo de como implementar um designer personalizado de atividade, consulte [como: criar um Designer personalizado de atividade](http://msdn.microsoft.com/library/2f3aade6-facc-44ef-9657-a407ef8b9b31).  
  
    > [!WARNING]
    >  Designers personalizados de atividade podem ser usados para atividades personalizadas, bem como para padrão [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)]atividades.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um projeto de fluxo de trabalho](../workflow-designer/creating-a-workflow-project.md)