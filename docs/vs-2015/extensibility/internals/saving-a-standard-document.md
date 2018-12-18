---
title: Salvar um documento padrão | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], saving standard documents
- projects [Visual Studio SDK], saving standard documents
- persistence, saving standard documents
ms.assetid: d692fedf-b46e-4d60-84bd-578635042235
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 72415a4ddfa3de9511aab4b52ae37960af872fde
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51803572"
---
# <a name="saving-a-standard-document"></a>Salvando um documento padrão
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O ambiente manipula o salvamento, salvar como e salvar todos os comandos. Quando um usuário escolhe **salvar**, **Salvar como**, ou **Salvar tudo** do **arquivo** menu ou fecha a solução, resultando em um  **Salvar tudo**, ocorre o seguinte processo.  
  
 ![Padrão do Editor](../../extensibility/internals/media/public.gif "pública")  
Salvar, salvar como e salvar tudo manipulação de comando para um editor padrão  
  
 Esse processo é detalhado nas etapas a seguir:  
  
1. Quando o **salve** e **Salvar como** comandos estiverem marcados, o ambiente usa o <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> de serviço para determinar a janela do documento ativo e, portanto, quais itens devem ser salvas. Depois que a janela de documento ativa é conhecida, o ambiente localiza o ponteiro de hierarquia e o identificador do item (itemID) para o documento na tabela de documento em execução. Para obter mais informações, consulte [tabela de documento em execução](../../extensibility/internals/running-document-table.md).  
  
    Quando o **Salvar tudo** comando estiver selecionado, o ambiente usa as informações na tabela de documento em execução para compilar a lista de todos os itens para salvar.  
  
2. Quando a solução recebe um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> chamada, ele itera no conjunto de itens selecionados (ou seja, as várias seleções expostas pelo <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> service).  
  
3. Em cada item na seleção, a solução usa o ponteiro de hierarquia para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> método para determinar se o **salvar** comando de menu deve ser habilitado. Se um ou mais itens estiverem sujos, o **salvar** comando está habilitado. Se a hierarquia usa um editor padrão, em seguida, os delegados de hierarquia consultando sujos status para o editor chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> método.  
  
4. Em cada item selecionado está sujo, a solução usa o ponteiro de hierarquia para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> método nas hierarquias apropriados.  
  
    É comum para a hierarquia usando um editor padrão para editar o documento. Nesse caso, os dados do documento de objeto para o editor deve dar suporte a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> interface. Ao receber o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> chamada de método, o projeto deve informar o editor que o documento está sendo salvo, chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SaveDocData%2A> método no objeto de dados de documento. O editor pode permitir que o ambiente lidar com o **Salvar como** caixa de diálogo, chamando `Query Service` para o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> interface. Isso retorna um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface. O editor deve, em seguida, chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> método, passando um ponteiro para o editor <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> implementação por meio do `pPersistFile` parâmetro. O ambiente, em seguida, executa a operação de salvamento e fornece o **Salvar como** caixa de diálogo para o editor. O ambiente, em seguida, chama de volta para o editor com <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>.  
  
5. Se o usuário está tentando salvar um documento sem título (ou seja, um documento não salvo anteriormente), um comando Salvar como, na verdade, é executado.  
  
6. Para o comando Salvar como, o ambiente exibe a caixa de diálogo Salvar como, solicitando que o usuário forneça um nome de arquivo.  
  
    Se o nome do arquivo foi alterado, a hierarquia é responsável por atualizar o quadro do documento informações armazenadas em cache chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A>(VSFPROPID_MkDocument).  
  
   Se o **Salvar como** comando move o local do documento e a hierarquia é sensível ao local do documento, em seguida, a hierarquia é responsável por entregando a propriedade da janela do documento aberto para outra hierarquia. Por exemplo, isso ocorre se o projeto controla se o arquivo é um arquivo (arquivo diverso) interno ou externo em relação ao projeto. Use o procedimento a seguir para alterar a propriedade de um arquivo ao projeto arquivos diversos.  
  
## <a name="changing-file-ownership"></a>Alterando a propriedade de arquivo  
  
#### <a name="to-change-file-ownership-to-the-miscellaneous-files-project"></a>Para alterar a propriedade de arquivo ao projeto arquivos diversos  
  
1.  Consultar o serviço para o <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> interface.  
  
     Um ponteiro para <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2> é retornado.  
  
2.  Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2.TransferDocument%2A> (`pszMkDocumentNew`, `punkWindowFrame`) a fim de transferir o documento para a nova hierarquia. A hierarquia de executar o comando Salvar como chama esse método.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 [Abrir e salvar itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md)

