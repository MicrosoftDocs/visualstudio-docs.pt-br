---
title: Visão geral do Visual Studio O/R Designer
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 45e477c0-5c6b-41f9-b2d0-2808fb4f6537
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 7c7abaa95c3b7c8f5ab78b4d58f383243b176f7a
ms.sourcegitcommit: e9d1018a01af62c3dc5aeb6b325faba7e20bd496
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37089406"
---
# <a name="linq-to-sql-tools-in-visual-studio"></a>Ferramentas LINQ to SQL no Visual Studio

O LINQ to SQL foi a primeira tecnologia de mapeamento relacional de objeto lançada pela Microsoft. Ele funciona bem em cenários básicos e continua a ter suporte no Visual Studio, mas ele não está mais sob desenvolvimento ativo. Use o LINQ to SQL durante a manutenção de um aplicativo herdado que já está usando, ou em aplicativos simples que usam o SQL Server e não exigem mapeamento de várias tabela. Em geral, os novos aplicativos devem usar o Entity Framework quando uma camada de mapeador relacional de objeto é necessária.

No Visual Studio, você cria classes LINQ to SQL que representam tabelas SQL usando o **Object Relational Designer** (**Relational Designer**).

O **Relational Designer** tem duas áreas distintas na superfície de design: o painel das entidades à esquerda e o painel de métodos à direita. O painel das entidades é a principal superfície de design que exibe as classes de entidade, as associações, e hierarquias de herança. O painel de métodos é a superfície de design que exibe o <xref:System.Data.Linq.DataContext> métodos que são mapeados para procedimentos armazenados e funções.

O **Relational Designer** fornece uma superfície de design visual para a criação [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) classes de entidade e associações (relações) que são baseadas em objetos em um banco de dados. Em outras palavras, o **Relational Designer** cria um modelo de objeto em um aplicativo que mapeia para objetos em um banco de dados. Ele também gera um tipo mais acentuado <xref:System.Data.Linq.DataContext> que envia e recebe dados entre as classes de entidade e o banco de dados. O **Relational Designer** também fornece funcionalidade para mapear procedimentos armazenados e funções para <xref:System.Data.Linq.DataContext> métodos para retornar dados e preencher classes de entidade. Por fim, o **Relational Designer** fornece a capacidade de criar relações de herança entre classes de entidade.

## <a name="open-the-or-designer"></a>Abra o designer relacional de objetos

Para adicionar um LINQ no modelo de entidade do SQL ao seu projeto, escolha **Project** > **Adicionar Novo Item**e, em seguida, selecione **Classes LINQ to SQL** da lista de itens de projeto:

![Classes LINQ to SQL](../data-tools/media/raddata-linq-to-sql-classes.png)

O Visual Studio cria uma *dbml* de arquivo e o adiciona à sua solução. Este é o arquivo de mapeamento de XML e seus arquivos de código relacionadas.

![Classes LINQ to SQL no Gerenciador de soluções](../data-tools/media/raddata-linq-to-sql-classes-in-solution-explorer.png)

Quando você seleciona o *dbml* do arquivo, o Visual Studio mostra o **Relational Designer** superfície que permite que você crie visualmente o modelo. A ilustração a seguir mostra o designer após o Northwind `Customers` e `Orders` foram arrastadas de tabelas **Gerenciador de servidores**. Observe a relação entre as tabelas.

![LINQ to SQL Designer](../data-tools/media/raddata-linq-to-sql-designer.png)

> [!IMPORTANT]
> O **Relational Designer** é um mapeador relacional de objeto simples, pois suporta apenas as relações de mapeamento de 1:1. Em outras palavras, uma classe de entidade pode ter apenas uma relação de mapeamento de 1:1 com uma tabela ou exibição de banco de dados. Não há suporte para o mapeamento complexo, como o mapeamento de uma classe de entidade associado a uma tabela, Use o Entity Framework para o mapeamento complexo. Além disso, o designer é um gerador de código unidirecional. Isso significa que somente as alterações feitas à superfície de designer são refletidas no arquivo de código. Alterações manuais ao arquivo de código não são refletidas na **Relational Designer**. As alterações que você fizer manualmente no arquivo de código são substituídas quando o designer é salvo e o código for gerado novamente. Para obter informações sobre como adicionar código de usuário e estender as classes geradas pela **Relational Designer**, consulte [como: estender o código gerado pelo Designer relacional de objetos](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md).

## <a name="create-and-configure-the-datacontext"></a>Criar e configurar o DataContext

