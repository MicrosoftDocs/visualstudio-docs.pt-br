---
title: Associar controles a dados no Visual Studio | Microsoft Docs
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
- data, displaying
- data sources, displaying data
- Data Sources window
- dislaying data
ms.assetid: be8b6623-86a6-493e-ab7a-050de4661fd6
caps.latest.revision: 42
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 3a4143777e51a03867e94f1d4ebdd9c8182a5401
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49291566"
---
# <a name="bind-controls-to-data-in-visual-studio"></a>Associar controles a dados no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Você pode exibir dados para usuários do seu aplicativo pela associação de dados a controles. Você pode criar esses controles ligados a dados arrastando itens dos **fontes de dados** window em uma superfície de design ou controles em uma superfície no Visual Studio.  
  
 Este tópico descreve as fontes de dados que você pode usar para criar controles associados a dados. Ele também descreve algumas das tarefas básicas envolvidas na associação de dados. Para obter detalhes mais específicos sobre como criar controles associados a dados, consulte [controles de ligar o Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md) e [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
## <a name="data-sources"></a>Fontes de dados  
 No contexto de associação de dados, uma fonte de dados representa os dados na memória que pode ser associado a sua interface do usuário. Em termos práticos, uma fonte de dados pode ser uma classe do Entity Framework, um conjunto de dados, um ponto de extremidade de serviço que é encapsulado em um objeto de proxy do .NET, uma classe LINQ to SQL, ou qualquer objeto do .NET ou coleção. Algumas fontes de dados permitem criar controles associados a dados arrastando itens dos **fontes de dados** janela, enquanto outras fontes de dados não. A tabela a seguir mostra quais fontes de dados têm suporte.  
  
|Fonte de dados|Suporte a arrastar e soltar no **o Designer de formulários do Windows**|Suporte a arrastar e soltar no **o WPF Designer**|Suporte a arrastar e soltar no **Silverlight Designer**|  
|-----------------|---------------------------------------------------------------|-----------------------------------------------------|-------------------------------------------------------------|  
|Conjunto de dados|Sim|Sim|Não|  
|Modelo de Dados de Entidade|Sim<sup>1</sup>|Sim|Sim|  
|Classes LINQ to SQL|Não<sup>2</sup>|Não<sup>2</sup>|Não<sup>2</sup>|  
|Serviços (incluindo [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)], WCF services e web services)|Sim|Sim|Sim|  
|Objeto|Sim|Sim|Sim|  
|SharePoint|Sim|Sim|Sim|  
  
 1. Gerar o modelo usando o **modelo de dados de entidade** assistente, em seguida, arrastar esses objetos para o designer.  
  
 2. Classes LINQ to SQL não aparecem na **fontes de dados** janela. No entanto, você pode adicionar uma nova fonte de dados de objeto com base no LINQ para classes SQL e, em seguida, arrastar esses objetos para o designer para criar controles associados a dados. Para obter mais informações, consulte [instruções passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233).  
  
## <a name="data-sources-window"></a>janela Fontes de Dados  
 Fontes de dados estão disponíveis para seu projeto como itens na **fontes de dados** janela. Esta janela está visível ou é acessível a partir de **exibição** menu, quando uma superfície de design do formulário é a janela ativa no seu projeto. Você pode arrastar itens dessa janela para criar controles associados aos dados subjacentes, e você também pode configurar as fontes de dados clicando com o.  
  
 ![Janela fontes de dados](../data-tools/media/raddata-data-sources-window.png "raddata janela de fontes de dados")  
  
 Para cada tipo de dados que aparece na **fontes de dados** janela, um controle padrão é criado quando você arrasta o item para o designer. Antes de arrastar um item a partir de **fontes de dados** janela, você pode alterar o controle que será criado. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
## <a name="tasks-involved-in-binding-controls-to-data"></a>Tarefas envolvidas na associação de controles a dados  
 A tabela a seguir lista algumas das tarefas mais comuns que você executa para associar controles a dados.  
  
|Tarefa|Mais informações|  
|----------|----------------------|  
|Abra o **fontes de dados** janela.|Abra uma superfície de design no editor e escolha **modo de exibição** > **fontes de dados**.|  
|Adicione uma fonte de dados ao seu projeto.|[Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)|  
|Definir o controle que é criado quando você arrasta um item do **fontes de dados** janela no Designer.|[Definir o controle a ser criado quando arrastado da janela Fontes de Dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)|  
|Modificar a lista de controles que estão associadas a itens do **fontes de dados** janela.|[Adicionar controles personalizados à janela Fontes de Dados](../data-tools/add-custom-controls-to-the-data-sources-window.md)|  
|Crie controles associados a dados.|[Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)<br /><br /> [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)|  
|Associe a um objeto ou coleção.|[Associar objetos no Visual Studio](../data-tools/bind-objects-in-visual-studio.md)|  
|Filtre dados que aparecem na interface do usuário.|[Filtrar e classificar dados em um Aplicativo do Windows Forms](../data-tools/filter-and-sort-data-in-a-windows-forms-application.md)|  
|Personalize legendas para controles.|[Personalizar o modo como o Visual Studio cria legendas para controles associados a dados](../data-tools/customize-how-visual-studio-creates-captions-for-data-bound-controls.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)   
 [Associação de dados do Windows Forms](http://msdn.microsoft.com/library/c3826d8e-ea25-4ad4-a669-45bfb19192aa)

