---
title: Direcionar aplicativos do Office por meio de assemblies de interoperabilidade primária
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- assemblies [Office development in Visual Studio], PIA references
- primary interop assemblies [Office development in Visual Studio], adding references to
- Office primary interop assemblies in Visual Studio, adding references to
- Office applications [Office development in Visual Studio], automating
- application development [Office development in Visual Studio], automating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 60e351a15af4994d2bf64a800e3019501cf0571d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545763"
---
# <a name="how-to-target-office-applications-through-primary-interop-assemblies"></a>Como: direcionar aplicativos do Office por meio de assemblies de interoperabilidade primária
  Quando você cria um novo projeto do Office, o Visual Studio adiciona automaticamente referências ao Microsoft Office PIAs (assemblies de interoperabilidade primária) que são necessários para criar seu projeto. Você deve adicionar referências a outros PIAs nos seguintes cenários:

- Você deseja usar recursos de outros aplicativos Microsoft Office em seu projeto. Por exemplo, talvez você queira usar os recursos do Microsoft Office Excel em um projeto para Microsoft Office Word.

- Você deseja automatizar Microsoft Office aplicativos que não têm projetos dedicados no Visual Studio, como acesso Microsoft Office.

  [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="to-add-a-reference-to-a-primary-interop-assembly"></a>Para adicionar uma referência a um assembly de interoperabilidade primário

1. Abra o projeto do Office e selecione o nome do projeto em **Gerenciador de soluções**.

2. No menu **Projeto**, clique em **Adicionar Referência**.

3. Na guia **estrutura** , selecione o pia desejado na lista nome do **componente** . Para obter mais informações sobre os assemblies de interoperabilidade primária Microsoft Office disponíveis, consulte [assemblies de interoperabilidade primária do Office](../vsto/office-primary-interop-assemblies.md).

     Se o projeto for direcionado [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] para o ou posterior, a propriedade **inserir tipos de interoperabilidade** para a referência de assembly será definida como **true** por padrão. Ao usar essa configuração, sua solução não requer o PIA nos computadores dos usuários finais. Para obter mais informações, consulte [design e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md).

    > [!NOTE]
    > Em projetos do Office, sempre adicione referências a PIAs do Office usando a guia **.net** da caixa de diálogo **Adicionar referência** em vez da guia **com** . Para obter mais informações, consulte [assemblies de interoperabilidade primária do Office](../vsto/office-primary-interop-assemblies.md).

4. Clique em **OK**.

     O nome do assembly aparece na pasta **References** de **Gerenciador de soluções**.

## <a name="see-also"></a>Consulte também
- [Assemblies de interoperabilidade primária do Office](../vsto/office-primary-interop-assemblies.md)
- [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)
- [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)
- [Como instalar assemblies de interoperabilidade primária do Office](../vsto/how-to-install-office-primary-interop-assemblies.md)
