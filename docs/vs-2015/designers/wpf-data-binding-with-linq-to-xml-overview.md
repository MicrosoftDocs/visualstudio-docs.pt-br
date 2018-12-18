---
title: Visão geral da vinculação de dados do WPF com LINQ o XML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bf80845-891b-41de-a71b-4080b5bd3ea6
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 457a097d46f9af409580d3784bb577090db0c535
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49852408"
---
# <a name="wpf-data-binding-with-linq-to-xml-overview"></a>Visão geral da associação de dados do WPF com LINQ to XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico apresenta os recursos dinâmicos de vinculação de dados no namespace <xref:System.Xml.Linq>. Esses recursos podem ser usados como uma fonte de dados para elementos de interface do usuário no Windows Presentation Foundation (WPF).  
  
## <a name="xaml-and-linq-to-xml"></a>XAML e LINQ to XML  
 A linguagem XAML é um dialeto XML criado pela Microsoft para dar suporte a tecnologias do .NET Framework 3.0. Ela é usada em WPF para representar elementos de interface do usuário e recursos relacionados, como associação de eventos e dados. No Windows Workflow Foundation, o XAML é usado para representar a estrutura do programa, como o controle de programa (*fluxos de trabalho*). O XAML permite que os aspectos declarativos de uma tecnologia sejam separados do código procedural relacionado que define o comportamento mais individualizado de um programa.  
  
 Há duas maneiras de o XAML e o LINQ to XML poderem interagir:  
  
- Como os arquivos XAML são XMLs bem-formados, podem ser consultados e manipulados pelas tecnologias XML como LINQ to XML.  
  
- Como as consultas LINQ to XML representam uma fonte de dados, elas podem ser usadas como uma fonte de dados para vinculação de dados para elementos de interface de usuário do WPF.  
  
  Esta documentação descreve o segundo cenário.  
  
## <a name="data-binding-in-the-windows-presentation-foundation"></a>Vinculação de dados no Windows Presentation Foundation  
 A vinculação de dados do WPF permite que um elemento de interface de usuário associe uma de suas propriedades a uma fonte de dados. Um exemplo simples disso é um <xref:System.Windows.Controls.Label> cujo texto apresenta o valor de uma propriedade pública em um objeto definido pelo usuário. A vinculação de dados do WPF depende dos seguintes componentes:  
  
