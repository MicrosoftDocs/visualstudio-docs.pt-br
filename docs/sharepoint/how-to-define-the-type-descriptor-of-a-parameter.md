---
title: 'Como: definir o descritor de tipo de um parâmetro | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], type descriptor
- BDC [SharePoint development in Visual Studio], parameter types
- BDC [SharePoint development in Visual Studio], type descriptor
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter types
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ec2b0173838446c770f3323aacefebabc195c48b
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51294975"
---
# <a name="how-to-define-the-type-descriptor-of-a-parameter"></a>Como: definir o descritor de tipo de um parâmetro
  Um descritor de tipo contém propriedades que descrevem o tipo de dados de um parâmetro. Um descritor de tipo pode definir um campo, uma entidade ou uma coleção de entidades. Para obter mais informações, consulte [TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\)).  
  
### <a name="to-define-the-type-descriptor-of-a-parameter"></a>Para definir o descritor de tipo de um parâmetro  
  
1.  No **detalhes do método BDC** janela, escolha o descritor de tipo do parâmetro.  
  
2.  Na barra de menus, escolha **modo de exibição**, **janela propriedades**.  
  
3.  No **propriedades** janela, defina as propriedades do descritor de tipo.  
  
     Os procedimentos a seguir descrevem como definir um descritor de tipo como uma coleção de entidade, entidade ou campo.  
  
### <a name="to-define-a-field"></a>Para definir um campo  
  
1.  No **propriedades** janela, defina as **nome** propriedade do descritor de tipo para o nome de um campo no tipo que representa a entidade (por exemplo: **FirstName**).  
  
2.  Na lista de Avançar para o **TypeName** propriedade, escolha o tipo de dados apropriado (por exemplo, **Int32**).  
  
     Para obter informações sobre outros parâmetros opcionais, consulte [TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\)).  
  
### <a name="to-define-an-entity"></a>Para definir uma entidade  
  
1.  No **propriedades** janela, defina as **nome** propriedade para um nome que descreve a entidade (por exemplo: **contato**).  
  
2.  Defina as **TypeName** propriedade para o nome totalmente qualificado do tipo que representa a entidade. Esse tipo pode ser uma classe em seu projeto, um tipo definido em um assembly que você faz referência na sua solução ou um tipo definido no modelo de objeto BDC.  
  
    -   Para uma classe em seu projeto, escolha a seta para baixo ao lado de **TypeName** propriedade, escolha a **projeto atual** guia na caixa de diálogo que aparece e, em seguida, selecione a classe em seu projeto.  
  
         O nome totalmente qualificado inclui o namespace e o nome da classe seguido pelo nome do sistema LOB. O exemplo a seguir define o valor da **TypeName** propriedade a uma classe em seu projeto.  
  
         `MyBDCNamespace.BdcModel1.Contact, BdcModel1`  
  
    -   Para um tipo localizado em um assembly em sua solução, o nome totalmente qualificado inclui o nome do tipo, o nome do assembly, o número de versão, cultura e token de chave pública.  
  
         O exemplo a seguir define o valor da **TypeName** propriedade para um tipo definido em um assembly que você faz referência na sua solução.  
  
         `MyNamespace.Contact, myAssemblyName, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`  
  
    -   Para um tipo definido no modelo de objeto de BDC, o nome totalmente qualificado inclui o namespace e o nome do tipo.  
  
         O exemplo a seguir define o valor da **TypeName** propriedade para um tipo no modelo de objeto BDC.  
  
         `Microsoft.BusinessData.Runtime.DynamicType`  
  
3.  No **detalhes do método BDC** , abra a lista que aparece para o descritor de tipo e, em seguida, escolha **editar**.  
  
     O **BDC Explorer** janela é aberta.  
  
4.  No **BDC Explorer**, abra o menu de atalho do descritor de tipo e, em seguida, escolha **Adicionar descritor de tipo**.  
  
     Um novo descritor de tipo é adicionado como um filho ao descritor de tipo de entidade. Configure esse descritor de tipo como um campo.  
  
5.  Repita a etapa 4 para adicionar um descritor de tipo filho para cada campo da entidade.  
  
### <a name="to-define-a-collection-of-entities"></a>Para definir uma coleção de entidades  
  
1. No **detalhes do método BDC** janela, escolha o descritor de tipo do parâmetro que você deseja.  
  
2. Na barra de menus, escolha **modo de exibição**, **janela propriedades**.  
  
3. No **propriedades** janela, defina as **nome** propriedade com um nome que descreve a entidade (por exemplo: **contatos**).  
  
4. Defina a **IsCollection** propriedade **verdadeiro**. Isso indica que esse descritor de tipo é uma coleção de entidades.  
  
5. Defina a **TypeName** propriedade como uma cadeia de caracteres que contém uma referência para o <xref:System.Collections.Generic.IEnumerable%601> interface e o nome totalmente qualificado do tipo que representa a entidade. Esse tipo pode ser uma classe em seu projeto, um tipo definido em um assembly que você faz referência na sua solução ou um tipo definido no modelo de objeto BDC.  
  
   - Para uma classe em seu projeto, escolha a seta para baixo ao lado de **TypeName** propriedade, escolha a **projeto atual** guia na caixa de diálogo que aparece e, em seguida, selecione a classe em seu projeto.  
  
      O nome totalmente qualificado inclui o namespace e o nome da classe seguido pelo nome do sistema LOB.  
  
      O exemplo a seguir define o valor da **TypeName** propriedade a uma coleção de classes em seu projeto.  
  
      `System.Collections.Generic.IEnumerable`1 [MyBDCNamespace.` ` BdcModel1.Contact, BdcModel1]'  
  
   - Para um tipo localizado em um assembly em sua solução, o nome totalmente qualificado inclui o nome do tipo, o nome do assembly, o número de versão, cultura e token de chave pública.  
  
      O exemplo a seguir define o valor da **TypeName** propriedade a uma coleção de tipos em um assembly que você faz referência em sua solução.  
  
      `System.Collections.Generic.IEnumerable`1 [MyNamespace.Contact, myAssemblyName, versão version=4.0.0.0, Culture = neutral, PublicKeyToken = b77a5c561934e089]'  
  
   - Para um tipo definido no modelo de objeto de BDC, o nome totalmente qualificado inclui somente o namespace e o nome do tipo.  
  
      O exemplo a seguir define o valor da **TypeName** propriedade a uma coleção de tipos definidos no modelo de objeto BDC.  
  
      `System.Collections.Generic.IEnumerable`1 [DynamicType]'  
  
6. No **detalhes do método BDC** , abra a lista que aparece para o descritor de tipo e, em seguida, escolha **editar**.  
  
    O **BDC Explorer** janela é aberta.  
  
7. No **BDC Explorer**, abra o menu de atalho do descritor de tipo e, em seguida, escolha **Adicionar descritor de tipo**.  
  
    Um novo descritor de tipo é adicionado como um filho ao descritor de tipo de coleção. Configure esse descritor de tipo como uma entidade.  
  
## <a name="see-also"></a>Consulte também
 [Visão geral de ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md)   
 [Como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md)   
 [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)   
 [Como: definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)   
 [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)  
  
