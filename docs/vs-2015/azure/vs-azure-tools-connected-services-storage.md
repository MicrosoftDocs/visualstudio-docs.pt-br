---
title: Adicionar armazenamento do Azure usando serviços conectados no Visual Studio | Microsoft Docs
description: Adicionar armazenamento do Azure para seu aplicativo usando a caixa de diálogo do Visual Studio adicionar serviços conectados
author: ghogen
manager: douge
assetId: 521ec044-ad4b-4828-8864-01decde2e758
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/26/2017
ms.author: ghogen
ms.openlocfilehash: 63b796d9c514602a40f15b5725c07b1b89787df1
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001141"
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Adicionando o armazenamento do Azure usando o Visual Studio Connected Services
Com o Visual Studio, você pode conectar qualquer um dos seguintes no armazenamento do Azure usando o **adicionar serviços conectados** caixa de diálogo:

- C#serviço de nuvem
- Serviço móvel de back-end do .NET
- Site da Web ASP.NET ou serviço
- Serviço do ASP.NET Core
- Serviço WebJob do Azure 

A funcionalidade do serviço conectado adiciona todas as referências necessárias e código de conexão ao seu projeto e modifica os arquivos de configuração adequadamente. 

Após a conclusão, o **adicionar serviços conectados** caixa de diálogo automaticamente exibe a documentação detalhando as etapas necessárias para começar a trabalhar com o armazenamento de BLOBs, filas e tabelas.

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a>Conectar ao armazenamento do Azure usando a caixa de diálogo Serviços conectados
1. Abra o projeto no Visual Studio

1. Na **Gerenciador de soluções**, clique com botão direito do **serviços conectados** nó e, no menu de contexto e selecione **Adicionar serviço conectado**.
   
    ![Adicionar o Azure serviço conectado](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. No **serviços conectados** página, selecione **armazenamento de nuvem com o armazenamento do Azure**.
   
    ![Adicionar armazenamento do Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. No **armazenamento do Azure** caixa de diálogo, selecione uma conta de armazenamento existente e selecione **Add**.
   
    Se você precisar criar uma conta de armazenamento, vá para a próxima etapa. Caso contrário, pule para a etapa 6.
    
    ![Adicionar conta de armazenamento existente ao projeto](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. Para criar uma conta de armazenamento: 
   
   1. Selecione **criar uma nova conta de armazenamento** na parte inferior da caixa de diálogo.

   1. Preencha a **criar conta de armazenamento** caixa de diálogo e selecione **criar**.
      
       ![Nova conta de armazenamento do Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Quando o **armazenamento do Azure** caixa de diálogo for exibida, a nova conta de armazenamento aparece na lista. Selecione a nova conta de armazenamento na lista e selecione **adicionar**.

1. O serviço de armazenamento conectado aparece sob o **referências de serviço** nó do projeto.
   
## <a name="how-your-project-is-modified"></a>Como o projeto é modificado
Quando você concluir a caixa de diálogo, o Visual Studio adiciona referências e modifica determinados arquivos de configuração. As alterações específicas dependem do tipo de projeto: 

- Projeto ASP.NET - [o que aconteceu — projetos ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- Projeto do ASP.NET Core - [o que aconteceu — projetos ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- Projeto de serviço de nuvem (funções web e funções de trabalho) - [o que aconteceu — projetos de serviço de nuvem](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- Projeto de WebJob - [o que aconteceu — projetos WebJob](/azure/visual-studio/vs-storage-webjobs-what-happened)

## <a name="next-steps"></a>Próximas etapas
- [Fórum do MSDN: O armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Blog da equipe de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/)
- [Documentação do armazenamento do Azure](https://docs.microsoft.com/azure/storage/)
