---
title: Editando TableAdapters | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.datasource.dbtablefunctionwizard
- vs.datasource.datacomponentquerywizard
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], data component queries
- data [Visual Studio], TableAdapters
- TableAdapter Query Configuration Wizard
- data [Visual Studio], table adapter queries
ms.assetid: 8c06b306-24d0-4521-948d-07e3b7badd95
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: b242f8154f31391d168f2a41bfd00c01f037d87e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49877641"
---
# <a name="editing-tableadapters"></a>Editando TableAdapters
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Às vezes, você talvez queira alterar o esquema de tabela do adaptador. Para fazer isso, você modifica o primário do adaptador `Fill` método. TableAdapters são criados com um principal `Fill` método que define o esquema da tabela de dados associado. Principal `Fill` método se baseia na consulta ou procedimento armazenado que você inseriu quando configurou o TableAdapter originalmente; é o primeiro método (superior) sob a tabela de dados sobre o [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md).  
  
 ![TableAdapter com várias consultas](../data-tools/media/tableadapter.gif "TableAdapter")  
  
 As alterações que fizer ao TableAdapter principal do `Fill` método são refletidas no esquema da tabela de dados associado. Por exemplo, remover uma coluna da consulta no principal `Fill` método também remove a coluna da tabela de dados associado. Além disso, remover a coluna da principal `Fill` método remove a coluna de quaisquer consultas adicionais para aquele TableAdapter.  
  
 Você pode usar o **Assistente de configuração de consulta do TableAdapter** para criar e editar consultas adicionais para o TableAdapter. Essas consultas adicionais devem estar em conformidade com o esquema da tabela, a menos que elas retornam um valor escalar.  As consultas adicionais que têm um nome que você especificar (por exemplo, `CustomersTableAdapter.FillByCity(NorthwindDataSet.Customers, "Seattle")`.)  
  
#### <a name="to-start-the-tableadapter-query-configuration-wizard-with-a-new-query"></a>Para iniciar o Assistente de configuração de consulta do TableAdapter com uma nova consulta  
  
1.  Abra o dataset na **Dataset Designer**.  
  
2.  Se você estiver criando uma nova consulta, arraste um **consulta** do objeto da **DataSet** guia da **caixa de ferramentas** em um <xref:System.Data.DataTable>, ou selecione **Add Query**no menu de atalho do TableAdapter. Você também pode arrastar uma **consulta** objeto em uma área vazia do **Dataset Designer**, que cria um TableAdapter sem um associado <xref:System.Data.DataTable>. Essas consultas são limitadas a retornar valores únicos (escalares) ou executar UPDATE, INSERT, ou exclua comandos no banco de dados. Para obter mais informações, consulte [como: adicionar consultas globais a um TableAdapter](../data-tools/how-to-add-global-queries-to-a-tableadapter.md).  
  
3.  Sobre o **escolha sua Conexão de dados** página, selecione ou crie a conexão usará a consulta.  
  
    > [!NOTE]
    >  Esta página só aparece quando o designer não pode determinar a conexão apropriada para usar, ou quando não há conexões disponíveis.  
  
4.  Sobre o **escolher um tipo de comando** página, selecione os seguintes métodos de busca de dados do banco de dados:  
  
    -   **Usar instruções SQL** permite que você digite uma instrução SQL para selecionar os dados de seu banco de dados.  
  
    -   **Criar novo procedimento armazenado** — Selecione esta opção para que o Assistente para criar um novo procedimento armazenado com base na instrução SELECT especificada (no banco de dados).  
  
    -   **Use os procedimentos armazenados existentes** — Selecione esta opção para executar um procedimento armazenado existente quando executar a consulta.  
  
#### <a name="to-start-the-tableadapter-query-configuration-wizard-on-an-existing-query"></a>Para iniciar o Assistente de configuração de consulta do TableAdapter em uma consulta existente  
  
-   Se você estiver editando uma consulta TableAdapter existente, a consulta com o botão direito e escolha **configurar** no menu de atalho.  
  
    > [!NOTE]
    >  Clicando duas vezes na consulta principal de um TableAdapter reconfigura o TableAdapter e <xref:System.Data.DataTable> esquema, enquanto o botão direito do mouse uma consulta adicional em um TableAdapter configura a consulta selecionada. O **Assistente de configuração TableAdapter** reconfigura a definição do TableAdapter; o **Assistente de configuração de consulta do TableAdapter** reconfigura apenas a consulta selecionada.  
  
