---
title: 'Como: criar LINQ to SQL classes mapeadas para tabelas e exibições (Object Relational Designer) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0fb78bbc-7a78-4ab4-b32f-85ece912e660
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 550fc362cf1652df48e029461a4d5fbdc6f04006
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49269523"
---
# <a name="how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-or-designer"></a>Como: criar LINQ to SQL classes mapeadas para tabelas e exibições (Designer relacional de objetos)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
Classes LINQ to SQL mapeadas para tabelas de banco de dados e modos de exibição são chamados *classes de entidade*. A classe de entidade é mapeado para um registro, enquanto as propriedades individuais de uma classe de entidade mapeiam para as colunas individuais que compõem um registro. Criar classes de entidade que se baseiam no banco de dados tabelas ou exibições arrastando tabelas ou exibições do **Gerenciador de servidores**/**Database Explorer** até a [ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md). O [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] gera as classes e aplica o específico [! LINQ para atributos de SQL para habilitar o [! LINQ para funcionalidade de SQL (a comunicação de dados e recursos de edição a <xref:System.Data.Linq.DataContext>). Para obter informações detalhadas sobre o [! Classes LINQ to SQL, consulte [o LINQ no modelo de objeto do SQL](http://msdn.microsoft.com/library/81dd0c37-e2a4-4694-83b0-f2e49e693810).

> [!NOTE]
> O [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] é um mapeador relacional de objeto simples, pois suporta apenas as relações de mapeamento de 1:1. Em outras palavras, uma classe de entidade pode ter apenas uma relação de mapeamento de 1:1 com uma tabela ou exibição de banco de dados. O mapeamento complexo, como o mapeamento de uma classe de entidade para várias tabelas, não tem suporte. No entanto, você pode mapear uma classe de entidade para uma exibição que une várias tabelas relacionadas.

## <a name="create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>Criar classes LINQ to SQL que são mapeadas para tabelas ou exibições de banco de dados
 Arrastar tabelas ou exibições do **Gerenciador de servidores**/**Database Explorer** até a [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] cria classes de entidade além o <xref:System.Data.Linq.DataContext> métodos que são usados para executando as atualizações.

 Por padrão, o [! Execução LINQ to SQL cria a lógica para salvar as alterações de uma classe de entidade atualizável no banco de dados. Essa lógica é baseada no esquema da tabela (as definições de coluna e informações de chave primária). Se você não quiser esse comportamento, você pode configurar uma classe de entidade para usar procedimentos armazenados para executar inserções, atualizações e exclusões em vez de usar o padrão [! LINQ ao comportamento de tempo de execução do SQL. Para obter mais informações, consulte [como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer relacional de objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md).

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>Para criar classes LINQ to SQL que são mapeadas para tabelas ou exibições de banco de dados

1.  Na **Server**/**Database Explorer**, expanda **tabelas** ou **exibições** e localize a tabela de banco de dados ou exibição a que você deseja Para usar em seu aplicativo.

2.  Arraste a tabela ou exibição para o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].

     Uma classe de entidade é criada e aparece na superfície de design. A classe de entidade tem propriedades que mapeiam para as colunas na tabela ou exibição selecionada.

## <a name="create-an-object-data-source-and-display-the-data-on-a-form"></a>Crie um objeto de fonte de dados e exiba os dados em um formulário
 Depois de criar classes de entidade usando o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)], você pode criar uma fonte de dados de objeto e preencher o [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) com as classes de entidade.

#### <a name="to-create-an-object-data-source-based-on-linq-to-sql-entity-classes"></a>Para criar uma fonte de dados de objeto com base nas classes de entidade do LINQ to SQL

1.  Sobre o **Build** menu, clique em **compilar solução** para compilar seu projeto.

2.  Sobre o **dados** menu, clique em **Show Data Sources**.

3.  No **fontes de dados** janela, clique em **Add New Data Source**.

4.  Clique em **objeto** sobre o **escolher um tipo de fonte de dados** página e, em seguida, clique em **próxima**.

5.  Expanda os nós e localize e selecione sua classe.

    > [!NOTE]
    > Se o **cliente** classe não estiver disponível, cancele o assistente, compile o projeto e execute o assistente novamente.

6.  Clique em **terminar** para criar a fonte de dados e adicionar o **Customer** classe de entidade para o **fontes de dados** janela.

7.  Arraste itens dos **fontes de dados** janela em um formulário.

## <a name="see-also"></a>Consulte também

- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)
- [Métodos DataContext (Designer Relacional de Objetos)](../data-tools/datacontext-methods-o-r-designer.md)
- [Como criar métodos DataContext mapeados para procedimentos armazenados e funções (Designer Relacional de Objetos)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
- [O modelo de objeto LINQ to SQL](http://msdn.microsoft.com/library/81dd0c37-e2a4-4694-83b0-f2e49e693810)
- [Passo a passo: personalizando a inserção, a atualização e o comportamento de exclusão de classes de entidade](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)
- [Passo a passo: Adicionando validação a Classes de entidade](http://msdn.microsoft.com/library/85b06a02-b2e3-4534-95b8-d077c8d4c1d7)
- [Como criar uma associação (relação) entre classes LINQ to SQL (Designer Relacional de Objetos)](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)