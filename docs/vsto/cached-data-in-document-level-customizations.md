---
title: Dados armazenados em cache em personalizações no nível de documento
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data islands [Office development in Visual Studio]
- view [Office development in Visual Studio]
- caching data [Office development in Visual Studio], about caching data
- data caching [Office development in Visual Studio], about data caching
- data [Office development in Visual Studio], cache
- data [Office development in Visual Studio], document-level solutions
- document-level customizations [Office development in Visual Studio], data model
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: c17c24dda11ea210c190a31197b783036357f2de
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248290"
---
# <a name="cached-data-in-document-level-customizations"></a>Dados armazenados em cache em personalizações no nível de documento
  É dos principais objetivos das personalizações em nível de documento separar dados de exibição em documentos do Office. Dados refere-se às informações que são armazenadas no documento, incluindo números e texto. Modo de exibição refere-se a interface do usuário e o modelo de objeto do Microsoft Office Word e Microsoft Office Excel.  
  
 Visual Studio separa os dados da exibição no nível do documento, permitindo que os dados a ser inserido como uma *ilha de dados*, também chamado de *cache de dados*. Você pode ler ou modificar os dados diretamente sem iniciar o Word ou Excel. Isso é útil quando você precisa modificar dados em documentos em um servidor que não tenha o Microsoft Office instalado. Word e Excel são destinadas para uso em ambientes de cliente; eles não são projetados para ser executado em um servidor.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Para obter mais informações sobre personalizações em nível de documento, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41; ](../vsto/office-solutions-development-overview-vsto.md) e [arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md).  
  
## <a name="understand-the-cached-data-programming-model"></a>Entender o modelo de programação de dados armazenados em cache  
 Ilha de dados pode conter qualquer objeto em sua solução que atenda a certos requisitos. Esses objetos incluem <xref:System.Data.DataSet> objetos, <xref:System.Data.DataTable> objetos e qualquer outro objeto que pode ser serializado pelo <xref:System.Xml.Serialization.XmlSerializer> classe. Para obter mais informações, consulte [armazenar em Cache dados](../vsto/caching-data.md).  
  
 Para fornecer o modo de exibição para os dados em cache, você pode associar controles dos Windows Forms e *hospedar controles* no documento para objetos na ilha de dados. Associação de dados entre os controles ligados a dados e da ilha de dados mantém as duas sincronizadas. Você também pode adicionar código de validação para os dados que não independentes dos controles. Para obter mais informações, consulte [ligar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).  
  
 Controles de host são estendidos versões de objetos nativos em modelos de objeto do Excel e Word. Ao contrário de objetos nativos, controles de host podem ser vinculados diretamente a objetos de dados gerenciados. Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md) e [controles de formulários do Windows de visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md).  
  
## <a name="access-cached-data-on-the-server"></a>Dados de acesso armazenada em cache no servidor  
 Para acessar dados armazenados em cache em um documento, você pode usar o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe. Essa classe faz parte do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)], e ele pode ser usado em um servidor sem execução Excel ou Word. Quando o usuário abre o documento depois que você modificar os dados armazenados em cache, todos os controles que são associados aos dados são sincronizados automaticamente com as alterações e o usuário é apresentado com os dados atualizados. Para obter mais informações, consulte [acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md).  
  
 Excel e Word não são necessários para gravar os dados no servidor, apenas para exibi-lo no cliente. Excel e Word precisa nem ser instalado no servidor. Isso fornece maior escalabilidade e a capacidade de executar o processamento de lote rápida de documentos que contêm as ilhas de dados.  
  
## <a name="data-caching-for-offline-use"></a>Dados em cache para uso offline  
 Armazenamento de dados na ilha de dados permite cenários offline. Quando um usuário abre um documento ou solicita o documento do servidor, a ilha de dados é preenchida com os dados mais recentes. Ilha de dados é armazenado em cache no documento e, em seguida, está disponível offline. O usuário (e seu código) podem manipular os dados, mesmo que nenhuma conexão ao vivo está disponível. Quando o usuário reconecta, as alterações aos dados podem ser propagadas de volta para uma fonte de dados do servidor.  
  
## <a name="cached-data-and-custom-xml-parts-compared"></a>Dados armazenados em cache e partes XML personalizadas em comparação comparadas  
 Partes XML personalizadas foram introduzidas no 2007 Microsoft Office system como uma maneira de armazenar partes arbitrárias de XML em um documento. Embora partes XML personalizadas são úteis em muitos dos mesmos cenários como o cache de dados, há algumas diferenças entre a ilha de dados e partes XML personalizadas. Para obter mais informações sobre partes XML personalizadas, consulte [visão geral de partes XML personalizadas](../vsto/custom-xml-parts-overview.md).  
  
 A tabela a seguir lista algumas das diferenças e semelhanças.  
  
||Cache de dados|Partes XML personalizadas|  
|-|----------------|----------------------|  
|Quais aplicativos do Office podem usá-los?|Personalizações no nível de documento para os seguintes aplicativos:<br /><br /> -Excel<br />-Word|Soluções de nível de documento e o nível de aplicativo para os seguintes aplicativos:<br /><br /> -Excel<br />-PowerPoint<br />-Word|  
|Quais tipos de dados pode armazenar?|Qualquer objeto público no seu assembly de personalização que atenda a certos requisitos. Para obter mais informações, consulte [armazenar em Cache dados](../vsto/caching-data.md).|Todos os dados XML.|  
|Você pode acessar os dados sem iniciar aplicativos do Microsoft Office?|Sim, usando o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe fornecida pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].|Sim, usando classes no <xref:System.IO.Packaging> namespace, ou usando o SDK de formato XML aberto.|  
  
## <a name="see-also"></a>Consulte também  
 [Dados em soluções do Office](../vsto/data-in-office-solutions.md)   
 [Arquitetura de soluções do Office no Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md)  
  
  