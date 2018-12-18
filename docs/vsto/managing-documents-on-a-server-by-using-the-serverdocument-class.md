---
title: Gerenciar documentos em um servidor usando a classe ServerDocument
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], managing on server
- Office documents [Office development in Visual Studio, managing on server
- ServerDocument class, managing documents on server
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e983f4cf1b90150113fcfa33702d85bb41a30924
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49939131"
---
# <a name="manage-documents-on-a-server-by-using-the-serverdocument-class"></a>Gerenciar documentos em um servidor usando a classe ServerDocument
  Você pode usar o `ServerDocument` classe o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] para gerenciar vários aspectos das personalizações em nível de documento, mesmo se o Microsoft Office Word e Microsoft Office Excel não são instalados. Você pode executar as seguintes tarefas:  
  
- Acessar e modificar dados no cache de dados de um documento ou pasta de trabalho. Para obter mais informações, consulte [trabalhar com dados armazenados em cache no documento](#CachedData).  
  
- Gerencie o assembly de personalização que está associado um documento. Para obter mais informações, consulte [gerenciar a personalização do documento](#CustomizationInfo).  
  
  [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
## <a name="understand-the-serverdocument-class"></a>Entenda a classe ServerDocument  
 O `ServerDocument` classe é projetada para ser usada em computadores que não têm o Office instalado. Portanto, você normalmente usa essa classe em aplicativos que não se integram com o Office, como projetos de Console ou projetos do Windows Forms, em vez de projetos do Office. Use o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe de *ServerDocument* assembly.  
  
 O `ServerDocument` classe pode ser usada para operar em personalizações no nível do documento que foram criadas usando [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)].  
  
 Para obter mais informações sobre o Visual Studio 2010 Tools for Office Runtime e as extensões do Office para o .NET Framework, consulte [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
> [!NOTE]  
>  Se você tiver um aplicativo herdado que usa o `ServerDocument` classe na `Visual Studio Tools for Office` sistema (versão 3.0 Runtime), o `Visual Studio Tools for Office` (versão 3.0 runtime) do sistema deve ser instalado em computadores que executam o aplicativo. O `Visual Studio 2010 Tools for Office runtime` não é possível executar esses aplicativos.  
  
##  <a name="CachedData"></a> Trabalhar com dados armazenados em cache no documento  
 O `ServerDocument` classe fornece membros que você pode usar para trabalhar com o cache de dados em documentos personalizados. Para obter mais informações sobre os dados armazenados em cache, consulte [armazenar dados em Cache](../vsto/caching-data.md) e [acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md).  
  
 A tabela a seguir lista os membros que você pode usar para trabalhar com dados armazenados em cache.  
  
|Tarefa|Membro a ser usado|  
|----------|-------------------|  
|Para determinar se um documento tem um cache de dados.|O método <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.IsCacheEnabled%2A>.|  
|Para acessar os dados armazenados em cache em um documento.<br /><br /> Para obter mais informações, consulte [acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md).|A propriedade de <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> .|  
  
##  <a name="CustomizationInfo"></a> Gerenciar a personalização do documento  
 Você pode usar os membros de `ServerDocument` classe para gerenciar o assembly de personalização que está associado um documento. Por exemplo, programaticamente você pode remover a personalização de um documento, para que o documento não é parte de uma personalização.  
  
 A tabela a seguir lista os membros que você pode usar para gerenciar o assembly de personalização.  
  
|Tarefa|Membro a ser usado|  
|----------|-------------------|  
|Para determinar se um documento é parte de uma personalização no nível de documento.|O método <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.GetCustomizationVersion%2A>.|  
|Por meio de programação anexar uma personalização a um documento em tempo de execução.<br /><br /> Para obter mais informações, consulte [como: anexar extensões para documentos de código gerenciado](../vsto/how-to-attach-managed-code-extensions-to-documents.md)|Um do <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> métodos.|  
|Para remover programaticamente uma personalização de um documento em tempo de execução.<br /><br /> Para obter mais informações, consulte [como: remover de extensões de código gerenciado de documentos](../vsto/how-to-remove-managed-code-extensions-from-documents.md).|O método <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A>.|  
|Para obter a URL do manifesto de implantação que está associada ao documento.|A propriedade de <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.DeploymentManifestUrl%2A> .|  
  
## <a name="see-also"></a>Consulte também  
 [Como: anexar extensões para documentos de código gerenciado](../vsto/how-to-attach-managed-code-extensions-to-documents.md)   
 [Como: remover as extensões de código gerenciado de documentos](../vsto/how-to-remove-managed-code-extensions-from-documents.md)   
 [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md)   
 [Dados de cache](../vsto/caching-data.md)  
  