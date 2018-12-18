---
title: 'Como: adicionar um método Finder específico | Microsoft Docs'
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
- Business Data Connectivity service [SharePoint development in Visual Studio], Specific Finder
- BDC [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], get an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], Specific Finder
- Business Data Connectivity service [SharePoint development in Visual Studio], get an entity
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 8005728d29c38e32d55f01e42d2666c69112b3f3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49886481"
---
# <a name="how-to-add-a-specific-finder-method"></a>Como: adicionar um método Finder específico
  Você pode retornar uma instância de entidade única, criando uma *Specific Finder* método. O serviço de conectividade de dados comerciais (BDC) executa o método de localizador específico quando um usuário escolhe uma entidade em uma web part de dados de negócios ou uma lista externa. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).  
  
### <a name="to-create-a-specific-finder-method"></a>Para criar um método Finder específico
  
1. Sobre o **Designer de BDC**, escolha uma entidade.  
  
    Para obter informações sobre como adicionar uma entidade para o **Designer de BDC** no Visual Studio, consulte [como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md).  
  
2. Na barra de menus, escolha **modo de exibição** > **Other Windows**, **detalhes do método BDC**.  
  
    O **detalhes do método BDC** janela é aberta. Para obter mais informações sobre essa janela, consulte [visão geral das ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md).  
  
3. No **adicionar um método** , escolha **criar método de localizador específico**.  
  
    Visual Studio adiciona os seguintes elementos ao modelo. Esses elementos aparecem na **detalhes do método BDC** janela.  
  
   - Um método.  
  
   - Um parâmetro de entrada para o método.  
  
   - Um parâmetro de retorno do método.  
  
   - Um descritor de tipo para cada parâmetro.  
  
   - Uma instância de método para o método.  
  
     Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).  
  
4. Abra o Visual Studio **propriedades** janela.  
  
5. Configure o descritor de tipo de parâmetro de retorno como um descritor de tipo de entidade. Para obter informações sobre como criar um descritor de tipo de entidade, consulte [como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).  
  
   > [!NOTE]  
   >  Você não precisa executar essa etapa se você tiver adicionado um método Finder para a entidade. O Visual Studio usa o descritor de tipo definido no método Finder.  
  
   > [!NOTE]  
   >  Se o campo de identificador do tipo de entidade representa um campo em uma tabela de banco de dados que é gerado automaticamente, defina a **somente leitura** propriedade de campo de identificador **verdadeiro**.  
  
6. No **detalhes do método** janela, escolha a instância de método do método.  
  
7. No **janela de propriedades**, defina as **retornar o nome do parâmetro** propriedade para o nome do parâmetro de retorno do método. Para obter mais informações sobre as propriedades de instância de método, consulte [MethodInstance](http://go.microsoft.com/fwlink/?LinkID=169282).  
  
8. Na **Gerenciador de soluções**, abra o menu de atalho do serviço arquivo de código que foi gerado para a entidade e, em seguida, escolha **Exibir código**.  
  
    O arquivo de código do serviço de entidade é aberto no Editor de códigos. Para obter mais informações sobre o arquivo de código do serviço de entidade, consulte [criar um modelo de conectividade de dados de negócios](../sharepoint/creating-a-business-data-connectivity-model.md).  
  
9. Adicione código ao método localizador específico. Esse código executa as seguintes tarefas:  
  
   - Recupera um registro de uma fonte de dados.  
  
   - Retorna uma entidade para o serviço de BDC.  
  
     O exemplo a seguir retorna um contato do banco de dados de exemplo AdventureWorks para SQL Server.  
  
     > [!NOTE]  
     >  Substitua o valor da `ServerName` campo com o nome do seu servidor.  
  
     [!code-csharp[SP_BDC#3](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#3)]
     [!code-vb[SP_BDC#3](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#3)]  
  
## <a name="see-also"></a>Consulte também
 [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)   
 [Como: adicionar um método Finder](../sharepoint/how-to-add-a-finder-method.md)   
 [Como: adicionar um método Creator](../sharepoint/how-to-add-a-creator-method.md)   
 [Como: adicionar um método Deleter](../sharepoint/how-to-add-a-deleter-method.md)   
 [Como: adicionar um método Updater](../sharepoint/how-to-add-an-updater-method.md)   
 [Visão geral de ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md)   
 [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)   
 [Como: definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)  
  
