---
title: 'Como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Object Relational Designer) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e88224ab-ff61-4a3a-b6b8-6f3694546cac
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4f65af06a275dc50afafc70fd95c9b93d9bba458
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49232707"
---
# <a name="how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-or-designer"></a>Como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer relacional de objetos)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Os procedimentos armazenados podem ser adicionados ao Designer Relacional de Objetos e executados como métodos típicos do <xref:System.Data.Linq.DataContext>. Eles também podem ser usados para substituir o padrão [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] comportamento de tempo de execução que executa inserções, atualizações e exclusões quando alterações são salvas de classes de entidade para um banco de dados (por exemplo, ao chamar o <xref:System.Data.Linq.DataContext.SubmitChanges%2A> método).  
  
> [!NOTE]
>  Se seu procedimento armazenado retornar valores que precisem ser reenviados ao cliente (por exemplo, valores calculados no procedimento armazenado), crie parâmetros de saída em seus procedimentos armazenados. Se você não pode usar parâmetros de saída, escreva uma implementação de método parcial em vez de depender das substituições geradas pelo Designer Relacional de Objetos. Os membros mapeados para os valores gerados por banco de dados precisam ser definidos para valores apropriados após a conclusão com êxito de operações INSERT ou UPDATE. Para obter mais informações, consulte [responsabilidades do desenvolvedor em Substituir padrão comportamento](http://msdn.microsoft.com/library/c6909ddd-e053-46a8-980c-0e12a9797be1).  
  
> [!NOTE]
>  O [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] manipula automaticamente os valores gerados por banco de dados para colunas de identidade (incremento automático), rowguidcol (GUID gerado por banco de dados) e carimbo de data/hora. Os valores gerados pelo banco de dados em outros tipos de coluna resultarão inesperadamente em um valor nulo. Para retornar os valores gerados pelo banco de dados, você deve definir manualmente <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> à `true` e <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> para um dos seguintes: <xref:System.Data.Linq.Mapping.AutoSync>, <xref:System.Data.Linq.Mapping.AutoSync>, ou <xref:System.Data.Linq.Mapping.AutoSync>.  
  
## <a name="configuring-the-update-behavior-of-an-entity-class"></a>Configurando o comportamento de atualização de uma classe de entidade  
 Por padrão, a lógica para atualizar um banco de dados (inserções, atualizações e exclusões), com alterações que foram feitas nos dados em classes de entidade [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)], é fornecida em tempo de execução pelo [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)]. O tempo de execução cria padrão de comandos Insert, Update e Delete com base no esquema da tabela (a coluna e informações de chave primária). Quando o comportamento padrão não for desejado, você pode configurar o comportamento de atualização atribuindo procedimentos armazenados específicos para executar as inserções, atualizações e exclusões necessárias para manipular os dados em sua tabela. Você também pode fazer isso quando o comportamento padrão não é gerado, por exemplo, quando as classes de entidade mapeiam para as exibições. Finalmente, você pode substituir o comportamento de atualização padrão quando o banco de dados exige o acesso à tabela através de procedimentos armazenados.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-assign-stored-procedures-to-override-the-default-behavior-of-an-entity-class"></a>Para atribuir procedimentos armazenados para substituir o comportamento padrão de uma classe de entidade  
  
1.  Abra o **LINQ to SQL** arquivo no designer. (Duas vezes no arquivo. dbml **Gerenciador de soluções**.)  
  
2.  Na **Gerenciador de servidores**/**Database Explorer**, expanda **Stored Procedures** e localize os procedimentos armazenados que você deseja usar para Insert, Update, e/ou comandos de exclusão da classe de entidade.  
  
3.  Arraste o procedimento armazenado para o Designer Relacional de Objetos.  
  
     O procedimento armazenado é adicionado ao painel de métodos como um método <xref:System.Data.Linq.DataContext>. Para obter mais informações, consulte [métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md).  
  
4.  Selecione a classe de entidade para a qual você deseja usar o procedimento armazenado para executar atualizações.  
  
5.  No **propriedades** janela, selecione o comando para substituir (**inserir**, **atualização**, ou **excluir**).  
  
6.  Clique nas reticências (...) ao lado das palavras **usar tempo de execução** para abrir o **configurar comportamento** caixa de diálogo.  
  
7.  Selecione **personalizar**.  
  
8.  Selecione o procedimento armazenado desejado na **personalizar** lista.  
  
9. Inspecione a lista de **argumentos de método** e **propriedades da classe** para verificar se o **argumentos de método** são mapeados para apropriado **propriedades da classe**. Mapeie os argumentos de método originais (original _*ArgumentName*) para as propriedades originais (*PropertyName* (Original)) para os comandos Update e Delete.  
  
    > [!NOTE]
    >  Por padrão, os argumentos do método são mapeados para as propriedades de classe quando os nomes coincidem. Se os nomes de propriedade forem modificados, não haverá mais correspondência entre a tabela e a classe de entidade. Talvez seja necessário selecionar a propriedade de classe equivalente para mapeamento se o designer não puder determinar o mapeamento correto.  
  
10. Clique em **Okey** ou **aplicar**.  
  
    > [!NOTE]
    >  Você pode continuar a configurar o comportamento para cada combinação de classe/comportamento desde que você clique em **aplicar** após cada alteração. Se você alterar a classe ou o comportamento antes de clicar em **aplicar**, uma caixa de diálogo de aviso fornecendo uma oportunidade de aplicar as alterações serão exibidas.  
  
     Para reverter para usar a lógica de tempo de execução padrão para atualizações, clique no botão de reticências ao lado de Insert, Update, ou excluir na **propriedades** janela e, em seguida, selecione **usar tempo de execução** no  **Configurar o comportamento de** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [Métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md)   
 [Passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [Passo a passo: Criando procedimentos armazenados atualizados para a tabela de clientes Northwind](../data-tools/walkthrough-creating-update-stored-procedures-for-the-northwind-customers-table.md)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [Operações de inserção, atualização e exclusão](http://msdn.microsoft.com/library/26a43a4f-83c9-4732-806d-bb23aad0ff6b)

