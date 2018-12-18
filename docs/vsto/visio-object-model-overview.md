---
title: Visão geral do modelo de objeto do Visio
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], object model
- object models [Office development in Visual Studio], Office
- object models [Office development in Visual Studio], Visio
- objects [Office development in Visual Studio], Office object models
- Office object models
- Visio object model
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 872665a9af220e1b86a3d053254880e3ababa6cd
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671398"
---
# <a name="visio-object-model-overview"></a>Visão geral do modelo de objeto do Visio
  Para desenvolver soluções do Office para Microsoft Office Visio, você pode interagir com o modelo de objeto do Visio. Esse modelo de objeto consiste em classes e interfaces que são fornecidos no assembly de interoperabilidade primário do Visio e são definidos na `Microsoft.Office.Interop.Visio` namespace.  
  
 Este tópico fornece uma visão geral do modelo de objeto do Visio. Para obter informações sobre como usar o modelo de objeto do Visio para executar tarefas em projetos do Office, consulte os tópicos a seguir:  
  
-   [Trabalhar com documentos do Visio](../vsto/working-with-visio-documents.md)  
  
-   [Trabalhar com formas do Visio](../vsto/working-with-visio-shapes.md)  
  
## <a name="understand-the-visio-object-model"></a>Entender o modelo de objeto do Visio  
 O Visio fornece muitos objetos com os quais você pode interagir. Esses objetos são organizados em uma hierarquia que segue rigorosamente a interface do usuário. Na parte superior da hierarquia é o [Microsoft.Office.Interop.Visio.Application](/office/vba/api/Visio.Application) objeto. Este objeto representa a instância atual do Visio. O `Microsoft.Office.Interop.Visio.Application` objeto contém o `Microsoft.Office.Interop.Visio.Document` e `Microsoft.Office.Interop.Visio.Page` objetos, bem como a `Microsoft.Office.Interop.Visio.Documents` e `Microsoft.Office.Interop.Visio.Pages` coleções. Cada um desses objetos e coleções tem vários métodos e propriedades que você pode acessar para manipular e interagir com ele.  
  
 Para obter mais informações, consulte a documentação de referência do VBA [Microsoft.Office.Interop.Visio.Application](/office/vba/api/Visio.Application), [Microsoft.Office.Interop.Visio.Document](/office/vba/api/Visio.Document), e [ Microsoft.Office.Interop.Visio.Page](/office/vba/api/Visio.Page) objetos e também a [Microsoft.Office.Interop.Visio.Documents](/office/vba/api/Visio.Documents) e [Microsoft.Office.Interop.Visio.Pages](/office/vba/api/Visio.Pages) coleções.  
  
 As seções a seguir descrevem brevemente os objetos de nível superior e como eles interagem entre si. Esses objetos incluem os seguintes objetos:  
  
-   Objeto de aplicativo  
  
-   Objeto de documento  
  
-   Objeto Page  
  
### <a name="application-object"></a>Objeto de aplicativo  
 O objeto Microsoft.Office.Interop.Visio.Application representa o aplicativo do Visio e é o pai de todos os outros objetos. Seus membros geralmente se aplicam para o Visio como um todo. Você pode usar as propriedades e métodos do Microsoft.Office.Interop.Visio.Application e o `Microsoft.Office.Interop.Visio.ApplicationSettings` objetos para controlar o ambiente do Visio.  
  
 Em projetos de suplemento do VSTO, você pode acessar o objeto Microsoft.Office.Interop.Visio.Application usando o `Application` campo do `ThisAddIn` classe. Para obter mais informações, consulte [Programando a validação](../vsto/programming-vsto-add-ins.md).  
  
