---
title: Como definir o descritor de tipo de um parâmetro | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], type descriptor
- BDC [SharePoint development in Visual Studio], parameter types
- BDC [SharePoint development in Visual Studio], type descriptor
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0b3ae803576c98a86a45d175af45aa28b3852134
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016848"
---
# <a name="how-to-define-the-type-descriptor-of-a-parameter"></a>Como definir o descritor de tipo de um parâmetro
  Um descritor de tipo contém propriedades que descrevem o tipo de dados de um parâmetro. Um descritor de tipo pode definir um campo, uma entidade ou uma coleção de entidades. Para obter mais informações, consulte [TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\)).

### <a name="to-define-the-type-descriptor-of-a-parameter"></a>Para definir o descritor de tipo de um parâmetro

1. Na janela **detalhes do método do BDC** , escolha o descritor de tipo do parâmetro.

2. Na barra de menus, escolha **Exibir**, **janela Propriedades**.

3. Na janela **Propriedades** , defina as propriedades do descritor de tipo.

     Os procedimentos a seguir descrevem como definir um descritor de tipo como um campo, entidade ou coleção de entidades.

### <a name="to-define-a-field"></a>Para definir um campo

1. Na janela **Propriedades** , defina a propriedade **Name** do descritor de tipo como o nome de um campo no tipo que representa a entidade (por exemplo: **FirstName**).

2. Na lista ao lado da propriedade **TypeName** , escolha o tipo de dados apropriado (por exemplo, **Int32**).

     Para obter informações sobre outros parâmetros opcionais, consulte [TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\)).

### <a name="to-define-an-entity"></a>Para definir uma entidade

1. Na janela **Propriedades** , defina a propriedade **Name** como um nome que descreve a entidade (por exemplo: **Contact**).

2. Defina a propriedade **TypeName** como o nome totalmente qualificado do tipo que representa a entidade. Esse tipo pode ser uma classe em seu projeto, um tipo definido em um assembly que você referencia em sua solução ou um tipo definido no modelo de objeto do BDC.

    - Para uma classe em seu projeto, escolha a seta para baixo ao lado da propriedade **TypeName** , escolha a guia **projeto atual** na caixa de diálogo que aparece e escolha a classe em seu projeto.

         O nome totalmente qualificado inclui o namespace e o nome da classe seguido pelo nome do sistema LOB. O exemplo a seguir define o valor da propriedade **TypeName** como uma classe em seu projeto.

         `MyBDCNamespace.BdcModel1.Contact, BdcModel1`

    - Para um tipo localizado em um assembly em sua solução, o nome totalmente qualificado inclui o nome do tipo, o nome do assembly, o número de versão, a cultura e o token de chave pública.

         O exemplo a seguir define o valor da propriedade **TypeName** para um tipo definido em um assembly que você referencia em sua solução.

         `MyNamespace.Contact, myAssemblyName, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`

    - Para um tipo definido no modelo de objeto do BDC, o nome totalmente qualificado inclui o namespace e o nome do tipo.

         O exemplo a seguir define o valor da propriedade **TypeName** como um tipo no modelo de objeto do BDC.

         `Microsoft.BusinessData.Runtime.DynamicType`

3. Na janela **detalhes do método BDC** , abra a lista que aparece para o descritor de tipo e escolha **Editar**.

     A janela do **Gerenciador do BDC** é aberta.

4. No **Gerenciador do BDC**, abra o menu de atalho do descritor de tipo e escolha **Adicionar descritor de tipo**.

     Um novo descritor de tipo é adicionado como um filho ao descritor de tipo de entidade. Configure este descritor de tipo como um campo.

5. Repita a etapa 4 para adicionar um descritor de tipo filho para cada campo da entidade.

### <a name="to-define-a-collection-of-entities"></a>Para definir uma coleção de entidades

1. Na janela **detalhes do método BDC** , escolha o descritor de tipo do parâmetro desejado.

2. Na barra de menus, escolha **Exibir**, **janela Propriedades**.

3. Na janela **Propriedades** , defina a propriedade **nome** como um nome que descreve a entidade (por exemplo: **contatos**).

4. Defina a propriedade **IsCollection** como **true**. Isso indica que esse descritor de tipo é uma coleção de entidades.

5. Defina a propriedade **TypeName** como uma cadeia de caracteres que contém uma referência à <xref:System.Collections.Generic.IEnumerable%601> interface e o nome totalmente qualificado do tipo que representa a entidade. Esse tipo pode ser uma classe em seu projeto, um tipo definido em um assembly que você referencia em sua solução ou um tipo definido no modelo de objeto do BDC.

   - Para uma classe em seu projeto, escolha a seta para baixo ao lado da propriedade **TypeName** , escolha a guia **projeto atual** na caixa de diálogo que aparece e escolha a classe em seu projeto.

      O nome totalmente qualificado inclui o namespace e o nome da classe seguido pelo nome do sistema LOB.

      O exemplo a seguir define o valor da propriedade **TypeName** como uma coleção de classes em seu projeto.

      `System.Collections.Generic.IEnumerable`1 [MyBDCNamespace. BdcModel1. Contact, BdcModel1] '

   - Para um tipo localizado em um assembly em sua solução, o nome totalmente qualificado inclui o nome do tipo, o nome do assembly, o número de versão, a cultura e o token de chave pública.

      O exemplo a seguir define o valor da propriedade **TypeName** como uma coleção de tipos em um assembly que você referencia em sua solução.

      `System.Collections.Generic.IEnumerable`1 [MyNamespace. Contact, myassemblyname, versão = 4.0.0.0, Culture = neutral, PublicKeyToken = b77a5c561934e089] '

   - Para um tipo definido no modelo de objeto do BDC, o nome totalmente qualificado inclui apenas o namespace e o nome do tipo.

      O exemplo a seguir define o valor da propriedade **TypeName** como uma coleção de tipos definidos no modelo de objeto do BDC.

      `System.Collections.Generic.IEnumerable`1 [Microsoft. BusinessData. Runtime. DynamicType] '

6. Na janela **detalhes do método BDC** , abra a lista que aparece para o descritor de tipo e escolha **Editar**.

    A janela do **Gerenciador do BDC** é aberta.

7. No **Gerenciador do BDC**, abra o menu de atalho do descritor de tipo e escolha **Adicionar descritor de tipo**.

    Um novo descritor de tipo é adicionado como um filho ao descritor de tipo de coleção. Configure este descritor de tipo como uma entidade.

## <a name="see-also"></a>Consulte também
- [Visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
