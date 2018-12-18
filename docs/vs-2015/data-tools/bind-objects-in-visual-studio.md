---
title: Associar objetos no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], object binding
- data [Visual Studio], binding to objects
- object binding
- binding, to objects
ms.assetid: ed743ce6-73af-45e5-a8ff-045eddaccc86
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: c832686cbe56bb9d2a3b9f31206dada8043e7b44
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49918630"
---
# <a name="bind-objects-in-visual-studio"></a>Associar objetos no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Visual Studio fornece ferramentas de tempo de design para trabalhar com objetos personalizados, como a fonte de dados em seu aplicativo. Quando você deseja armazenar os dados de um banco de dados em um objeto que você associa a controles de interface do usuário, a abordagem recomendada é usar o Entity Framework para gerar a classe ou classes. Entidade Frameworkautogenerates todo o código de controle de alterações de texto clichê, o que significa que todas as alterações aos objetos locais são persistidas no banco de dados quando você chamar AcceptChanges no objeto DbSet.    Para obter mais informações, consulte [documentação do Entity Framework](https://ef.readthedocs.org/en/latest/).  
  
> [!TIP]
>  As abordagens para associação de objeto neste artigo só devem ser consideradas se seu aplicativo já é baseado em conjuntos de dados. Essas abordagens também podem ser usadas se você já estiver familiarizado com conjuntos de dados e os dados que você processará são tabular e não muito complexa ou muito grande. Para obter um exemplo ainda mais simples, que envolve o carregamento de dados diretamente em objetos usando um DataReader e atualizar manualmente a interface do usuário sem associação de dados, consulte [criar um aplicativo de dados simples usando o ADO.NET](../data-tools/create-a-simple-data-application-by-using-adonet.md).  
  
## <a name="object-requirements"></a>Requisitos de objeto  
 O único requisito para objetos personalizados para trabalhar com os dados de ferramentas de design no Visual Studio é que o objeto precisa de pelo menos uma propriedade pública.  
  
 Em geral, objetos personalizados não exigem qualquer interfaces específicas, construtores ou atributos para atuar como uma fonte de dados para um aplicativo. No entanto, se você deseja arrastar o objeto a partir de **fontes de dados** janela para uma superfície de design para criar um controle associado a dados, e se o objeto implementa a <xref:System.ComponentModel.ITypedList> ou <xref:System.ComponentModel.IListSource> interface, o objeto deve ter um padrão construtor. Caso contrário, o Visual Studio não é possível instanciar o objeto de fonte de dados, e ele exibirá um erro quando você arrasta o item para a superfície de design.  
  
## <a name="examples-of-using-custom-objects-as-data-sources"></a>Exemplos de como usar objetos personalizados como fontes de dados  
 Embora existam inúmeras maneiras de implementar a lógica do aplicativo ao trabalhar com objetos como uma fonte de dados, para o SQL há bancos de dados são algumas operações padrão que podem ser simplificadas usando os objetos TableAdapter gerados do Visual Studio. Esta página explica como implementar esses processos padrão usar TableAdapters.It não destina-se como um guia para a criação de seus objetos personalizados. Por exemplo, normalmente você executará as seguintes operações padrão independentemente da implementação específica de seus objetos, ou lógica do aplicativo:  
  
-   Carregando dados em objetos (normalmente de um banco de dados).  
  
-   Criando uma coleção tipada de objetos.  
  
-   Adicionando objetos a serem e remoção de uma coleção de objetos.  
  
-   Exibindo os dados de objeto para os usuários em um formulário.  
  
-   Alterando/edição de dados em um objeto.  
  
-   Salvar dados de objetos no banco de dados.  
  
