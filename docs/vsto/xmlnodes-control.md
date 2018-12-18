---
title: Controle XMLNodes
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNodes control, events
- XMLNodes control
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 18b1a9cf6028b02d16b15b17950b9918b7b79d89
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35258532"
---
# <a name="xmlnodes-control"></a>Controle XMLNodes
  **Importante** as informações que propus neste tópico sobre o Microsoft Word são desenvolver ou apresentadas exclusivamente para o uso e benefício de indivíduos e organizações que estão localizados fora dos Estados Unidos e seus territórios ou que estão usando o programas que são executados em produtos do Microsoft Word que foram licenciados pela Microsoft antes de janeiro de 2010, quando a Microsoft removido uma implementação da funcionalidade específica relacionada para XML personalizado do Microsoft Word. Essas informações sobre o Microsoft Word não podem ser lidas ou usadas por indivíduos ou organizações nos Estados Unidos ou em seus territórios de quem estão usando ou desenvolver programas que são executados em produtos do Microsoft Word que foram licenciados pela Microsoft depois de 10 de janeiro de 2010 ; Esses produtos não se comportará como produtos licenciados antes dessa data ou adquirido e licenciado para uso fora dos Estados Unidos.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 O <xref:Microsoft.Office.Tools.Word.XMLNodes> controle é uma coleção de objetos de nó XML mapeados que expõe eventos. O <xref:Microsoft.Office.Tools.Word.XMLNodes> controle é criado somente quando um elemento de esquema de repetição é mapeado para um documento do Microsoft Office Word. Se o elemento de repetição contém elementos filho, cada um dos elementos filho também será criada como um <xref:Microsoft.Office.Tools.Word.XMLNodes> controle.  
  
 Depois que o Visual Studio cria a coleção de nós XML, você pode programar o controle diretamente sem ter que percorrer o modelo de objeto do Word. O <xref:Microsoft.Office.Tools.Word.XMLNodes> controle pode ser excluído apenas removendo o mapeamento de elemento do documento.  
  
> [!NOTE]  
>  Se você acessar um elemento filho do <xref:Microsoft.Office.Tools.Word.XMLNodes> controlar por meio das <xref:Microsoft.Office.Tools.Word.XMLNodes.Item%2A> propriedade, ele retorna um <xref:Microsoft.Office.Interop.Word.XMLNode> objeto em vez de um <xref:Microsoft.Office.Tools.Word.XMLNode> controle. Para obter mais informações, consulte [limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md).  
  
## <a name="bind-data-to-the-control"></a>Associar dados ao controle  
 Um <xref:Microsoft.Office.Tools.Word.XMLNodes> controle não dá suporte a vinculação de dados. Isso ocorre porque o <xref:Microsoft.Office.Tools.Word.XMLNodes> controle não tem recursos de ligação de dados complexos e associação de dados simples não pode representar dados de repetição.  
  
## <a name="formatting"></a>Formatação  
 Qualquer formatação que pode ser aplicado ao texto dentro do documento pode ser aplicado a um <xref:Microsoft.Office.Tools.Word.XMLNodes> controle.  
  
## <a name="events"></a>Eventos  
 Os eventos disponíveis para o <xref:Microsoft.Office.Tools.Word.XMLNodes> controle são:  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNodes.AfterInsert>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNodes.BeforeDelete>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect>  
  
-   <xref:System.ComponentModel.IComponent.Disposed>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNodes.Select>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNodes.ValidationError>  
  
## <a name="compare-events"></a>Comparar eventos  
 Você pode capturar um evento quando o usuário move o seu cursor dentro do contexto de um determinado <xref:Microsoft.Office.Tools.Word.XMLNodes> controle. Por exemplo, você pode ter um <xref:Microsoft.Office.Tools.Word.XMLNodes> controle chamado `Customer` que tem um filho <xref:Microsoft.Office.Tools.Word.XMLNodes> controle denominado `Company`, e `Company` tem dois filhos <xref:Microsoft.Office.Tools.Word.XMLNodes> controles chamados `CompanyName` e `CompanyRegion` da seguinte maneira:  
  
```xml  
<Customer>  
    <Company>  
        <CompanyName>  
        <CompanyRegion>  
```  
  
 Se você quiser mostrar um controle no painel de ações sempre que o cursor é movido para o `Company` nó, ela deve não importa se o cursor é colocado na `CompanyName` ou `CompanyRegion` porque eles são ambos dentro do contexto de `Company`. Nesse caso, você pode escrever seu código na <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> eventos de `Company`.  
  
 Na maioria dos casos, quando o cursor entra em um <xref:Microsoft.Office.Tools.Word.XMLNodes> controlar, ambos os <xref:Microsoft.Office.Tools.Word.XMLNodes.Select> e <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> eventos são gerados. A tabela a seguir mostra as diferenças entre esses eventos.  
  
|Selecionar evento|Evento ContextEnter|  
|------------------|------------------------|  
|Ocorre quando o cursor é colocado dentro de um dos nós da coleção <xref:Microsoft.Office.Tools.Word.XMLNodes>.|Ocorre quando o cursor é movido para dentro de um dos nós, ou nós descendentes, da coleção <xref:Microsoft.Office.Tools.Word.XMLNodes> para uma área fora do contexto do nó. Em outras palavras, ele é disparado apenas quando o contexto é alterado e pode ser aumentado para várias aninhadas <xref:Microsoft.Office.Tools.Word.XMLNodes> controles.|  
  
 Por exemplo, quando você move o cursor de fora do `Customer` em `CompanyName`, o <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> eventos para `Customer`, `Company`, e `CompanyName` são gerados. Se você mover o cursor a partir `CompanyName` para `CompanyRegion`, o <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> eventos apenas para `CompanyRegion` é gerado, porque o contexto é o mesmo para ambos `Company` e `Customer`. Você pode ter vários `Company` nós no documento. Se você mover o cursor a partir o `CompanyName` nó de um `Company` para o `CompanyName` nó de outro `Company`, o contexto é o mesmo, portanto, somente o <xref:Microsoft.Office.Tools.Word.XMLNodes.Select> é gerado.  
  
 As mesmas diferenças existem entre o <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave> evento e o <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect> eventos.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Controle XMLNode](../vsto/xmlnode-control.md)   
 [Como: adicionar controles XMLNodes a documentos do Word](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)   
 [Como: mapear esquemas para documentos do Word dentro do Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  