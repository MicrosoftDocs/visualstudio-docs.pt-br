---
title: Visão geral do LINQ to SQL O/R Designer
ms.date: 11/04/2016
ms.topic: overview
ms.assetid: 45e477c0-5c6b-41f9-b2d0-2808fb4f6537
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 55f6fa2ad9eda2d701563d1fa99c76f5cd5c7c1d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282001"
---
# <a name="linq-to-sql-tools-in-visual-studio"></a>Ferramentas do LINQ to SQL no Visual Studio

LINQ to SQL foi a primeira tecnologia de mapeamento relacional de objeto lançada pela Microsoft. Ele funciona bem em cenários básicos e continua a ter suporte no Visual Studio, mas não está mais sob o desenvolvimento ativo. Use LINQ to SQL ao manter um aplicativo herdado que já o esteja usando, ou em aplicativos simples que usam SQL Server e não exigem mapeamento de várias tabelas. Em geral, novos aplicativos devem usar o Entity Framework quando uma camada de mapeador relacional de objeto é necessária.

## <a name="install-the-linq-to-sql-tools"></a>Instalar as ferramentas de LINQ to SQL

No Visual Studio, você cria LINQ to SQL classes que representam tabelas SQL usando o **Object Relational Designer** (**o/R Designer**). O o/R Designer é a interface do usuário para edição de arquivos. dbml. A edição de arquivos. dbml com uma superfície de designer requer as ferramentas de LINQ to SQL que não são instaladas por padrão como parte de qualquer uma das cargas de trabalho do Visual Studio.

Para instalar as ferramentas de LINQ to SQL, inicie o instalador do Visual Studio, escolha **Modificar**, selecione a guia **componentes individuais** e, em seguida, selecione **LINQ to SQL ferramentas** na categoria **ferramentas de código** .

## <a name="what-is-the-or-designer"></a>O que é o o/R Designer

O o **/R Designer** tem duas áreas distintas em sua superfície de design: o painel entidades à esquerda e o painel métodos à direita. O painel das entidades é a principal superfície de design que exibe as classes de entidade, as associações, e hierarquias de herança. O painel de métodos é a superfície de design que exibe os métodos do <xref:System.Data.Linq.DataContext> que são mapeados para os procedimentos armazenados e as funções.

O o **/R Designer** fornece uma superfície de Design Visual para criar [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) classes de entidade e associações (relações) que se baseiam em objetos em um banco de dados. Em outras palavras, o **/R Designer** cria um modelo de objeto em um aplicativo que mapeia para objetos em um banco de dados. Ele também gera um tipo fortemente tipado <xref:System.Data.Linq.DataContext> que envia e recebe dados entre as classes de entidade e o banco de dado. O o **/R Designer** também fornece funcionalidade para mapear procedimentos armazenados e funções para <xref:System.Data.Linq.DataContext> métodos de retorno de dados e preenchimento de classes de entidade. Por fim, o o **/R Designer** fornece a capacidade de projetar relações de herança entre classes de entidade.

## <a name="open-the-or-designer"></a>Abrir o o/R Designer

Para adicionar um modelo de entidade LINQ to SQL ao seu projeto, escolha **projeto**  >  **Adicionar novo item**e, em seguida, selecione **LINQ to SQL classes** na lista de itens de projeto:

![Classes do LINQ to SQL](../data-tools/media/raddata-linq-to-sql-classes.png)

O Visual Studio cria um arquivo *. dbml* e o adiciona à sua solução. Este é o arquivo de mapeamento XML e seus arquivos de código relacionados.

![LINQ to SQL classes no Gerenciador de Soluções](../data-tools/media/raddata-linq-to-sql-classes-in-solution-explorer.png)

Quando você seleciona o arquivo *. dbml* , o Visual Studio mostra a superfície **o/R Designer** que permite que você crie visualmente o modelo. A ilustração a seguir mostra o designer depois que a Northwind `Customers` e as `Orders` tabelas foram arrastadas de **Gerenciador de servidores**. Observe a relação entre as tabelas.

![Designer do LINQ to SQL](../data-tools/media/raddata-linq-to-sql-designer.png)

> [!IMPORTANT]
> O o **/R Designer** é um mapeador relacional de objeto simples, pois dá suporte apenas a relações de mapeamento 1:1. Em outras palavras, uma classe de entidade pode ter apenas uma relação de mapeamento de 1:1 com uma tabela ou exibição de banco de dados. Não há suporte para mapeamento complexo, como mapear uma classe de entidade para uma tabela unida; Use o Entity Framework para mapeamento complexo. Além disso, o designer é um gerador de código unidirecional. Isso significa que somente as alterações feitas à superfície de designer são refletidas no arquivo de código. As alterações manuais no arquivo de código não são refletidas no **designer o/R**. As alterações feitas manualmente no arquivo de código são substituídas quando o designer é salvo e o código é regenerado. Para obter informações sobre como adicionar código de usuário e estender as classes geradas pela **Relational Designer**, consulte [como: Estender o código gerado pelo Designer Relacional de Objetos](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md).

