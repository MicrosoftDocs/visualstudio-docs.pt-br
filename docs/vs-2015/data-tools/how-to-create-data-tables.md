---
title: 'Como: criar tabelas de dados | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Microsoft.VSDesigner.DataSource.DesignTable
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], creating data tables
- Dataset Designer, creating data tables
- tables [Visual Studio], creating
ms.assetid: 0e8bf4c4-3d05-4b20-9926-9d29914b26ed
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 8b26bf0cfbd387f33f9f038d5927db795a8f2769
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49288906"
---
# <a name="how-to-create-data-tables"></a>Como criar tabelas de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Dados podem ser armazenados na memória em <xref:System.Data.DataTable> objetos. (Conjuntos de dados são compostos de <xref:System.Data.DataTable> objetos.) Você normalmente cria novas tabelas de dados com o uso de TableAdapters a [Assistente de configuração TableAdapter](http://msdn.microsoft.com/library/3a373dd9-7b34-4d3c-a48b-69414512bac8) ou arrastando objetos de banco de dados do **Gerenciador de servidores** até o **Dataset Designer** .  
  
 Tabelas de dados são criadas como um subproduto quando você cria novas TableAdapters na [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f) também, mas também podem ser criados independentemente. Criar uma tabela de dados autônomo, arrastando uma <xref:System.Data.DataTable> do objeto do **conjunto de dados** guia da **caixa de ferramentas** até a **Dataset Designer**.  
  
> [!NOTE]
>  Para criar tabelas de dados programaticamente, consulte [criando um DataTable](http://msdn.microsoft.com/library/eecf9d78-60e3-4fdc-8de0-e56c13a89414).  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="creating-a-datatable-with-tableadapter"></a>Criando um DataTable com TableAdapter  
 Tabelas de dados com TableAdapters incluem métodos que preenchê-la com dados e gravam alterações de volta para o banco de dados. Criar TableAdapters executando o **Assistente de configuração TableAdapter** ou arrastando objetos de banco de dados do **Gerenciador de servidores** até o **Dataset Designer**.  
  
#### <a name="to-create-a-new-data-table-with-tableadapter"></a>Para criar uma nova tabela de dados com um TableAdapter  
  
1.  Abra o dataset na **Dataset Designer**. Para obter informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3).  
  
2.  Arraste uma **TableAdapter** da **conjunto de dados** guia da **caixa de ferramentas** para o **Dataset Designer**.  
  
     O **Assistente de configuração TableAdapter** é aberta.  
  
3.  Conclua o assistente. Para obter mais informações, consulte [Assistente de configuração TableAdapter](http://msdn.microsoft.com/library/3a373dd9-7b34-4d3c-a48b-69414512bac8)  
  
#### <a name="to-create-a-new-data-table-with-a-tableadapter-from-server-explorer"></a>Para criar uma nova tabela de dados com um TableAdapter no Gerenciador de servidores  
  
1.  Abra o dataset na **Designer de fonte de dados**.  
  
2.  Arraste um objeto de banco de dados (por exemplo, uma tabela) da **Gerenciador de servidores** até a **Dataset Designer**.  
  
## <a name="creating-a-standalone-datatable"></a>Criando um DataTable autônomo  
 Tabelas autônomas precisam ter `Fill` lógica implementada para ser preenchida com dados. Para obter informações sobre o preenchimento de tabelas de dados autônoma, consulte [populando um DataSet a partir de um DataAdapter](http://msdn.microsoft.com/library/3fa0ac7d-e266-4954-bfac-3fbe2f913153).  
  
#### <a name="to-create-a-new-stand-alone-data-table"></a>Para criar uma nova tabela de dados autônomo  
  
1.  Abra o dataset na **Dataset Designer**.  
  
2.  Arraste um <xref:System.Data.DataTable> do **conjunto de dados** guia da **caixa de ferramentas** até a **Dataset Designer**.  
  
3.  Adicione colunas para definir sua tabela de dados. Para obter mais informações, consulte [como: adicionar colunas a uma DataTable](http://msdn.microsoft.com/library/8ca21f77-b99a-47a7-a656-7cfd7a1bd9df).  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Data.DataTable>   
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Passo a passo: Exibindo dados em um formulário do Windows](../data-tools/walkthrough-displaying-data-on-a-windows-form.md)   
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Criar e editar Datasets tipados](../data-tools/creating-and-editing-typed-datasets.md)   
 [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)   
 [Janela Fontes de Dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)   
 [Como conectar-se a dados em um banco de dados](../data-tools/how-to-connect-to-data-in-a-database.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)