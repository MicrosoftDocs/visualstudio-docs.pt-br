---
title: 'Como: adicionar um descritor de filtro a um método localizador | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], filter descriptors
- Business Data Connectivity service [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], filter descriptors
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 228afb2f49f4d528fa9b806e9bf8d2531f7de901
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016738"
---
# <a name="how-to-add-a-filter-descriptor-to-a-finder-method"></a>Como: adicionar um descritor de filtro a um método localizador
  Os descritores de filtro permitem que os consumidores do modelo passem valores para métodos antes de serem executados. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

 Um cenário comum é que os usuários no SharePoint desejam recuperar instâncias de um tipo de conteúdo externo que correspondam a alguns critérios. Você pode dar suporte a esse cenário adicionando um descritor de filtro a um método localizador.

### <a name="to-add-a-filter-descriptor-to-a-finder-method"></a>Para adicionar um descritor de filtro a um método localizador

1. Na janela **detalhes do método do BDC** , expanda o nó de um método localizador, expanda o nó **parâmetros** e, em seguida, adicione um parâmetro de entrada. Para obter mais informações, consulte [como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md).

2. Na janela **detalhes do método** , escolha o descritor de tipo do parâmetro.

3. Na barra de menus, escolha **Exibir**  >  **janela de propriedades**.

4. Na janela **Propriedades** , defina a propriedade **nome do tipo** como um tipo de dados apropriado para o filtro.

     Por exemplo, um filtro pode usar uma data de pedido para limitar o número de pedidos de vendas retornados pelo método. Para dar suporte a esse filtro, a propriedade **nome do tipo** do descritor de tipo deve ser definida como **System. DateTime**.

5. Na janela **detalhes do método** , expanda o nó **descritores de filtro** .

6. Na lista **Adicionar um descritor de filtro** , escolha **criar descritor de filtro**.

     Um novo descritor de filtro é exibido abaixo do nó descritores de **filtro** .

7. Na barra de menus, escolha **Exibir**  >  **janela de propriedades**.

8. Na janela **Propriedades** , escolha a propriedade **tipo** .

9. Na lista que aparece para a propriedade **Type** , escolha o padrão de filtragem desejado.

     Por exemplo, para criar um filtro que usa uma data de pedido para limitar o número de pedidos de vendas retornados em um método localizador, escolha **comparação**. Um filtro de comparação garante que um método localizador retorne apenas instâncias que atendam a uma condição específica. Para obter mais informações sobre cada padrão de filtragem, consulte [tipos de filtros com suporte pelo BDC](/previous-versions/office/developer/sharepoint-2010/ee556392(v=office.14)).

10. Na janela **Propriedades** , escolha a propriedade **descritores de tipo associados** .

11. Na lista que aparece para a propriedade de descritores de **tipo associados** , escolha a descrição de tipo que você criou anteriormente neste procedimento. Isso relaciona o filtro ao parâmetro de entrada do método Finder.

12. Adicione o código ao método Finder que retorna dados. Você pode usar o parâmetro de entrada como uma condição em uma consulta SELECT.

     O exemplo a seguir retorna pedidos de vendas que têm a data do pedido especificado.

    > [!NOTE]
    > Substitua o valor do `ServerName` campo pelo nome do seu servidor.

     [!code-csharp[SP_BDC#11](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs#11)]
     [!code-vb[SP_BDC#11](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb#11)]

## <a name="see-also"></a>Consulte também
- [Como adicionar um método localizador](../sharepoint/how-to-add-a-finder-method.md)
- [Como adicionar um método localizador específico](../sharepoint/how-to-add-a-specific-finder-method.md)
- [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Integrando dados corporativos ao SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
