---
title: Como adicionar um método localizador específico | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], Specific Finder
- BDC [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], get an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], Specific Finder
- Business Data Connectivity service [SharePoint development in Visual Studio], get an entity
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 403213b6dcd87251df0b24333c759c8de8720afd
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014811"
---
# <a name="how-to-add-a-specific-finder-method"></a>Como adicionar um método localizador específico
  Você pode retornar uma única instância de entidade criando um método *localizador específico* . O serviço corporativo de conectividade de dados (BDC) executa o método localizador específico quando um usuário escolhe uma entidade em uma Web Part de dados corporativos ou em uma lista externa. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

### <a name="to-create-a-specific-finder-method"></a>Para criar um método localizador específico

1. No **BDC designer**, escolha uma entidade.

    Para obter informações sobre como adicionar uma entidade ao **designer do BDC** no Visual Studio, consulte [como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md).

2. Na barra de menus, escolha **Exibir**  >  **outras janelas**, **detalhes do método do BDC**.

    A janela **detalhes do método BDC** é aberta. Para obter mais informações sobre essa janela, consulte [visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md).

3. Na lista **Adicionar um método** , escolha **criar método localizador específico**.

    O Visual Studio adiciona os seguintes elementos ao modelo. Esses elementos aparecem na janela **detalhes do método BDC** .

   - Um método.

   - Um parâmetro de entrada para o método.

   - Um parâmetro de retorno para o método.

   - Um descritor de tipo para cada parâmetro.

   - Uma instância de método para o método.

     Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

4. Abra a janela **Propriedades** do Visual Studio.

5. Configure o descritor de tipo do parâmetro de retorno como um descritor de tipo de entidade. Para obter informações sobre como criar um descritor de tipo de entidade, consulte [como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).

   > [!NOTE]
   > Você não precisará executar esta etapa se tiver adicionado um método localizador à entidade. O Visual Studio usa o descritor de tipo que você definiu no método Finder.

   > [!NOTE]
   > Se o campo identificador do tipo de entidade representa um campo em uma tabela de banco de dados gerada automaticamente, defina a propriedade **somente leitura** do campo identificador como **true**.

6. Na janela **detalhes do método** , escolha a instância do método do método.

7. Na **janela Propriedades**, defina a propriedade **nome do parâmetro de retorno** como o nome do parâmetro de retorno do método. Para obter mais informações sobre propriedades de instância de método, consulte [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14)).

8. No **Gerenciador de soluções**, abra o menu de atalho do arquivo de código de serviço que foi gerado para a entidade e escolha **Exibir código**.

    O arquivo de código do serviço de entidade é aberto no editor de código. Para obter mais informações sobre o arquivo de código do serviço de entidade, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

9. Adicione código ao método localizador específico. Esse código executa as seguintes tarefas:

   - Recupera um registro de uma fonte de dados.

   - Retorna uma entidade para o serviço BDC.

     O exemplo a seguir retorna um contato do banco de dados de exemplo AdventureWorks para SQL Server.

     > [!NOTE]
     > Substitua o valor do `ServerName` campo pelo nome do seu servidor.

     [!code-csharp[SP_BDC#3](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#3)]
     [!code-vb[SP_BDC#3](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#3)]

## <a name="see-also"></a>Consulte também
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Como adicionar um método localizador](../sharepoint/how-to-add-a-finder-method.md)
- [Como: adicionar um método de criador](../sharepoint/how-to-add-a-creator-method.md)
- [Como adicionar um método excluidor](../sharepoint/how-to-add-a-deleter-method.md)
- [Como adicionar um método de atualizador](../sharepoint/how-to-add-an-updater-method.md)
- [Visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
