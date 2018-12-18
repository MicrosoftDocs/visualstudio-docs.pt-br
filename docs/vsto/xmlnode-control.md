---
title: Controle XMLNode
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNode control
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: cd047814f11b5fddad868bd65b84deba369facd5
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35258883"
---
# <a name="xmlnode-control"></a>Controle XMLNode
  **Importante** as informações que propus neste tópico sobre o Microsoft Word são desenvolver ou apresentadas exclusivamente para o uso e benefício de indivíduos e organizações que estão localizados fora dos Estados Unidos e seus territórios ou que estão usando o programas que são executados em produtos do Microsoft Word que foram licenciados pela Microsoft antes de janeiro de 2010, quando a Microsoft removido uma implementação da funcionalidade específica relacionada para XML personalizado do Microsoft Word. Essas informações sobre o Microsoft Word não podem ser lidas ou usadas por indivíduos ou organizações nos Estados Unidos ou em seus territórios de quem estão usando ou desenvolver programas que são executados em produtos do Microsoft Word que foram licenciados pela Microsoft depois de 10 de janeiro de 2010 ; Esses produtos não se comportará como produtos licenciados antes dessa data ou adquirido e licenciado para uso fora dos Estados Unidos.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 O <xref:Microsoft.Office.Tools.Word.XMLNode> controle é um objeto de nó XML mapeado que expõe eventos e pode ser associado a dados. O <xref:Microsoft.Office.Tools.Word.XMLNode> controle é criado somente quando um elemento de esquema não repetição é mapeado para um documento do Microsoft Office Word. Depois que o Visual Studio cria o nó XML, você pode programar em relação a ela diretamente sem ter que percorrer o modelo de objeto do Word.  
  
 O <xref:Microsoft.Office.Tools.Word.XMLNode> controle pode ser excluído apenas removendo o mapeamento de elemento no Word.  
  
## <a name="bind-data-to-the-control"></a>Associar dados ao controle  
 Um <xref:Microsoft.Office.Tools.Word.XMLNode> controle dá suporte à vinculação de dados simples. O nó XML deve ser associado a uma fonte de dados usando o <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> propriedade. Se os dados no conjunto de dados associado forem atualizados, o <xref:Microsoft.Office.Tools.Word.XMLNode> controle reflete as alterações.  
  
## <a name="formatting"></a>Formatação  
 Formatação que pode ser aplicado a um <xref:Microsoft.Office.Interop.Word.XMLNode> objeto pode ser aplicado a um <xref:Microsoft.Office.Tools.Word.XMLNode> controle. Isso inclui fontes, estilos de sublinhado e estilos de caractere.  
  
## <a name="events"></a>Eventos  
 Os eventos a seguir estão disponíveis para o <xref:Microsoft.Office.Tools.Word.XMLNode> controle:  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNode.AfterInsert>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNode.BeforeDelete>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNode.BindingContextChanged>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect>  
  
-   <xref:System.ComponentModel.IComponent.Disposed>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNode.Select>  
  
-   <xref:Microsoft.Office.Tools.Word.XMLNode.ValidationError>  
  
## <a name="compare-events"></a>Comparar eventos  
 Você pode capturar um evento quando o usuário move o seu cursor dentro do contexto de um determinado <xref:Microsoft.Office.Tools.Word.XMLNode> controle. Por exemplo, você pode ter um <xref:Microsoft.Office.Tools.Word.XMLNode> controle chamado `Customer` que tem um filho <xref:Microsoft.Office.Tools.Word.XMLNode> controle denominado `Company`, e `Company` tem dois filhos <xref:Microsoft.Office.Tools.Word.XMLNode> controles chamados `CompanyName` e `CompanyRegion` da seguinte maneira:  
  
```xml  
<Customer>  
    <Company>  
        <CompanyName>  
        <CompanyRegion>  
```  
  
 Se você quiser mostrar um controle no painel de ações sempre que o cursor é movido para o `Company` nó, ela deve não importa se o cursor é colocado na `CompanyName` ou `CompanyRegion` porque eles são ambos dentro do contexto de `Company`. Nesse caso, você pode escrever seu código na <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> eventos de `Company`.  
  
 Na maioria dos casos, quando o cursor entra em um <xref:Microsoft.Office.Tools.Word.XMLNode> controlar, ambos os <xref:Microsoft.Office.Tools.Word.XMLNode.Select> e <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> eventos são gerados. A tabela a seguir mostra as diferenças entre esses eventos.  
  
|Selecionar evento|Evento ContextEnter|  
|------------------|------------------------|  
|Ocorre quando o cursor é colocado dentro um <xref:Microsoft.Office.Tools.Word.XMLNode>.|Ocorre quando o cursor é colocado dentro de um <xref:Microsoft.Office.Tools.Word.XMLNode> ou um de seus nós descendentes, de uma área fora do contexto do nó. Em outras palavras, ele é gerado somente quando o contexto é alterado.|  
  
 Por exemplo, quando você move o cursor de fora do `Customer` em `CompanyName`, o <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> evento `Customer`, `Company`, e `CompanyName` é gerado. Se você mover o cursor a partir do `CompanyName` para `CompanyRegion`, somente os <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> evento para `CompanyRegion` foi gerado porque você ainda estiver dentro do contexto de ambos `Company` e `Customer`.  
  
 As mesmas diferenças existem entre o <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave> evento e <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect> eventos.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Controle XMLNodes](../vsto/xmlnodes-control.md)   
 [Como: adicionar controles XMLNode a documentos do Word](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)   
 [Como: mapear esquemas para documentos do Word dentro do Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  