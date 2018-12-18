---
title: Manipular uma exceção de simultaneidade | Microsoft Docs
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
- concurrency control, exceptions
- datasets [Visual Basic], errors
- exception handling, concurrency issues
- data concurrency, walkthroughs
- updating datasets, errors
- concurrency control, walkthroughs
ms.assetid: 73ee9759-0a90-48a9-bf7b-9d6fc17bff93
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: a3141f2480aabc2ce6aa7b10f99991fc5cba0d05
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220411"
---
# <a name="handle-a-concurrency-exception"></a>Tratar uma exceção de simultaneidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Exceções de simultaneidade (<xref:System.Data.DBConcurrencyException>) são acionados quando dois usuários tentam alterar os mesmos dados em um banco de dados ao mesmo tempo. Este passo a passo, você criará um aplicativo do Windows que ilustra como capturar uma <xref:System.Data.DBConcurrencyException>, localize a linha que causou o erro e Aprenda uma estratégia para como lidar com ele.  
  
 Este passo a passo leva você através do seguinte processo:  
  
1.  Criar um novo **aplicativo do Windows** projeto.  
  
2.  Criar um novo conjunto de dados com base em Northwind `Customers` tabela.  
  
3.  Criar um formulário com um <xref:System.Windows.Forms.DataGridView> para exibir os dados.  
  
4.  Preencher um conjunto de dados com os dados do `Customers` tabela no banco de dados Northwind.  
  
