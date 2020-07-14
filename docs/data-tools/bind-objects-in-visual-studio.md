---
title: Objetos personalizados de associação de dados
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], object binding
- data [Visual Studio], binding to objects
- object binding
- binding, to objects
ms.assetid: ed743ce6-73af-45e5-a8ff-045eddaccc86
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: a1d72ed179324b8ab7682e485fbaaf8f34b25cd4
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282924"
---
# <a name="bind-objects-as-data-sources-in-visual-studio"></a>Associar objetos como fontes de dados no Visual Studio

O Visual Studio fornece ferramentas de tempo de design para trabalhar com objetos personalizados como a fonte de dados em seu aplicativo. Quando você deseja armazenar dados de um banco de dado em um objeto que você associa aos controles da interface do usuário, a abordagem recomendada é usar Entity Framework para gerar a classe ou classes. Entity Framework gera automaticamente todo o código de controle de alterações clichê, o que significa que qualquer alteração nos objetos locais é persistida automaticamente no banco de dados quando você chama AcceptChanges no objeto DbSet. Para obter mais informações, consulte a [documentação do Entity Framework](https://ef.readthedocs.org/en/latest/).

> [!TIP]
> As abordagens para a associação de objetos neste artigo só devem ser consideradas se o seu aplicativo já estiver baseado em conjuntos de aplicativos. Você também pode usar essas abordagens se já estiver familiarizado com conjuntos de dados, e se você estiver processando a tabela, e não muito complexa ou muito grande. Para um exemplo ainda mais simples, envolvendo carregar dados diretamente em objetos usando um DataReader e atualizar manualmente a interface do usuário sem DataBinding, consulte [criar um aplicativo de dados simples usando ADO.net](../data-tools/create-a-simple-data-application-by-using-adonet.md).

## <a name="object-requirements"></a>Requisitos de objeto

O único requisito para os objetos personalizados trabalharem com as ferramentas de design de dados no Visual Studio é que o objeto precisa de pelo menos uma propriedade pública.

Em geral, os objetos personalizados não exigem interfaces, construtores ou atributos específicos para atuar como uma fonte de dados para um aplicativo. No entanto, se você quiser arrastar o objeto da janela **fontes de dados** para uma superfície de design para criar um controle vinculado a dados e se o objeto implementar a <xref:System.ComponentModel.ITypedList> interface ou <xref:System.ComponentModel.IListSource> , o objeto deverá ter um construtor padrão. Caso contrário, o Visual Studio não pode instanciar o objeto de fonte de dados e ele exibirá um erro quando você arrastar o item para a superfície de design.

## <a name="examples-of-using-custom-objects-as-data-sources"></a>Exemplos de como usar objetos personalizados como fontes de dados

Embora existam inúmeras maneiras de implementar a lógica do aplicativo ao trabalhar com objetos como uma fonte de dados, para bancos de dado SQL, há algumas operações padrão que podem ser simplificadas usando os objetos TableAdapter gerados pelo Visual Studio. Esta página explica como implementar esses processos padrão usando TableAdapters. Ele não se destina como um guia para a criação de seus objetos personalizados. Por exemplo, normalmente você executará as seguintes operações padrão, independentemente da implementação específica de seus objetos, ou da lógica do aplicativo:

- Carregar dados em objetos (normalmente de um banco de dados).

- Criando uma coleção de objetos tipada.

- Adicionando objetos a e removendo objetos de uma coleção.

- Exibindo os dados do objeto para os usuários em um formulário.

- Alterar/editar os dados em um objeto.

- Salvando dados de objetos de volta para o Database.

### <a name="load-data-into-objects"></a>Carregar dados em objetos

Para este exemplo, você carrega dados em seus objetos usando TableAdapters. Por padrão, os TableAdapters são criados com dois tipos de métodos que buscam dados de um banco de dados e populam tabelas.

- O `TableAdapter.Fill` método preenche uma tabela de dados existente com os dados retornados.

- O `TableAdapter.GetData` método retorna uma nova tabela de dados populada com dados.

A maneira mais fácil de carregar objetos personalizados com dados é chamar o `TableAdapter.GetData` método, executar um loop através da coleção de linhas na tabela de dados retornada e preencher cada objeto com os valores de cada linha. Você pode criar um `GetData` método que retorna uma tabela de dados preenchida para qualquer consulta adicionada a um TableAdapter.

> [!NOTE]
> O Visual Studio nomeia as consultas do TableAdapter `Fill` e, `GetData` por padrão, mas você pode alterar esses nomes para qualquer nome de método válido.

O exemplo a seguir mostra como executar um loop pelas linhas em uma tabela de dados e preencher um objeto com dados:

[!code-csharp[VbRaddataConnecting#4](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_1.cs)]
[!code-vb[VbRaddataConnecting#4](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_1.vb)]

### <a name="create-a-typed-collection-of-objects"></a>Criar uma coleção de objetos tipada

Você pode criar classes de coleção para seus objetos ou usar as coleções tipadas que são fornecidas automaticamente pelo [componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component).

Quando você estiver criando uma classe de coleção personalizada para objetos, sugerimos que você herde de <xref:System.ComponentModel.BindingList%601> . Essa classe genérica fornece funcionalidade para administrar sua coleção, bem como a capacidade de gerar eventos que enviam notificações para a infraestrutura de ligação de dados no Windows Forms.

A coleção gerada automaticamente no <xref:System.Windows.Forms.BindingSource> usa um <xref:System.ComponentModel.BindingList%601> para sua coleção tipada. Se seu aplicativo não exigir funcionalidade adicional, você poderá manter sua coleção dentro do <xref:System.Windows.Forms.BindingSource> . Para obter mais informações, consulte a <xref:System.Windows.Forms.BindingSource.List%2A> propriedade da <xref:System.Windows.Forms.BindingSource> classe.

> [!NOTE]
> Se sua coleção exigir funcionalidade não fornecida pela implementação base do <xref:System.ComponentModel.BindingList%601> , você deverá criar uma coleção personalizada para que possa adicionar à classe conforme necessário.

O código a seguir mostra como criar a classe para uma coleção de objetos fortemente tipada `Order` :

[!code-csharp[VbRaddataConnecting#8](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_2.cs)]
[!code-vb[VbRaddataConnecting#8](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_2.vb)]

### <a name="add-objects-to-a-collection"></a>Adicionar objetos a uma coleção

Você adiciona objetos a uma coleção chamando o `Add` método da sua classe de coleção personalizada ou do <xref:System.Windows.Forms.BindingSource> .

> [!NOTE]
> O `Add` método é fornecido automaticamente para sua coleção personalizada quando você herda de <xref:System.ComponentModel.BindingList%601> .

O código a seguir mostra como adicionar objetos à coleção tipada em um <xref:System.Windows.Forms.BindingSource> :

[!code-csharp[VbRaddataConnecting#5](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_3.cs)]
[!code-vb[VbRaddataConnecting#5](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_3.vb)]

O código a seguir mostra como adicionar objetos a uma coleção tipada que herda de <xref:System.ComponentModel.BindingList%601> :

> [!NOTE]
> Neste exemplo, a `Orders` coleção é uma propriedade do `Customer` objeto.

[!code-csharp[VbRaddataConnecting#6](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_4.cs)]
[!code-vb[VbRaddataConnecting#6](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_4.vb)]

### <a name="remove-objects-from-a-collection"></a>Remover objetos de uma coleção

Você remove objetos de uma coleção chamando o `Remove` método ou `RemoveAt` da sua classe de coleção personalizada ou do <xref:System.Windows.Forms.BindingSource> .

> [!NOTE]
> Os `Remove` `RemoveAt` métodos e são fornecidos automaticamente para sua coleção personalizada quando você herda de <xref:System.ComponentModel.BindingList%601> .

O código a seguir mostra como localizar e remover objetos da coleção tipada em um <xref:System.Windows.Forms.BindingSource> com o <xref:System.Windows.Forms.BindingSource.RemoveAt%2A> método:

[!code-csharp[VbRaddataConnecting#7](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_5.cs)]
[!code-vb[VbRaddataConnecting#7](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_5.vb)]

### <a name="display-object-data-to-users"></a>Exibir dados de objeto para usuários

Para exibir os dados em objetos para os usuários, crie uma fonte de dados de objeto usando o assistente de **configuração de fonte de dados** e, em seguida, arraste o objeto inteiro ou as propriedades individuais para o formulário na janela fontes de **dados** .

### <a name="modify-the-data-in-objects"></a>Modificar os dados em objetos

Para editar dados em objetos personalizados que são associados a dados a controles Windows Forms, basta editar os dados no controle ligado (ou diretamente nas propriedades do objeto). A arquitetura de vinculação de dados atualiza os dados no objeto.

Se seu aplicativo exigir o acompanhamento de alterações e a reversão de alterações propostas para seus valores originais, você deverá implementar essa funcionalidade em seu modelo de objeto. Para obter exemplos de como as tabelas de dados acompanham as alterações propostas, consulte <xref:System.Data.DataRowState> , <xref:System.Data.DataSet.HasChanges%2A> e <xref:System.Data.DataTable.GetChanges%2A> .

### <a name="save-data-in-objects-back-to-the-database"></a>Salvar dados em objetos de volta no banco de dado

Salve os dados de volta no banco de dado passando os valores de seu objeto para os métodos DBDirect do TableAdapter.

O Visual Studio cria métodos DBDirect que podem ser executados diretamente no banco de dados. Esses métodos não exigem objetos DataSet ou DataTable.

|Métodos DBDirect TableAdapter|Descrição|
| - |-----------------|
|`TableAdapter.Insert`|Adiciona novos registros a um banco de dados, permitindo que você transmita valores de coluna individuais como parâmetros de método.|
|`TableAdapter.Update`|Atualiza os registros existentes em um banco de dados. O método Update usa valores originais e novos de coluna como parâmetros de método. Os valores originais são usados para localizar o registro original e os novos valores são usados para atualizar esse registro.<br /><br /> O `TableAdapter.Update` método também é usado para reconciliar as alterações em um conjunto de dados de volta para o Database, por meio de uma <xref:System.Data.DataSet> <xref:System.Data.DataTable> matriz,, <xref:System.Data.DataRow> ou de <xref:System.Data.DataRow> s como parâmetros de método.|
|`TableAdapter.Delete`|Exclui os registros existentes do banco de dados com base nos valores de coluna originais passados como parâmetros de método.|

Para salvar dados de uma coleção de objetos, faça um loop através da coleção de objetos (por exemplo, usando um loop for-Next). Envie os valores para cada objeto para o banco de dados usando os métodos DBDirect do TableAdapter.

O exemplo a seguir mostra como usar o `TableAdapter.Insert` Método DBDirect para adicionar um novo cliente diretamente ao banco de dados:

[!code-csharp[VbRaddataSaving#23](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_6.cs)]
[!code-vb[VbRaddataSaving#23](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_6.vb)]

## <a name="see-also"></a>Veja também

- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
