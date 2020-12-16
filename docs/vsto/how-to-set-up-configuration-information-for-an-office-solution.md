---
title: Configurar informações de configuração para uma solução do Office
description: Saiba como você pode usar arquivos de configuração para definir configurações específicas para suas soluções de Microsoft Office.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 3cff5e6f559245e361eda0db6623312917891969
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97528154"
---
# <a name="how-to-set-up-configuration-information-for-an-office-solution"></a>Como definir informações de configuração para uma solução do Office
  Você pode usar arquivos de configuração para definir configurações específicas para suas soluções do Office. Você pode especificar configurações como política de associação de assembly, objetos de comunicação remota, depuração e configurações de rastreamento.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-configuration-file-to-your-office-project"></a>Para adicionar um arquivo de configuração ao seu projeto do Office

1. No menu **Projeto** , clique em **Adicionar Novo Item**.

2. No painel **categorias** , clique em **geral**.

3. No painel **modelos** , selecione **arquivo de configuração do aplicativo**.

4. Na caixa **nome** , digite o mesmo nome que o assembly mais a extensão *. config*. Por exemplo, um arquivo de configuração para um assembly de projeto do Excel chamado *ExcelWorkbook1.dll* seria nomeado *ExcelWorkbook1.dll.config*.

5. Clique em **Adicionar**.

6. Crie seu arquivo de configuração de acordo com o esquema do arquivo de configuração do aplicativo. Para obter mais informações, consulte [esquema do arquivo de configuração para o .NET Framework](/dotnet/framework/configure-apps/file-schema/index).

   Não há considerações especiais para o uso de arquivos de configuração com projetos do Office.

## <a name="see-also"></a>Veja também
- [Esquema do arquivo de configuração para o .NET Framework](/dotnet/framework/configure-apps/file-schema/index)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
