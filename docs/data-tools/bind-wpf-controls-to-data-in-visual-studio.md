---
title: Associar controles WPF a dados-parte 1
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: e05a1e0c-5082-479d-bbc9-d395b0bc6580
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 27d0c14bcf09a3b0d30cd23dea0f8348c45fcab7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282875"
---
# <a name="bind-wpf-controls-to-data-in-visual-studio"></a>Associar controles WPF a dados no Visual Studio

É possível exibir dados para usuários do aplicativo associando-se dados a controles [!INCLUDE[TLA#tla_titlewinclient](../data-tools/includes/tlasharptla_titlewinclient_md.md)]. Para criar esses controles associados a dados, você pode arrastar itens da janela **fontes de dados** para o [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)] no Visual Studio. Este tópico descreve algumas das tarefas, ferramentas e classes mais comuns que é possível usar para criar aplicativos [!INCLUDE[TLA#tla_titlewinclient](../data-tools/includes/tlasharptla_titlewinclient_md.md)] de associação de dados.

Para obter informações gerais sobre como criar controles vinculados a dados no Visual Studio, consulte [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md). Para obter mais informações sobre [!INCLUDE[TLA#tla_titlewinclient](../data-tools/includes/tlasharptla_titlewinclient_md.md)] Associação de dados, consulte [visão geral da ligação de dados](/dotnet/desktop-wpf/data/data-binding-overview).

## <a name="tasks-involved-in-binding-wpf-controls-to-data"></a>Tarefas envolvidas na associação de controles WPF a dados

A tabela a seguir lista as tarefas que podem ser realizadas arrastando-se itens da janela **Fontes de Dados** para o [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)].

|Tarefa|Mais informações|
|----------| - |
|Crie novos controles de associação de dados.<br /><br /> Associe controles existentes a dados.|[Associar controles do WPF a um conjunto de dados](../data-tools/bind-wpf-controls-to-a-dataset.md)|
|Crie controles que exibam dados relacionados em uma relação pai-filho: quando o usuário seleciona um registro de dados pai em um controle, outro controle exibe dados filho relacionados ao registro selecionado.|[Exibir dados relacionados em aplicativos WPF](../data-tools/display-related-data-in-wpf-applications.md)|
|Crie uma *tabela de pesquisa* que exiba informações de uma tabela com base no valor de um campo de chave estrangeira em outra tabela.|[Criar tabelas de pesquisa em aplicativos do WPF](../data-tools/create-lookup-tables-in-wpf-applications.md)|
|Associe um controle a uma imagem em um banco de dados.|[Associar controles a imagens de um banco de dados](../data-tools/bind-controls-to-pictures-from-a-database.md)|

## <a name="valid-drop-targets"></a>Reproduções automáticas válidas

É possível arrastar itens na janela **Fontes de Dados** apenas para reproduções automáticas válidas no [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)]. Existem dois tipos principais de destinos depósitos válidos: contêineres e controles. Um contêiner é um elemento de interface do usuário que normalmente contém controles. Por exemplo, uma grade é um contêiner, assim como uma janela.

## <a name="generated-xaml-and-code"></a>XAML e código gerados

Quando você arrasta um item da janela **fontes de dados** para o [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)] , o Visual Studio gera [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] que define um novo controle vinculado a dados (ou associa um controle existente à fonte de dados). Para algumas fontes de dados, o Visual Studio também gera código no arquivo code-behind que preenche a fonte de dados com dados.

A tabela a seguir lista o [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] e o código que o Visual Studio gera para cada tipo de fonte de dados na janela **fontes de dados** .

| Fonte de dados | Gerar XAML que associa um controle à fonte de dados | Gerar código que preenche a fonte de dados com dados |
| - | - | - |
| Dataset | Sim | Sim |
| [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] | Sim | Sim |
| Serviço | Sim | Não |
| Objeto | Sim | Não |

### <a name="datasets"></a>Conjunto de dados

Quando você arrasta uma tabela ou coluna da janela **fontes de dados** para o designer, o Visual Studio gera [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] o seguinte:

- Adiciona o conjunto de dados e um novo <xref:System.Windows.Data.CollectionViewSource> aos recursos do contêiner arrastados para o item. O <xref:System.Windows.Data.CollectionViewSource> é um objeto que pode ser usado para navegar e exibir os dados no conjunto de dados.

- Cria uma associação de dados para um controle. Se você arrastar o item para um controle existente no designer, o XAML associará o controle ao item. Se você arrastar o item para um contêiner, o XAML criará o controle que foi selecionado para o item arrastado e associará o controle ao item. O controle é criado dentro de um novo <xref:System.Windows.Controls.Grid>.

O Visual Studio também faz as seguintes alterações no arquivo code-behind:

- Cria um manipulador de eventos <xref:System.Windows.FrameworkElement.Loaded> para o elemento [!INCLUDE[TLA2#tla_ui](../data-tools/includes/tla2sharptla_ui_md.md)] que contém o controle. O manipulador de eventos preenche a tabela com dados, recupera o <xref:System.Windows.Data.CollectionViewSource> dos recursos do contêiner e, em seguida, torna o primeiro item dados o item atual. Se um <xref:System.Windows.FrameworkElement.Loaded> manipulador de eventos já existir, o Visual Studio adicionará esse código ao manipulador de eventos existente.

### <a name="entity-data-models"></a>Modelos de dados de entidade

Quando você arrasta uma entidade ou uma propriedade de entidade da janela **fontes de dados** para o designer, o Visual Studio gera [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] o seguinte:

- Adiciona um novo <xref:System.Windows.Data.CollectionViewSource> aos recursos do contêiner arrastados para o item. O <xref:System.Windows.Data.CollectionViewSource> é um objeto que pode ser usado para navegar e exibir os dados na entidade.

- Cria uma associação de dados para um controle. Se você arrastar o item para um controle existente no designer, o [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] associará o controle ao item. Se você arrastar o item para um contêiner, o [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] criará o controle que foi selecionado para o item arrastado e associará o controle ao item. O controle é criado dentro de um novo <xref:System.Windows.Controls.Grid>.

O Visual Studio também faz as seguintes alterações no arquivo code-behind:

- Adiciona um novo método que retorna uma consulta para a entidade arrastada para o designer (ou a entidade que contém a propriedade que você arrastou para o designer). O novo método tem o nome `Get<EntityName>Query` , em que `\<EntityName>` é o nome da entidade.

- Cria um manipulador de eventos <xref:System.Windows.FrameworkElement.Loaded> para o elemento [!INCLUDE[TLA2#tla_ui](../data-tools/includes/tla2sharptla_ui_md.md)] que contém o controle. O manipulador de eventos chama o `Get<EntityName>Query` método para preencher a entidade com dados, recupera o <xref:System.Windows.Data.CollectionViewSource> dos recursos do contêiner e, em seguida, torna o primeiro item de dados o item atual. Se um <xref:System.Windows.FrameworkElement.Loaded> manipulador de eventos já existir, o Visual Studio adicionará esse código ao manipulador de eventos existente.

### <a name="services"></a>Serviços

Quando você arrasta um objeto de serviço ou uma propriedade da janela **fontes de dados** para o designer, o Visual Studio gera [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] que cria um controle vinculado a dados (ou associa um controle existente ao objeto ou à propriedade). No entanto, o Visual Studio não gera código que preenche o objeto de serviço de proxy com dados. Você deve gravar esse código sozinho. Para obter um exemplo que demonstra como fazer isso, consulte [associar controles WPF a um serviço de dados WCF](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md).

O Visual Studio gera XAML, que faz o seguinte:

- Adiciona um novo <xref:System.Windows.Data.CollectionViewSource> aos recursos do contêiner arrastados para o item. O <xref:System.Windows.Data.CollectionViewSource> é um objeto que pode ser usado para navegar e exibir os dados no objeto retornado pelo serviço.

- Cria uma associação de dados para um controle. Se você arrastar o item para um controle existente no designer, o [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] associará o controle ao item. Se você arrastar o item para um contêiner, o [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] criará o controle que foi selecionado para o item arrastado e associará o controle ao item. O controle é criado dentro de um novo <xref:System.Windows.Controls.Grid>.

### <a name="objects"></a>Objetos

Quando você arrasta um objeto ou uma propriedade da janela **fontes de dados** para o designer, o Visual Studio gera [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] que cria um controle associado a dados (ou associa um controle existente ao objeto ou à propriedade). No entanto, o Visual Studio não gera código para preencher o objeto com dados. Você deve gravar esse código sozinho.

> [!NOTE]
> As classes personalizadas devem ser públicas e, por padrão, têm um construtor sem parâmetros. Eles não podem ser classes aninhadas que tenham um "ponto" em sua sintaxe. Para obter mais informações, consulte [XAML e classes personalizadas para WPF](/dotnet/framework/wpf/advanced/xaml-and-custom-classes-for-wpf).

O Visual Studio gera [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] o seguinte:

- Adiciona um novo <xref:System.Windows.Data.CollectionViewSource> aos recursos do contêiner arrastados para o item. O <xref:System.Windows.Data.CollectionViewSource> é um objeto que pode ser usado para navegar e exibir os dados no objeto.

- Cria uma associação de dados para um controle. Se você arrastar o item para um controle existente no designer, o XAML associará o controle ao item. Se você arrastar o item para um contêiner, o XAML criará o controle que foi selecionado para o item arrastado e associará o controle ao item. O controle é criado dentro de um novo <xref:System.Windows.Controls.Grid>.

## <a name="see-also"></a>Veja também

- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
