---
title: Como adicionar um método localizador | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], get entities
- Business Data Connectivity service [SharePoint development in Visual Studio], return entities
- BDC [SharePoint development in Visual Studio], return entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Finder method
- Business Data Connectivity service [SharePoint development in Visual Studio], get entities
- BDC [SharePoint development in Visual Studio], Finder method
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1fa8f8eb34943cc17bc6cabca8e93ea7569a7ba6
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016721"
---
# <a name="how-to-add-a-finder-method"></a>Como adicionar um método localizador
  Para habilitar o serviço BDC (conectividade de dados corporativos) para exibir uma lista de entidades em uma Web Part ou lista, você deve criar um método *localizador* . Um método Finder é um método especial que retorna uma coleção de instâncias de entidade. Para obter mais informações, consulte [criando um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

### <a name="to-create-a-finder-method"></a>Para criar um método localizador

1. No **BDC designer**, escolha uma entidade.

    Para obter mais informações, consulte [como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md).

2. Na barra de menus, escolha **Exibir**  >  **outros**  >  **detalhes do método**do Windows BDC.

    A janela **detalhes do método BDC** é aberta. Para obter mais informações sobre a janela **detalhes do método BDC** , consulte [visão geral das ferramentas de design do modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md).

3. Na lista **Adicionar um método** , escolha **criar método localizador**.

    O Visual Studio adiciona um método, um parâmetro de retorno e um descritor de tipo.

4. Configure o descritor de tipo como um descritor de tipo de coleção de entidade. Para obter mais informações sobre como criar um descritor de tipo de coleção de entidades, consulte [como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).

   > [!NOTE]
   > Você não precisará executar esta etapa se tiver adicionado um método localizador específico à entidade. O Visual Studio usa o descritor de tipo que você definiu no método localizador específico.

5. No **Gerenciador de soluções**, abra o menu de atalho do arquivo de código de serviço que foi gerado para a entidade e escolha **Exibir código**. Para obter mais informações sobre o arquivo de código de serviço, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

6. Adicione o código ao método Finder. Esse código executa as seguintes tarefas:

   - Recupera dados de uma fonte de dados.

   - Retorna uma lista de entidades para o serviço BDC.

     O exemplo a seguir retorna uma coleção de `Contact` entidades usando dados do banco de dado de exemplo AdventureWorks para SQL Server.

   > [!NOTE]
   > Substitua o valor do `ServerName` campo pelo nome do seu servidor.

    [!code-csharp[SP_BDC#2](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#2)]
    [!code-vb[SP_BDC#2](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#2)]

## <a name="see-also"></a>Consulte também
- [Visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Como adicionar um método localizador específico](../sharepoint/how-to-add-a-specific-finder-method.md)
- [Como: adicionar um método de criador](../sharepoint/how-to-add-a-creator-method.md)
- [Como adicionar um método excluidor](../sharepoint/how-to-add-a-deleter-method.md)
- [Como adicionar um método de atualizador](../sharepoint/how-to-add-an-updater-method.md)
- [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