Depois de adicionar um **Classes LINQ to SQL** item a um projeto e abrir os **Relational Designer**, a superfície de design vazio representa vazio <xref:System.Data.Linq.DataContext> pronto para ser configurado. o <xref:System.Data.Linq.DataContext> é configurado com as informações de conexão fornecidas pelo primeiro item que é arrastado para a superfície de design. Portanto, o <xref:System.Data.Linq.DataContext> é configurado usando as informações de conexão do primeiro item descartado na superfície de design. Para obter mais informações sobre o <xref:System.Data.Linq.DataContext> classe, consulte [métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md).

## <a name="create-entity-classes-that-map-to-database-tables-and-views"></a>Criar classes de entidade que são mapeados para tabelas de banco de dados e exibições

Você pode criar classes de entidade mapeadas para tabelas e exibições arrastando tabelas de banco de dados e exibições da **Gerenciador de servidores** ou **Database Explorer** até o **Relational Designer**. Conforme indicado na seção anterior, o <xref:System.Data.Linq.DataContext> é configurado com as informações de conexão fornecidas pelo primeiro item que é arrastado para a superfície de design. Se um item subsequente que usa uma conexão diferente é adicionado para o **Relational Designer**, você pode alterar a conexão para o <xref:System.Data.Linq.DataContext>. Para obter mais informações, consulte [como: criar classes LINQ to SQL mapeadas para tabelas e exibições (Designer relacional de objetos)](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md).

## <a name="create-datacontext-methods-that-call-stored-procedures-and-functions"></a>Criar métodos DataContext que chamam procedimentos armazenados e funções

Você pode criar <xref:System.Data.Linq.DataContext> métodos que chamam (são mapeados) procedimentos armazenados e funções arrastando-as da **Gerenciador de servidores** ou **Gerenciador de banco de dados** até a **O/R Designer** . Procedimentos armazenados e funções são adicionadas para o **Relational Designer** como métodos do <xref:System.Data.Linq.DataContext>.

> [!NOTE]
> Quando você arrasta procedimentos armazenados e funções do **Gerenciador de servidores** ou **Database Explorer** até o **Relational Designer**, o tipo de retorno de gerado <xref:System.Data.Linq.DataContext> método difere dependendo de onde você solta o item. Para obter mais informações, consulte [métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md).

## <a name="configure-a-datacontext-to-use-stored-procedures-to-save-data-between-entity-classes-and-a-database"></a>Configurar um DataContext para usar procedimentos armazenados para salvar os dados entre as classes de entidade e um banco de dados

Conforme observado anteriormente, você pode criar os métodos de <xref:System.Data.Linq.DataContext> que chamam procedimentos armazenados e funções. Além disso, você também pode atribuir procedimentos armazenados que são usados para o padrão LINQ para o comportamento de tempo de execução SQL, que executa inserções, atualizações e exclusões. Para obter mais informações, consulte [como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer relacional de objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md).

## <a name="inheritance-and-the-or-designer"></a>Herança e o O/R designer

Como outros objetos, classes LINQ to SQL pode usar a herança e ser derivado de outras classes. Em uma base de dados, as relações de herança são criadas de várias maneiras. O **Relational Designer** suporta o conceito de herança de tabela única como geralmente é implementado em sistemas relacionais. Para obter mais informações, consulte [como: configurar a herança usando o Designer relacional de objetos](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md).

## <a name="linq-to-sql-queries"></a>Consultas LINQ to SQL

As classes de entidade criadas pelo **Relational Designer** são projetados para uso com [Language-Integrated query (LINQ)](/dotnet/csharp/linq/). Para obter mais informações, consulte [como: consultar informações](/dotnet/framework/data/adonet/sql/linq/how-to-query-for-information).

## <a name="separate-the-generated-datacontext-and-entity-class-code-into-different-namespaces"></a>Separar o código da classe DataContext e de entidade gerado em namespaces diferentes

O **Relational Designer** fornece o **Namespace de contexto** e **Namespace da entidade** propriedades no <xref:System.Data.Linq.DataContext>. Essas propriedades que determinam o namespace <xref:System.Data.Linq.DataContext> e o código de classe de entidade são gerados. Por padrão, essas propriedades são vazios e <xref:System.Data.Linq.DataContext> e classes de entidade são gerados no namespace do aplicativo. Para gerar o código em um namespace diferente do namespace do aplicativo, insira um valor para o **Namespace de contexto** e/ou **Namespace da entidade** propriedades.

## <a name="reference-content"></a>Conteúdo de referência

- <xref:System.Linq>
- <xref:System.Data.Linq>

## <a name="see-also"></a>Consulte também

- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)
- [Perguntas frequentes (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/frequently-asked-questions)