5.  Use o [Visual Database Tools](http://msdn.microsoft.com/en-us/6b145922-2f00-47db-befc-bf351b4809a1) no Visual Studio para acessar diretamente o `Customers` tabela de dados e alterar um registro.  
  
6.  Alterar o mesmo registro com um valor diferente, atualize o conjunto de dados e tentam gravar as alterações no banco de dados, o que resulta em um erro de simultaneidade que está sendo gerado.  
  
7.  Capturar o erro e, em seguida, exibir as diferentes versões do registro, permitindo que o usuário determinar se deseja continuar e atualizar o banco de dados, ou cancelar a atualização.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind com permissão para executar atualizações. Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
> [!NOTE]
>  As caixas de diálogo e comandos de menu que você vê podem diferir dos descritos na Ajuda, dependendo de suas configurações ativas ou a edição que você está usando. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="create-a-new-project"></a>Criar um novo projeto  
 Passo a passo você começa criando um novo aplicativo do Windows.  
  
#### <a name="to-create-a-new-windows-application-project"></a>Para criar um novo projeto de aplicativo do Windows  
  
1.  Sobre o **arquivo** menu, crie um novo projeto.  
  
2.  No **tipos de projeto** painel, selecione uma linguagem de programação.  
  
3.  No **modelos** painel, selecione **aplicativo do Windows**.  
  
4.  Nomeie o projeto `ConcurrencyWalkthrough`e, em seguida, selecione **Okey**.  
  
     O projeto para o Visual Studio adiciona **Gerenciador de soluções** e exibe um novo formulário no designer.  
  
## <a name="create-the-northwind-dataset"></a>Criar o conjunto de dados Northwind  
 Nesta seção, você criará um conjunto de dados denominado `NorthwindDataSet`.  
  
#### <a name="to-create-the-northwinddataset"></a>Para criar o NorthwindDataSet  
  
1.  Sobre o **dados** menu, escolha **fonte de adicionar novos dados**.  
  
     O [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f) é aberta.  
  
2.  Sobre o **escolher um tipo de fonte de dados**tela, selecione **banco de dados**.  
  
3.  Selecione uma conexão para o banco de dados de exemplo Northwind na lista de conexões disponíveis. Se a conexão não está disponível na lista de conexões, selecione**nova Conexão**  
  
    > [!NOTE]
    >  Se você estiver se conectando a um arquivo de banco de dados local, selecione **não** quando for perguntado se você preferir que você deseja adicionar o arquivo ao seu projeto.  
  
4.  Sobre o **salvar a cadeia de caracteres de conexão no arquivo de configuração de aplicativo**tela, selecione **próxima**.  
  
5.  Expanda o **tabelas** nó e selecione o `Customers` tabela. O nome padrão para o conjunto de dados deve ser `NorthwindDataSet`.  
  
6.  Selecione **concluir** para adicionar o conjunto de dados ao projeto.  
  
## <a name="create-a-data-bound-datagridview-control"></a>Criar um controle DataGridView de associação de dados  
 Nesta seção, você criará um <xref:System.Windows.Forms.DataGridView> arrastando a **clientes** do item dos **fontes de dados** janela para o formulário do Windows.  
  
#### <a name="to-create-a-datagridview-control-that-is-bound-to-the-customers-table"></a>Para criar um controle DataGridView que está associado à tabela clientes  
  
1.  Sobre o **dados** menu, escolha **Mostrar fontes de dados** para abrir o **janela fontes de dados**.  
  
2.  No **fontes de dados** janela, expanda o **NorthwindDataSet** nó e, em seguida, selecione o **clientes** tabela.  
  
3.  Selecione a seta para baixo no nó da tabela e, em seguida, selecione **DataGridView** na lista suspensa.  
  
4.  Arraste a tabela para uma área vazia do formulário.  
  
     Um <xref:System.Windows.Forms.DataGridView> controle chamado `CustomersDataGridView` e um <xref:System.Windows.Forms.BindingNavigator> denominado `CustomersBindingNavigator` são adicionados ao formulário que está associado a <xref:System.Windows.Forms.BindingSource>. É por isso, é por sua vez associado para o `Customers` na tabela a `NorthwindDataSet`.  
  
## <a name="test-the-form"></a>Testar o formulário  
 Agora você pode testar o formulário para certificar-se de que ele se comporta como esperado até este ponto.  
  
#### <a name="to-test-the-form"></a>Para testar o formulário  
  
1.  Selecione **F5** para executar o aplicativo  
  
     O formulário é exibido com um <xref:System.Windows.Forms.DataGridView> controle que é preenchido com dados do `Customers` tabela.  
  
2.  Sobre o **Debug** menu, selecione**parar depuração**.  
  
## <a name="handleconcurrency-errors"></a>Erros de Handleconcurrency  
 Como tratar erros é depende das regras de negócios específicas que regem seu aplicativo. Para este passo a passo, usamos a seguinte estratégia de exemplo para saber como tohandle o erro de simultaneidade.  
  
 O usuário com três versões do registro applicationpresents:  
  
- O registro atual no banco de dados  
  
- O registro original que é carregado no conjunto de dados  
  
- As alterações propostas no conjunto de dados  
  
  O usuário, em seguida, é capaz de substituir o banco de dados com a versão proposta, ou cancelar a atualização e atualizar o conjunto de dados com os novos valores do banco de dados.  
  
#### <a name="to-enable-the-handling-of-concurrency-errors"></a>Para habilitar o tratamento de erros de simultaneidade  
  
1.  Crie um manipulador de erro personalizada.  
  
2.  Exibir as opções para o usuário.  
  
3.  Processe a resposta do usuário.  
  
4.  Reenviar a atualização ou redefinir os dados no conjunto de dados.  
  
### <a name="addcode-to-handle-the-concurrency-exception"></a>Addcode para tratar a exceção de simultaneidade  
 Quando você tenta executar uma atualização e uma exceção é gerada, você geralmente deseja fazer algo com as informações que são fornecidas pela exceção gerada.  
  
 Nesta seção, você deve adicionar código que tenta atualizar o banco de dados. Você também lidar com qualquer <xref:System.Data.DBConcurrencyException> que pode ser gerada, bem como todas as outras exceções.  
  
> [!NOTE]
>  O `CreateMessage` e `ProcessDialogResults` métodos serão adicionados posteriormente neste passo a passo.  
  
##### <a name="to-add-error-handling-for-the-concurrency-error"></a>Para adicionar o tratamento de erro para o erro de simultaneidade  
  
1.  Adicione o seguinte código abaixo a `Form1_Load` método:  
  
     [!code-csharp[VbRaddataConcurrency#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#1)]
     [!code-vb[VbRaddataConcurrency#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#1)]  
  
2.  Substitua os `CustomersBindingNavigatorSaveItem_Click` método para chamar o `UpdateDatabase` método para que fique semelhante ao seguinte:  
  
     [!code-csharp[VbRaddataConcurrency#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#2)]
     [!code-vb[VbRaddataConcurrency#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#2)]  
  
### <a name="displaychoices-to-the-user"></a>Displaychoices ao usuário  
 O código que você acabou de escrever chama o `CreateMessage` procedimento para exibir informações de erro para o usuário. Para este passo a passo, você pode usar uma caixa de mensagem para exibir as diferentes versões do registro para o usuário. Isso permite que o usuário escolha se deseja substituir o registro com as alterações ou cancelar a edição. Depois que o usuário seleciona uma opção (clica em um botão) na caixa de mensagem, a resposta é passada para o `ProcessDialogResult` método.  
  
##### <a name="to-create-the-message-to-display-to-the-user"></a>Para criar a mensagem a ser exibida ao usuário  
  
-   Crie a mensagem, adicionando o seguinte código para o **Editor de códigos**. Digite este código abaixo a `UpdateDatabase` método.  
  
     [!code-csharp[VbRaddataConcurrency#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#4)]
     [!code-vb[VbRaddataConcurrency#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#4)]  
  
### <a name="process-the-users-response"></a>Processar a resposta do usuário  
 Você também precisa de código para processar a resposta do usuário para a caixa de mensagem. As opções são substituir o registro atual no banco de dados com a alteração proposta, ou abandonar as alterações locais e atualizar a tabela de dados com o registro que está atualmente no banco de dados. Se o usuário escolher Sim, o <xref:System.Data.DataTable.Merge%2A> método for chamado com o *preserveChanges* argumento definido como `true`. Isso faz com que a tentativa de atualização seja bem-sucedida, porque a versão original do registro agora coincide com o registro no banco de dados.  
  
##### <a name="to-process-the-user-input-from-the-message-box"></a>Para processar o usuário de entrada da caixa de mensagem  
  
-   Adicione o código a seguir abaixo do código que foi adicionado na seção anterior.  
  
     [!code-csharp[VbRaddataConcurrency#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#3)]
     [!code-vb[VbRaddataConcurrency#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#3)]  
  
## <a name="test-the-form"></a>Testar o formulário  
 Agora, é possível testar o formulário para garantir que ele se comporta da forma esperada. Para simular uma violação de simultaneidade, que você precisará alterar os dados no banco de dados depois de preencher o NorthwindDataSet.  
  
#### <a name="to-test-the-form"></a>Para testar o formulário  
  
1.  Selecione **F5** para executar o aplicativo.  
  
2.  Depois que o formulário for exibido, deixe-o em execução e alterne para o IDE do Visual Studio.  
  
3.  Sobre o **modo de exibição** menu, escolha **Gerenciador de servidores**.  
  
4.  Na **Gerenciador de servidores**, expanda a conexão de seu aplicativo está usando e, em seguida, expanda o **tabelas** nó.  
  
5.  Clique com botão direito do **clientes** da tabela e, em seguida, selecione **Mostrar dados da tabela**.  
  
6.  No primeiro registro (`ALFKI`) alterar `ContactName` para `Maria Anders2`.  
  
    > [!NOTE]
    >  Navegue até uma linha diferente para confirmar a alteração.  
  
7.  Alterne para o `ConcurrencyWalkthrough`do formulário em execução.  
  
8.  No primeiro registro no formulário (`ALFKI`), altere`ContactName` para `Maria Anders1`.  
  
9. Selecione o **salvar** botão.  
  
     O erro de simultaneidade é gerado e a caixa de mensagem é exibida.  
  
10. Selecionando **não** cancela a atualização e atualiza o conjunto de dados com os valores que estão atualmente no banco de dados. Selecionando **Sim** grava o valor proposto para o banco de dados.
  
## <a name="see-also"></a>Consulte também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)