## <a name="running-the-wizard"></a>Executando o assistente  
 Arraste consultas para o **Dataset Designer**, ou configure consultas existentes (qualquer consulta listada abaixo da primeira consulta).  
  
 A primeira consulta em um TableAdapter é a consulta principal do TableAdapter. Editar esta consulta principal abre o **Assistente de configuração TableAdapter** e edita o esquema da tabela de dados do TableAdapter. Todas as consultas listadas abaixo da consulta principal são consultas adicionais e são configuradas usando o **Assistente de configuração de consulta do TableAdapter**. Para obter mais informações sobre como executar o assistente, consulte [como: iniciar o Assistente de configuração de consulta do TableAdapter](http://msdn.microsoft.com/library/fc7b468e-3417-48a4-a8aa-cace8f99c24a).  
  
## <a name="choose-your-data-connection"></a>Escolha a Conexão de Dados  
 Escolha uma conexão existente na lista de conexões ou clique em **nova Conexão** para criar uma conexão ao banco de dados.  
  
 Após a conclusão do **propriedades de Conexão** caixa de diálogo, o **os detalhes de Conexão** área exibe informações somente leitura sobre o provedor selecionado, bem como a cadeia de caracteres de conexão.  
  
## <a name="save-the-connection-string-to-the-application-configuration-file"></a>Salvar a cadeia de conexão no arquivo de configuração do aplicativo  
 Escolher **Sim, salvar a conexão como** para armazenar a cadeia de conexão no arquivo de configuração do aplicativo. Digite um nome para a conexão ou use o nome padrão fornecido.  
  
 Salvar cadeias de caracteres de conexão no arquivo de configuração do aplicativo simplifica o processo de manutenção do aplicativo se a conexão com o banco de dados for alterada. Em caso de alteração na conexão com o banco de dados, é possível editar a cadeia de caracteres de conexão no arquivo de configuração do aplicativo. Dessa maneira, não será necessário editar o código-fonte e recompilar o aplicativo. Para obter informações sobre como editar uma cadeia de caracteres de conexão no arquivo de configuração do aplicativo, consulte [como: salvar e editar cadeias de caracteres de Conexão](~/E:/Repos/visualstudio-docs-pr/docs/data-tools/how-to-save-and-edit-connection-strings.md).  
  
> [!IMPORTANT]
>  As informações são armazenadas no arquivo de configuração do aplicativo como texto simples. Para reduzir a possibilidade de acesso não autorizado a informações confidenciais, é possível criptografar os dados. Para obter mais informações, consulte [criptografando e descriptografando dados](http://msdn.microsoft.com/en-us/22812ae8-e082-4eb1-a29b-21b6ee00c6b5).  
  
## <a name="use-sql-statements"></a>Usar Instruções SQL  
 Esta seção explica como concluir o **Assistente de configuração de consulta do TableAdapter** ao selecionar o **usar instruções SQL** opção.  
  
## <a name="choose-a-query-type"></a>Escolha um Tipo de Consulta  
 O assistente cria vários tipos de consultas dependendo dos requisitos do aplicativo. É possível escolher consultas SELECT que retornam linhas de dados (uma tabela de dados) ou consultas SELECT que retornam um valor escalar (um único valor como `Count` ou `Sum`).  
  
 Sobre o **escolher um tipo de consulta** , selecione o tipo de consulta para criar a partir da lista de consultas disponíveis.  
  
> [!NOTE]
>  Criar uma instrução INSERT, UPDATE ou DELETE não substitui os comandos do TableAdapter que são usados ao chamar o método `Update` do TableAdapter. Por exemplo, selecionar UPDATE como tipo de consulta criará uma nova consulta com um nome especificado posteriormente no assistente. Essa consulta é executada ao chamar esse método nomeado do TableAdapter. Chamar o método `Update` de um TableAdapter executará instruções criadas quando o TableAdapter original foi configurado.  
  
## <a name="specify-a-sql-query-type-statement"></a>Especificar um SQL \<tipo de consulta > instrução  
 Sobre o **especificar uma instrução SQL** página, digite a instrução SQL para executar ao chamar a consulta.  
  
> [!TIP]
>  O assistente fornece acesso para o **construtor de consultas**, uma ferramenta visual para criar consultas SQL. Para abri-lo, clique no **construtor de consultas** botão.  
  
## <a name="choose-methods-to-generate"></a>Escolha Métodos para Gerar  
 Esta página fornece opções para selecionar quais métodos o assistente gera para a consulta.  
  
 **Preencher uma DataTable**  
 Cria um método para preencher a tabela de dados. O nome da tabela de dados é passado como um parâmetro ao chamar esse método para preencher a tabela de dados com os dados retornados.  
  
 Opcionalmente, você pode alterar o nome padrão no **nome do método** caixa. Pode ser útil fornecer um nome significativo ao trabalhar com essa consulta em código.  
  
 **Retornar uma DataTable**  
 Cria um método para retornar uma tabela de dados preenchida. Em determinados aplicativos, pode ser mais vantajoso retornar uma tabela de dados preenchida ao invés de preencher a tabela de dados existente com dados.  
  
 Opcionalmente, você pode alterar o nome padrão no **nome do método** caixa.  
  
## <a name="choose-function-name"></a>Escolha o Nome da Função  
 Digite um nome para a função. Criar uma consulta do TableAdapter adiciona um método ao TableAdapter com o nome fornecido aqui. Chame esse método para executar a consulta. É útil fornecer um nome significativo ao trabalhar com essa consulta em código.  
  
> [!NOTE]
>  Ao criar novos procedimentos armazenados, são solicitados dois nomes. O primeiro nome é o nome do procedimento armazenado criado no banco de dados; o segundo nome é o nome do método no TableAdapter que executa o procedimento armazenado quando chamado.  
  
## <a name="create-new-stored-procedures"></a>Criar novos procedimentos armazenados  
 Esta seção explica como concluir o **Assistente de configuração de consulta do TableAdapter** ao selecionar o **criar novos procedimentos armazenados** opção.  
  
1. No **gerar os procedimentos armazenados** página, digite a instrução SQL para executar ao chamar o procedimento armazenado.  
  
   > [!NOTE]
   >  O assistente fornece acesso para o **construtor de consultas**, uma ferramenta visual para criar consultas SQL. Para abri-lo, clique no **construtor de consultas** botão.  
  
2. No **criar os procedimentos armazenados** página, faça o seguinte:  
  
   1. Digite um nome para o novo procedimento armazenado.  
  
   2. Especifique se o procedimento armazenado será criado no banco de dados subjacente.  
  
      > [!NOTE]
      >  A capacidade de criar um procedimento armazenado no banco de dados é determinada pelas configurações de segurança do banco de dados específico.  
  
      O **visualizar resultados do assistente** página mostra os resultados de criar a consulta do TableAdapter. Se o assistente encontrar problemas, esta página fornecerá as informações sobre o erro.  
  
## <a name="use-existing-stored-procedures"></a>Usar procedimentos armazenados existentes  
 Esta seção explica como concluir o **Assistente de configuração de consulta do TableAdapter** ao selecionar o **usar procedimentos armazenados existentes** opção.  
  
1.  Selecione um procedimento armazenado existente na lista suspensa na **escolha um procedimento armazenado existente** página do assistente.  
  
     O **parâmetros** e **resultados** para armazenados selecionado procedimento são exibidos para referência.  
  
2.  Clique em **Avançar**.  
  
## <a name="choose-the-shape-of-data-returned-by-the-stored-procedure"></a>Escolha o formato dos dados retornados pelo procedimento armazenado  
 O tipo dos dados retornados pelo procedimento armazenado selecionado determina como o assistente cria os métodos do TableAdapter.  
  
 Selecione o tipo dos dados retornados por esta consulta.  
  
-   Selecionando **dados tabulares** abre os **escolha métodos para gerar** página (descrita anteriormente nesta página Ajuda), que permite que você especifique os tipos de métodos, nomes de método e suporte a paginação a ser criado.  
  
-   Selecionando **um único valor** cria um método que retorna um único valor digitado. Essa opção abre o **Escolher nome de função** página (descrita anteriormente nesta página Ajuda).  
  
-   Selecionando **nenhum valor** cria um método tipado que executa o procedimento armazenado e não espera nenhum dado a ser retornado. Essa opção abre o **Escolher nome de função** página (descrita anteriormente nesta página Ajuda).  
  
## <a name="view-wizards-results"></a>Visualizar resultados do Assistente  
 O **visualizar resultados do assistente** página mostra os resultados de criar a consulta do TableAdapter. Se o assistente encontrar problemas, os detalhes serão exibidos nesta página.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Como: editar consultas TableAdapter](../data-tools/how-to-edit-tableadapter-queries.md)   
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Visão geral de aplicativos de dados no Visual Studio](../data-tools/overview-of-data-applications-in-visual-studio.md)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)