|Componente|Descrição|  
|---------------|-----------------|  
|Destino de associação|O elemento de interface do usuário a ser associado com a fonte de dados. Os elementos visuais no WPF são derivados da classe <xref:System.Windows.UIElement>.|  
|Propriedade de destino|A *propriedade de dependência* do destino da associação que reflete o valor da fonte da vinculação de dados. As propriedades de dependência têm suporte direto pela classe <xref:System.Windows.DependencyObject>, da qual <xref:System.Windows.UIElement>.|  
|Fonte de associação|O objeto de origem para um ou mais valores que são fornecidos para o elemento da interface de usuário para apresentação. O WPF oferece suporte automático aos seguintes tipos como fontes de associação: objetos CLR, objetos de dados ADO.NET, dados XML (de consultas XPath ou LINQ to XML) ou outro <xref:System.Windows.DependencyObject>.|  
|Caminho de origem|A propriedade da fonte de associação que resolve para o valor ou conjunto de valores que devem ser associados.|  
  
 Uma propriedade de dependência é um conceito específico do WPF que representa uma propriedade dinamicamente computada de um elemento de interface do usuário. Por exemplo, as propriedades de dependência geralmente têm valores padrão ou valores que são fornecidos por um elemento pai. Essas propriedades especiais têm o suporte de instâncias da classe <xref:System.Windows.DependencyProperty> (e não de campos com propriedades padrão). Para obter mais informações, consulte [Visão geral sobre propriedades de dependência](http://msdn.microsoft.com/library/d119d00c-3afb-48d6-87a0-c4da4f83dee5).  
  
### <a name="dynamic-data-binding-in-wpf"></a>Associação dinâmica de dados no WPF  
 Por padrão, a vinculação de dados ocorre somente quando o elemento de interface do usuário de destino é inicializado. Isso é chamado de associação *única*. Para a maioria das finalidades, isso é insuficiente; normalmente, uma solução de vinculação de dados exige que as alterações sejam propagadas dinamicamente em tempo de execução usando um destes procedimentos:  
  
- A associação *unidirecional* faz as alterações em um lado serem propagadas automaticamente. Mais comumente, as alterações da origem são refletidas no destino, mas o inverso muitas vezes pode ser útil.  
  
- Na associação *bidirecional*, as alterações da origem são propagadas automaticamente para o destino, e as alterações para o destino são propagadas automaticamente para a origem.  
  
  Para que a associação unidirecional ou bidirecional ocorra, a origem deve implementar um mecanismo de notificação de mudança, por exemplo, implementando a interface de <xref:System.ComponentModel.INotifyPropertyChanged> ou usando um padrão *PropertyNameChanged* para cada propriedade com suporte.  
  
  Para obter mais informações sobre vinculação de dados no WPF, consulte [Vinculação de dados (WPF)](http://msdn.microsoft.com/library/90f79b97-17e7-40d1-abf0-3ba600ad1d7e).  
  
## <a name="dynamic-properties-in-linq-to-xml-classes"></a>Propriedades dinâmicas nas classes LINQ to XML  
 A maioria de classes LINQ to XML não são qualificadas como fontes de dados dinâmicas adequadas do WPF: algumas das informações mais úteis está disponível somente através de métodos (e não propriedades), e as propriedades nessas classes não implementam as notificações de alteração. Para oferecer suporte à vinculação de dados do WPF, o LINQ to XML expõe um conjunto de *propriedades dinâmicas*.  
  
 Essas propriedades dinâmicas são as propriedades especiais em tempo de execução que duplicam a funcionalidade dos métodos existentes e as propriedades nas classes <xref:System.Xml.Linq.XAttribute> e de <xref:System.Xml.Linq.XElement>. Elas foram adicionados às classes exclusivamente para habilitá-las para atuar como fontes de dados dinâmicas para WPF. Para atender essa necessidade, todas essas propriedades dinâmicas implementam notificações de alterações. Uma referência detalhada sobre essas propriedades dinâmicas é fornecida na próxima seção, [Propriedades dinâmicas LINQ to XML](../designers/linq-to-xml-dynamic-properties.md).  
  
> [!NOTE]
>  Muitas das propriedades públicas padrão, localizadas em várias classes no namespace <xref:System.Xml.Linq>, podem ser usadas para a vinculação de dados única. No entanto, lembre-se de que nem a origem ou o destino serão atualizados dinamicamente neste esquema.  
  
### <a name="accessing-dynamic-properties"></a>Acessando propriedades dinâmicas  
 As propriedades dinâmicas nas classes <xref:System.Xml.Linq.XAttribute> e <xref:System.Xml.Linq.XElement> não podem ser acessadas como propriedades padrão. Por exemplo, em linguagens compatíveis com CLR, como C#, elas não podem ser:  
  
- Acessadas diretamente em tempo de compilação. As propriedades dinâmicas são invisíveis para o compilador e o Visual Studio IntelliSense.  
  
- Descobertas ou acessadas em tempo de execução usando reflexão .NET. Mesmo em tempo de execução, elas não são propriedades no sentido básico de CLR.  
  
  No C#, as propriedades dinâmicas podem ser acessadas somente em tempo de execução através de recursos fornecidos pelo namespace <xref:System.ComponentModel>.  
  
  Ao contrário, no entanto, em uma origem XML as propriedades dinâmicas podem ser acessadas através de uma notação simples da seguinte forma:  
  
```  
<object>.<dynamic-property>  
```  
  
 As propriedades dinâmicas para essas duas classes resolvem para um valor que pode ser usado diretamente, ou para um indexador que deve ser fornecido com um índice para obter o valor resultante ou uma coleção de valores. A última sintaxe utiliza o formato:  
  
```  
<object>.<dynamic-property>[<index-value>]  
```  
  
 Para obter mais informações, consulte [Propriedades dinâmicas LINQ to XML](../designers/linq-to-xml-dynamic-properties.md).  
  
 Para implementar a associação dinâmica de WPF, as propriedades dinâmicas serão usadas com os recursos fornecidos pelo namespace <xref:System.Windows.Data>, especialmente a classe <xref:System.Windows.Data.Binding>.  
  
## <a name="see-also"></a>Consulte também  
 [Vinculação de dados de WPF com LINQ to XML](../designers/wpf-data-binding-with-linq-to-xml.md)   
 [Propriedades dinâmicas LINQ to XML](../designers/linq-to-xml-dynamic-properties.md)   
 [XAML no WPF](http://msdn.microsoft.com/library/5d858575-a83b-42df-ad3f-047ed2d6e3c8)   
 [Associação de dados (WPF)](http://msdn.microsoft.com/library/90f79b97-17e7-40d1-abf0-3ba600ad1d7e)   
 [Usando a marcação de fluxo de trabalho](http://go.microsoft.com/fwlink/?LinkId=98685)



