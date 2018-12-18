---
title: 'Como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- assemblies [Office development in Visual Studio], PIA references
- primary interop assemblies [Office development in Visual Studio], adding references to
- Office primary interop assemblies in Visual Studio, adding references to
- Office applications [Office development in Visual Studio], automating
- application development [Office development in Visual Studio], automating
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 576d26f039005dac3d494652f1e5127c39092a00
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49863744"
---
# <a name="how-to-target-office-applications-through-primary-interop-assemblies"></a>Como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários
  Quando você cria um novo projeto do Office, o Visual Studio adiciona automaticamente referências para os Microsoft Office assemblies de interoperabilidade primários (PIAs) que são necessários para compilar seu projeto. Você deve adicionar referências a outros PIAs nos seguintes cenários:  
  
- Você deseja usar os recursos de outros aplicativos do Microsoft Office em seu projeto. Por exemplo, você talvez queira usar os recursos do Microsoft Office Excel em um projeto para o Microsoft Office Word.  
  
- Você deseja automatizar aplicativos do Microsoft Office que não tenham projetos dedicados no Visual Studio, como o Microsoft Office Access.  
  
  [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="to-add-a-reference-to-a-primary-interop-assembly"></a>Para adicionar uma referência a um assembly de interoperabilidade primário  
  
1.  Abra seu projeto do Office e selecione o nome do projeto no **Gerenciador de soluções**.  
  
2.  No menu **Projeto**, clique em **Adicionar Referência**.  
  
3.  Sobre o **Framework** , selecione o PIA desejado na **nome do componente** lista. Para obter mais informações sobre disponíveis Microsoft Office assemblies de interoperabilidade primários, consulte [assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md).  
  
     Se o projeto é direcionado a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, o **inserir tipos Interop** propriedade para a referência de assembly é definida como **True** por padrão. Ao usar essa configuração, sua solução não exige o PIA nos computadores dos usuários finais. Para obter mais informações, consulte [Design e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md).  
  
    > [!NOTE]  
    >  Em projetos do Office, sempre adicionar referências aos PIAs do Office usando o **.NET** guia da **adicionar referência** caixa de diálogo, em vez do **COM** guia. Para obter mais informações, consulte [assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md).  
  
4.  Clique em **OK**.  
  
     O nome do assembly aparece na **referências** pasta de **Gerenciador de soluções**.  
  
## <a name="see-also"></a>Consulte também  
 [Assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md)   
 [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)   
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Como: assemblies de interoperabilidade primários do Office de instalação](../vsto/how-to-install-office-primary-interop-assemblies.md)  
  
  