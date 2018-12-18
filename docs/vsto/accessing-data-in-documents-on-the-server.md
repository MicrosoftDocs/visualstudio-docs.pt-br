---
title: Acessar dados em documentos no servidor
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], accessing on server
- data access [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 70c00a9c0de4afd9f54062e1c2ffabcc2911a538
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305566"
---
# <a name="access-data-in-documents-on-the-server"></a>Acessar dados em documentos no servidor
  Você pode programar os dados em uma personalização no nível do documento sem precisar usar o modelo de objeto do Microsoft Office Word ou Microsoft Office Excel. Isso significa que você pode acessar dados que estão contidos em um documento em um servidor que não tenha o Word ou Excel instalado. Por exemplo, o código em um servidor (por exemplo, em um [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] página) podem personalizar os dados em um documento e enviar o documento personalizado para o usuário final. Quando o usuário final abre o documento, o código de associação de dados em que o assembly da solução associa os dados personalizados no documento. Isso é possível porque os dados do documento são separados da interface do usuário. Para obter mais informações, consulte [armazenado em cache dados personalizações no nível do documento](../vsto/cached-data-in-document-level-customizations.md).  

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  

## <a name="cache-data-for-use-on-a-server"></a>Dados de cache para uso em um servidor  
 Para armazenar em cache um objeto de dados em um documento, marcá-la com o <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> de atributo em tempo de design, ou usar o `StartCaching` método de um item de host em tempo de execução. Quando você armazena em cache um objeto de dados em um documento, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] serializa o objeto em uma cadeia de caracteres XML que é armazenada no documento. Objetos devem atender a certos requisitos para ser qualificado para o cache. Para obter mais informações, consulte [armazenar em Cache dados](../vsto/caching-data.md).  

 Código do lado do servidor pode manipular quaisquer objetos de dados no cache de dados. Controles que estão associados às instâncias de dados armazenados em cache são sincronizados com a interface do usuário, para que as alterações do lado do servidor que são feitas nos dados aparecerão automaticamente quando o documento é aberto no cliente.  

## <a name="access-data-in-the-cache"></a>Acessar dados em cache  
 Você pode acessar dados no cache de aplicativos fora do escritório, por exemplo, de um aplicativo de console, um aplicativo do Windows Forms ou uma página da Web. O aplicativo que acessa os dados armazenados em cache deve ter a confiança total; um aplicativo Web que tenha relação de confiança parcial não pode inserir, recuperar ou alterar dados armazenados em cache em um documento do Office.  

 O cache de dados está acessível por meio de uma hierarquia de coleções que é exposta pela <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> propriedade do <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe:  

- O <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> propriedade retorna um <xref:Microsoft.VisualStudio.Tools.Applications.CachedData>, que contém todos os dados armazenados em cache em uma personalização no nível de documento.  

- Cada <xref:Microsoft.VisualStudio.Tools.Applications.CachedData> contém um ou mais <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> objetos. Um <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> contém todos os objetos de dados armazenados em cache que são definidos em uma única classe.  