> [!NOTE]
>  Para entender melhor e fornecer contexto para os exemplos nesta página, sugerimos que você conclua o seguinte: [instruções passo a passo: conectando a dados em objetos (Windows Forms)](http://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05). Essa explicação passo a passo cria os objetos discutidos aqui.  
  
### <a name="loaddata-into-objects"></a>LoadData em objetos  
 Neste exemplo, você carrega dados em seus objetos usando TableAdapters. Por padrão, os TableAdapters são criados com dois tipos de métodos que buscam dados de um banco de dados e popular tabelas de dados.  
  
- O `TableAdapter.Fill` método preenche uma tabela de dados existente com os dados retornados.  
  
- O `TableAdapter.GetData` método retorna uma nova tabela de dados preenchida com dados.  
  
  A maneira mais fácil de carregar os objetos personalizados com dados é chamar o `TableAdapter.GetData` método, um loop através da coleção de linhas na tabela de dados retornados e preencher cada objeto com os valores em cada linha. Você pode criar um `GetData` método que retorna uma tabela de dados preenchida para qualquer consulta adicionada a um TableAdapter.  
  
> [!NOTE]
>  Visual Studio nomeia as consultas TableAdapter `Fill` e `GetData` por padrão, mas esses nomes podem ser alterados a qualquer nome de método válido.  
  
 O exemplo a seguir mostra como executar um loop pelas linhas em uma tabela de dados e preencher um objeto com dados:  
  
 [!code-csharp[VbRaddataConnecting#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Form1.cs#4)]
 [!code-vb[VbRaddataConnecting#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Form1.vb#4)]  
  
### <a name="create-a-typed-collection-of-objects"></a>Criar uma coleção tipada de objetos  
 Você pode criar classes de coleção para os objetos ou usar as coleções de tipados que são fornecidas automaticamente pelo [componente BindingSource](http://msdn.microsoft.com/library/3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9).  
  
 Quando você estiver criando uma classe de coleção personalizada para objetos, sugerimos que você herdar de <xref:System.ComponentModel.BindingList%601>. Essa classe genérica fornece funcionalidade para administrar sua coleção, bem como a capacidade de gerar eventos que enviam notificações para a infra-estrutura de ligação de dados em formulários do Windows.  
  
 A coleção gerada automaticamente na <xref:System.Windows.Forms.BindingSource> usa um <xref:System.ComponentModel.BindingList%601> para sua coleção tipada. Se seu aplicativo não requer funcionalidade adicional, em seguida, você pode manter sua coleção dentro de <xref:System.Windows.Forms.BindingSource>. Para obter mais informações, consulte o <xref:System.Windows.Forms.BindingSource.List%2A> propriedade do <xref:System.Windows.Forms.BindingSource> classe.  
  
> [!NOTE]
>  Se sua coleção requer funcionalidade não fornecida pela implementação de base a <xref:System.ComponentModel.BindingList%601>, você deve criar uma coleção personalizada para que você possa adicionar à classe conforme necessário.  
  
 O código a seguir mostra como criar a classe para uma coleção fortemente tipada de `Order` objetos:  
  
 [!code-csharp[VbRaddataConnecting#8](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#8)]
 [!code-vb[VbRaddataConnecting#8](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#8)]  
  
### <a name="addobjects-to-a-collection"></a>Addobjects a uma coleção  
 Adicionar objetos a uma coleção chamando o `Add` método de sua classe de coleção personalizada ou do <xref:System.Windows.Forms.BindingSource>.  
  
 Para obter um exemplo de como adicionar a uma coleção usando um <xref:System.Windows.Forms.BindingSource>, consulte o `LoadCustomers` método na [passo a passo: conectando a dados em objetos (Windows Forms)](http://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05).  
  
 Para obter um exemplo de como adicionar objetos a uma coleção personalizada, consulte o `LoadOrders` método no [passo a passo: conectando a dados em objetos (Windows Forms)](http://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05).  
  
> [!NOTE]
>  O `Add` método é fornecido automaticamente para sua coleção personalizada quando você herda do <xref:System.ComponentModel.BindingList%601>.  
  
 O código a seguir mostra como adicionar objetos à coleção com tipo em um <xref:System.Windows.Forms.BindingSource>:  
  
 [!code-csharp[VbRaddataConnecting#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#5)]
 [!code-vb[VbRaddataConnecting#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#5)]  
  
 O código a seguir mostra como adicionar objetos a uma coleção tipada que herda de <xref:System.ComponentModel.BindingList%601>:  
  
> [!NOTE]
>  Neste exemplo o `Orders` coleção é uma propriedade do `Customer` objeto.  
  
 [!code-csharp[VbRaddataConnecting#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#6)]
 [!code-vb[VbRaddataConnecting#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#6)]  
  
### <a name="removeobjects-from-a-collection"></a>Removeobjects de uma coleção  
 Remover objetos de uma coleção chamando o `Remove` ou `RemoveAt` método de sua classe de coleção personalizada ou de <xref:System.Windows.Forms.BindingSource>.  
  
> [!NOTE]
>  O `Remove` e `RemoveAt` métodos são fornecidos automaticamente para sua coleção personalizada quando você herda do <xref:System.ComponentModel.BindingList%601>.  
  
 O código a seguir mostra como localizar e remover objetos de coleção tipada em uma <xref:System.Windows.Forms.BindingSource> com o <xref:System.Windows.Forms.BindingSource.RemoveAt%2A> método:  
  
 [!code-csharp[VbRaddataConnecting#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#7)]
 [!code-vb[VbRaddataConnecting#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#7)]  
  
### <a name="displayobject-data-to-users"></a>Dados DisplayObject para os usuários  
 Para exibir os dados em objetos para usuários, crie uma fonte de dados de objeto usando o **Data Source Configuration** assistente e, em seguida, arraste o objeto inteiro ou propriedades individuais para seu formulário do **fontes de dados**janela.  
  
### <a name="modify-the-data-in-objects"></a>Modificar os dados em objetos  
 Para editar dados em objetos personalizados que são associados a dados para controles dos Windows Forms, basta edite os dados no controle associado (ou diretamente nas propriedades do objeto). Arquitetura de vinculação de dados atualiza os dados no objeto.  
  
 Se seu aplicativo exigir o rastreamento de alterações e a reversão alterações propostas para seus valores originais, você deve implementar essa funcionalidade em seu modelo de objeto. Para obter exemplos de como tabelas de dados manter controle de alterações propostas, consulte <xref:System.Data.DataRowState>, <xref:System.Data.DataSet.HasChanges%2A>, e <xref:System.Data.DataTable.GetChanges%2A>.  
  
### <a name="savedata-in-objects-back-to-the-database"></a>SaveData nos objetos no banco de dados  
 Salve dados no banco de dados, passando os valores de seu objeto para métodos DBDirect do TableAdapter.  
  
 O Visual Studio cria métodos DBDirect que podem ser executados diretamente no banco de dados. Esses métodos não requerem objetos DataSet ou DataTable.  
  
|Método TableAdapter DBDirect|Descrição|  
|----------------------------------|-----------------|  
|`TableAdapter.Insert`|Adiciona novos registros para um banco de dados, permitindo que você passe valores de colunas individuais como parâmetros de método.|  
|`TableAdapter.Update`|Atualizações de registros existentes em um banco de dados. O método de atualização usa valores da coluna original e novo como parâmetros de método. Os valores originais são usados para localizar o registro original e os novos valores são usados para atualizar esse registro.<br /><br /> O `TableAdapter.Update` método também é usado para acomodar as alterações em um conjunto de dados no banco de dados, fazendo uma <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, <xref:System.Data.DataRow>, ou uma matriz de <xref:System.Data.DataRow>s como parâmetros de método.|  
|`TableAdapter.Delete`|Exclui registros existentes do banco de dados com base em valores da coluna original passados como parâmetros de método.|  
  
 Para salvar dados de uma coleção de objetos, executar um loop através da coleção de objetos (por exemplo, usando um loop for-next). Envie os valores para cada objeto no banco de dados usando os métodos DBDirect do TableAdapter.  
  
 O exemplo a seguir mostra como usar o `TableAdapter.Insert` DBDirect de método para adicionar um novo cliente diretamente ao banco de dados:  
  
 [!code-csharp[VbRaddataSaving#23](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#23)]
 [!code-vb[VbRaddataSaving#23](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#23)]  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)