### <a name="document-object"></a>Objeto de documento  
 O objeto Microsoft.Office.Interop.Visio.Document é fundamental para programação do Visio. Ele representa um desenho, estêncil ou arquivo de modelo. Quando você abre um documento do Visio ou cria um novo documento, você cria um novo objeto Microsoft.Office.Interop.Visio.Document, que é adicionado à coleção do objeto Microsoft.Office.Interop.Visio.Application Microsoft.Office.Interop.Visio.Documents .  
  
 O documento que tem o foco é chamado o documento ativo. Ele é representado pelo `Microsoft.Office.Interop.Visio.Application.ActiveDocument` propriedade do objeto Microsoft.Office.Interop.Visio.Application.  
  
### <a name="page-object"></a>Objeto Page  
 O objeto Microsoft.Office.Interop.Visio.Page representa a área de desenho de uma página de primeiro plano ou uma página de fundo. Você pode usar o `Microsoft.Office.Interop.Visio.Page.Background` propriedade para determinar se uma página é uma página de primeiro plano ou segundo plano.  
  
 Para criar formas, você pode usar métodos que incluem o `Microsoft.Office.Interop.Visio.Page.DrawSpline` e `Microsoft.Office.Interop.Visio.Page.DrawOval` métodos. Além disso, você pode recuperar os mestres de estênceis e colocar as formas em uma página usando o `Microsoft.Office.Interop.Visio.Page.Drop` ou `Microsoft.Office.Interop.Visio.Page.DropMany` métodos.  
  
## <a name="use-the-visio-object-model-documentation"></a>Use a documentação do modelo de objeto do Visio  
 Para obter informações completas sobre o modelo de objeto do Visio, consulte a referência de modelo de objeto do Visio VBA. A referência de modelo de objeto VBA documenta o modelo de objeto do Visio, conforme ele é exposto ao Visual Basic para código Applications (VBA). Para obter mais informações, consulte [referência de modelo de objeto do Visio 2010](http://go.microsoft.com/fwlink/?LinkId=199775).  
  
 Todos os objetos e membros na referência de modelo de objeto do VBA correspondem aos tipos e membros no Visio assembly de interoperabilidade primário (PIA). Por exemplo, o `Document` objeto na referência de modelo de objeto do VBA corresponde ao tipo Microsoft.Office.Interop.Visio.Document no PIA do Visio. Embora a referência de modelo de objeto VBA fornece exemplos de código para a maioria das propriedades, métodos e eventos, você deve converter o código VBA essa referência para o Visual Basic ou Visual c#, se você quiser usá-los em um projeto de suplemento VSTO do Visio que você cria usando o Visual Studio.  
  
> [!NOTE]  
>  Neste momento, não há nenhuma documentação de referência para o assembly de interoperabilidade primária do Visio.  
  
 Para obter exemplos de código relacionadas e ferramentas adicionais para a criação de soluções do Visio, consulte [software development kit do Visio 2010](http://go.microsoft.com/fwlink/?LinkId=196501).  
  
### <a name="additional-types-in-primary-interop-assemblies"></a>Outros tipos em assemblies de interoperabilidade primários  
 Você pode encontrar os tipos em assemblies de interoperabilidade primários que não são visíveis ao VBA devido às diferenças de implementação. VBA fornece uma exibição do modelo de objeto do Visio que inclui apenas os objetos e membros que você pode usar diretamente. Assemblies de interoperabilidade primários expõem o mesmo modelo de objeto, mas eles também incluem outras interfaces, classes e membros que convertem os objetos no modelo de objeto COM para código gerenciado. Esses itens adicionais não se destinam a ser usado diretamente em seu código.  
  
 Para obter mais informações, consulte [visão geral de classes e interfaces em assemblies de interoperabilidade primários do Office](http://go.microsoft.com/fwlink/?LinkId=189592) e [assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md).  
  
## <a name="see-also"></a>Consulte também  
 [Soluções do Visio](../vsto/visio-solutions.md)   
 [Trabalhar com documentos do Visio](../vsto/working-with-visio-documents.md)   
 [Trabalhar com formas do Visio](../vsto/working-with-visio-shapes.md)  
  
  