- Cada <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> contém um ou mais <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> objetos. Um <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> representa um objeto de dados armazenados em cache único.  

  O exemplo de código a seguir demonstra como acessar uma cadeia de caracteres armazenados em cache o `Sheet1` classe de um projeto de pasta de trabalho do Excel. Este exemplo é parte de um exemplo maior fornecido para o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> método.  

  [!code-csharp[Trin_ServerDocument#12](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#12)]
  [!code-vb[Trin_ServerDocument#12](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#12)]  

## <a name="modify-data-in-the-cache"></a>Modificar dados em cache  
 Para modificar um objeto de dados armazenados em cache, você normalmente executam as seguintes etapas:  

1.  Desserialize a representação XML do objeto armazenado em cache em uma nova instância do objeto. Você pode acessar o XML usando o <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> propriedade do <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> que representa o objeto de dados armazenados em cache.  

2.  Faça as alterações a essa cópia.  

3.  Serialize o objeto alterado novamente no cache de dados usando uma das seguintes opções:  

    -   Se você deseja serializar automaticamente as alterações, use o <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> método. Esse método usa o **DiffGram** formato de serialização <xref:System.Data.DataSet>, <xref:System.Data.DataTable>e objetos de conjunto de dados tipados no cache de dados. O **DiffGram** formato garante que as alterações para o cache de dados em um documento offline são enviadas corretamente para o servidor.  

    -   Se você quiser executar sua própria serialização as alterações nos dados armazenados em cache, você pode escrever diretamente para o <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> propriedade. Especifique o **DiffGram** Formatar se você usar um <xref:System.Data.Common.DataAdapter> para atualizar um banco de dados com alterações feitas nos dados em um <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, ou com o tipo de conjunto de dados. Caso contrário, o <xref:System.Data.Common.DataAdapter> atualizará o banco de dados, adicionando novas linhas em vez de modificar linhas existentes.  

### <a name="modify-data-without-deserializing-the-current-value"></a>Modificar os dados sem desserializar o valor atual  
 Em alguns casos, talvez você queira modificar o valor do objeto em cache sem primeiro ao desserializar o valor atual. Por exemplo, você pode fazer isso se você estiver alterando o valor de um objeto que tem um tipo simples, como uma cadeia de caracteres ou inteiro, ou se você estiver inicializando em um cache <xref:System.Data.DataSet> em um documento em um servidor. Nesses casos, você pode usar o <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> método sem primeiro ao desserializar o valor atual do objeto armazenado em cache.  

 O exemplo de código a seguir demonstra como alterar o valor de uma cadeia de caracteres armazenados em cache o `Sheet1` classe de um projeto de pasta de trabalho do Excel. Este exemplo é parte de um exemplo maior fornecido para o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> método.  

 [!code-csharp[Trin_ServerDocument#11](../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs#11)]
 [!code-vb[Trin_ServerDocument#11](../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb#11)]  

### <a name="modify-null-values-in-the-data-cache"></a>Modificar valores nulos no cache de dados  
 O cache de dados não armazena objetos que têm o valor **nulo** quando o documento for salvo e fechado. Essa limitação tem várias consequências quando você modifica os dados armazenados em cache:  

-   Se você definir qualquer objeto no cache de dados para o valor **nulo**, todos os objetos no cache de dados serão automaticamente definidos como **nulo** quando o documento for aberto, e o cache de dados inteira será limpo quando a documento for salvo e fechado. Ou seja, todos os objetos armazenados em cache serão removidos do cache de dados e o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> coleção estará vazia.  

-   Se você criar uma solução com **nulo** objetos no cache de dados e você deseja inicializar esses objetos usando o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe antes do documento é aberto pela primeira vez, você deve garantir que você inicialize todos os objetos no cache de dados. Se você inicializar somente alguns dos objetos, todos os objetos serão definidos como **nulo** quando o documento for aberto, e o cache de dados inteira será removido quando o documento for salvo e fechado.  

## <a name="access-typed-datasets-in-the-cache"></a>Acesso digitado a conjuntos de dados no cache  
 Se você deseja acessar os dados em um dataset tipado de uma solução do Office e de um aplicativo fora do escritório, como um aplicativo do Windows Forms ou um [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] projeto, você deve definir o conjunto de dados tipado em um assembly separado que é referenciado em ambas projetos. Se você adiciona o conjunto de dados tipado para cada projeto usando o **Data Source Configuration** assistente ou na **Dataset Designer**, o .NET Framework tratará os conjuntos de dados tipados em dois projetos de diferentes tipos . Para obter mais informações sobre como criar datasets tipados, consulte [criar e configurar conjuntos de dados no Visual Studio](/visualstudio/data-tools/create-and-configure-datasets-in-visual-studio).  

## <a name="see-also"></a>Consulte também  
 [Acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md)   
 [Dados armazenados em cache em personalizações no nível de documento](../vsto/cached-data-in-document-level-customizations.md)  
