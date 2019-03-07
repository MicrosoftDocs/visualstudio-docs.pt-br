---
title: 'Como: Configurar as informações de configuração para uma solução do Office'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], configuration files
- configuration files [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 159708bfad49e6a4a303363c6a0e9dd83b23d8e7
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56632011"
---
# <a name="how-to-set-up-configuration-information-for-an-office-solution"></a>Como: Configurar as informações de configuração para uma solução do Office
  Você pode usar arquivos de configuração para definir as configurações que são específicas para as soluções do Office. Você pode especificar configurações como a política de associação de assembly, objetos de comunicação remota, depuração e configurações de rastreamento.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-configuration-file-to-your-office-project"></a>Para adicionar um arquivo de configuração ao seu projeto do Office

1. No menu **Projeto**, clique em **Adicionar Novo Item**.

2. No **categorias** painel, clique em **geral**.

3. No **modelos** painel, selecione **arquivo de configuração de aplicativo**.

4. No **nome** , digite o mesmo nome que o assembly mais a extensão *. config*. Por exemplo, um arquivo de configuração para um assembly de projeto do Excel chamado *ExcelWorkbook1.dll* seria nomeado *ExcelWorkbook1.dll.config*.

5. Clique em **Adicionar**.

6. Crie arquivo de configuração de acordo com o esquema de arquivo de configuração do aplicativo. Para obter mais informações, consulte [esquema de arquivo de configuração para o .NET Framework](/dotnet/framework/configure-apps/file-schema/index).

   Não há nenhuma consideração especial para usar arquivos de configuração com projetos do Office.

## <a name="see-also"></a>Consulte também
- [Esquema de arquivo de configuração para o .NET Framework](/dotnet/framework/configure-apps/file-schema/index)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
