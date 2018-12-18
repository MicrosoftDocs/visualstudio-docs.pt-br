---
title: Dados de cache
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], about caching data
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: b46fa8b0138eff03757a7bd7828053cee039090f
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248110"
---
# <a name="cache-data"></a>Dados de cache
  Você pode armazenar em cache objetos de dados em uma personalização no nível de documento para que os dados possam ser acessados offline ou sem abrir o Microsoft Office Word ou Microsoft Office Excel. Para armazenar em cache um objeto, o objeto deve ter um tipo de dados que atenda a certos requisitos. Muitos tipos de dados comum no .NET Framework atendam a esses requisitos, incluindo <xref:System.String>, <xref:System.Data.DataSet>, e <xref:System.Data.DataTable>.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Há duas maneiras de adicionar um objeto ao cache de dados:  
  
- Para adicionar um objeto ao cache de dados quando a solução é criada, aplicar o <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> à declaração de objeto de atributo. Confira mais informações em [Como: Armazenar em cache dados para uso offline ou em um servidor](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md).  
  
- Para adicionar programaticamente um objeto ao cache de dados em tempo de execução, use o `StartCaching` método de um host de itens, como o `ThisDocument` ou `ThisWorkbook` classes. Confira mais informações em [Como: Armazenar em cache programaticamente uma fonte de dados em um documento do Office](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md).  
  
  Depois de adicionar um objeto ao cache de dados, você pode acessar e modificar os dados armazenados em cache sem iniciar o Word ou Excel. Para obter mais informações, consulte [acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md).  
  
## <a name="requirements-for-data-objects-to-be-cached"></a>Requisitos para objetos de dados sejam armazenados em cache  
 Para armazenar em cache um objeto de dados em sua solução, o objeto deve atender a esses requisitos:  
  
- Ser um campo público de leitura/gravação ou a propriedade de um item de host, como o `ThisDocument` ou `ThisWorkbook` classes.  
  
- Não se um indexador ou outra propriedade com parâmetros.  
  
  Além disso, o objeto de dados deve ser serializável pelo <xref:System.Xml.Serialization.XmlSerializer> classe, o que significa que o tipo do objeto deve ter as seguintes características:  
  
- Ser um tipo público.  
  
- Ter um construtor público sem parâmetros.  
  
- Não execute o código que requer privilégios de segurança adicional.  
  
- Expor somente de leitura/gravação propriedades públicas (outras propriedades serão ignoradas).  
  
- Não expor matrizes multidimensionais (matrizes aninhadas são aceitos).  
  
- Retorne interfaces de propriedades e campos.  
  
- Não implementar <xref:System.Collections.IDictionary> se uma coleção.  
  
  Quando você armazena em cache um objeto de dados, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] serializa o objeto em uma cadeia de caracteres XML que é armazenada em um *parte XML personalizada* no documento. Para obter mais informações, consulte [visão geral de partes XML personalizadas](../vsto/custom-xml-parts-overview.md).  
  
## <a name="cached-data-size-limits"></a>Limites de tamanho de dados armazenados em cache  
 Há alguns limites para a quantidade total de dados que você pode adicionar ao cache de dados em um documento e para o tamanho de qualquer objeto individual no cache de dados. Se você exceder esses limites, o aplicativo poderá fechar inesperadamente quando os dados são salvos para o cache de dados.  
  
 Para evitar esses limites, siga estas diretrizes:  
  
- Não adicione qualquer objeto maior do que 10 MB para o cache de dados.  
  
- Não adicione mais de 100 MB de dados total para o cache de dados em um único documento.  
  
  Estes são valores aproximados. Os limites exatos dependem de vários fatores, incluindo a RAM disponível e o número de processos em execução.  
  
## <a name="control-the-behavior-of-cached-objects"></a>Controlar o comportamento de objetos em cache  
 Para obter mais controle sobre o comportamento de um objeto armazenado em cache, você pode implementar o <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> interface no tipo de objeto armazenado em cache. Por exemplo, você pode implementar essa interface se você quiser controlar como o usuário é notificado quando o objeto foi alterado. Para obter exemplos de código que demonstram como implementar <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType>, consulte o `ControlCollection` classe no exemplo de controles dinâmicos do Excel e Word dinâmico Controls Sample em [amostras de desenvolvimento do Office e instruções passo a passo](../vsto/office-development-samples-and-walkthroughs.md).  
  
## <a name="persist-changes-to-cached-data-in-password-protected-documents"></a>Manter as alterações em dados armazenados em cache em documentos protegidos por senha  
 Se você armazenar em cache objetos de dados em um documento protegido com uma senha, as alterações nos dados armazenados em cache não serão salvas. Você pode salvar as alterações aos dados armazenados em cache por substituir dois métodos. Substituir esses métodos para remover temporariamente a proteção quando o documento é salvo e, em seguida, reaplicar a proteção depois que a operação for concluída.  
  
 Confira mais informações em [Como: Armazenar em cache os dados em um documento protegido por senha](../vsto/how-to-cache-data-in-a-password-protected-document.md).  
  
## <a name="prevent-data-loss-when-adding-null-values-to-the-data-cache"></a>Evitar a perda de dados ao adicionar valores nulos para o cache de dados  
 Quando você adiciona objetos ao cache de dados, todos os objetos armazenados em cache devem ser inicializados como um não -**nulo** valor antes do documento for salvo e fechado. Se qualquer objeto em cache tem um **nulo** valor quando o documento for salvo e fechado, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] automaticamente removerá todos os objetos em cache do cache de dados.  
  
 Se você adicionar um objeto com um **nulo** valor para o cache de dados usando o <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> atributo em tempo de design, você pode usar o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> objetos de classe para inicializar os dados em cache antes do documento é aberto. Isso é útil se você quiser inicializar os dados armazenados em cache em um servidor sem o Word ou Excel instalados, antes do documento é aberto por um usuário final. Para obter mais informações, consulte [acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como: Armazenar em cache dados para uso offline ou em um servidor](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)   
 [Como: Armazenar em cache programaticamente uma fonte de dados em um documento do Office](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)   
 [Como: Cache de dados em um documento protegido por senha](../vsto/how-to-cache-data-in-a-password-protected-document.md)   
 [Passo a passo: Criar uma relação de detalhes mestre usando um conjunto de dados armazenados em cache](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)  
  
  