## <a name="create-and-configure-the-datacontext"></a>Criar e configurar o DataContext

Depois de adicionar um item de **classes de LINQ to SQL** a um projeto e abrir o o **/R Designer**, a superfície de design vazia representa um vazio <xref:System.Data.Linq.DataContext> pronto para ser configurado. O <xref:System.Data.Linq.DataContext> é configurado com as informações de conexão fornecidas pelo primeiro item que é arrastado para a superfície de design. Portanto, o <xref:System.Data.Linq.DataContext> é configurado usando as informações de conexão do primeiro item solto na superfície de design. Para obter mais informações sobre a <xref:System.Data.Linq.DataContext> classe, consulte [métodos DataContext (o/R Designer)](../data-tools/datacontext-methods-o-r-designer.md).

## <a name="create-entity-classes-that-map-to-database-tables-and-views"></a>Criar classes de entidade que são mapeadas para exibições e tabelas de banco de dados

Você pode criar classes de entidade mapeadas para tabelas e exibições arrastando tabelas e exibições de banco de dados de **Gerenciador de servidores** ou **Gerenciador de banco de dados** para o o **/R Designer**. Conforme indicado na seção anterior, o <xref:System.Data.Linq.DataContext> é configurado com as informações de conexão fornecidas pelo primeiro item que é arrastado para a superfície de design. Se um item subsequente que usa uma conexão diferente for adicionado ao o **/R Designer**, você poderá alterar a conexão para o <xref:System.Data.Linq.DataContext> . Para obter mais informações, consulte [como: criar classes de LINQ to SQL mapeadas para tabelas e exibições (O/R Designer)](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md).

## <a name="create-datacontext-methods-that-call-stored-procedures-and-functions"></a>Criar métodos DataContext que chamam procedimentos e funções armazenados

Você pode criar <xref:System.Data.Linq.DataContext> métodos que chamam (são mapeados para) procedimentos armazenados e funções arrastando-os de **Gerenciador de Servidores** ou **Gerenciador de banco de dados** para o o **/R Designer**. Os procedimentos armazenados e funções são adicionados ao o **/R Designer** como métodos do <xref:System.Data.Linq.DataContext> .

> [!NOTE]
> Quando você arrasta procedimentos armazenados e funções de **Gerenciador de servidores** ou **Gerenciador de banco de dados** para o o **/R Designer**, o tipo de retorno do <xref:System.Data.Linq.DataContext> método gerado difere dependendo de onde você solta o item. Para obter mais informações, consulte [métodos DataContext (O/R Designer)](../data-tools/datacontext-methods-o-r-designer.md).

## <a name="configure-a-datacontext-to-use-stored-procedures-to-save-data-between-entity-classes-and-a-database"></a>Configurar um DataContext para usar procedimentos armazenados a fim de salvar dados entre classes de entidade e um banco de dados

Conforme observado anteriormente, você pode criar os métodos de <xref:System.Data.Linq.DataContext> que chamam procedimentos armazenados e funções. Além disso, você também pode atribuir procedimentos armazenados que são usados para o comportamento padrão LINQ to SQL tempo de execução, que executa inserções, atualizações e exclusões. Para obter mais informações, consulte [como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (O/R Designer)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md).

## <a name="inheritance-and-the-or-designer"></a>Herança e Designer Relacional de Objetos

Assim como outros objetos, LINQ to SQL classes podem usar a herança e serem derivadas de outras classes. Em uma base de dados, as relações de herança são criadas de várias maneiras. O o **/R Designer** dá suporte ao conceito de herança de tabela única, pois ela geralmente é implementada em sistemas relacionais. Para obter mais informações, consulte [como: configurar a herança usando o o/R Designer](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md).

## <a name="linq-to-sql-queries"></a>Consultas do LINQ to SQL

As classes de entidade criadas pelo o **/R Designer** são projetadas para uso com [LINQ (consulta integrada à linguagem)](/dotnet/csharp/linq/). Para obter mais informações, consulte [como consultar informações](/dotnet/framework/data/adonet/sql/linq/how-to-query-for-information).

## <a name="separate-the-generated-datacontext-and-entity-class-code-into-different-namespaces"></a>Separar o DataContext gerado e o código de classe de entidade em namespaces diferentes

O o **/R Designer** fornece as propriedades de namespace de **contexto** e de **namespace de entidade** no <xref:System.Data.Linq.DataContext> . Essas propriedades que determinam o namespace <xref:System.Data.Linq.DataContext> e o código de classe de entidade são gerados. Por padrão, essas propriedades são vazios e <xref:System.Data.Linq.DataContext> e classes de entidade são gerados no namespace do aplicativo. Para gerar código em um namespace diferente do namespace do aplicativo, insira um valor nas propriedades do **Namespace do Contexto** e/ou do **Namespace da Entidade**.

## <a name="reference-content"></a>Conteúdo de referência

- <xref:System.Linq>
- <xref:System.Data.Linq>

## <a name="see-also"></a>Veja também

- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)
- [Perguntas frequentes (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/frequently-asked-questions)
