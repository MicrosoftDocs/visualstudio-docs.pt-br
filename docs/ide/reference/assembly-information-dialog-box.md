---
title: Caixa de diálogo Informações do Assembly
description: Saiba mais sobre a caixa de diálogo informações do assembly e como ela é usada para especificar os valores da .NET Framework atributos de assembly global.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesAssemblyInfo
helpviewer_keywords:
- Assembly Information dialog box
ms.assetid: 8f1f6449-e03d-4a5b-9076-d3b1f84ada48
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee8738d06c0f02adb6f5e6352d2006e0133c66ef
ms.sourcegitcommit: 935e4d9a20928b733e573b6801a6eaff0d0b1b14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "95871334"
---
# <a name="assembly-information-dialog-box"></a>Caixa de diálogo Informações do Assembly

A caixa de diálogo Informações do Assembly é usada para especificar os valores dos atributos de assembly global do .NET Framework, que são armazenados no arquivo AssemblyInfo criado automaticamente com o projeto. No Gerenciador de Soluções, o arquivo AssemblyInfo está localizado no nó **Meu Projeto** para projetos do Visual Basic (clique em **Mostrar todos os arquivos** para exibi-lo). Para projetos do C#, está localizado em **Propriedades**. Para saber mais, confira [Atributos (C#)](/dotnet/csharp/programming-guide/concepts/attributes/index).

Para acessar essa caixa de diálogo, selecione um nó de projeto no **Gerenciador de Soluções** e, no menu **Projeto**, selecione **Propriedades**. Na página **Aplicativo**, selecione o botão **Informações do Assembly**.

## <a name="uielement-list"></a>Lista de elementos de interface do usuário

**Título**\
Especifica um título para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyTitleAttribute>.

**Descrição**\
Especifica uma descrição opcional para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyDescriptionAttribute>.

**Corporativa**\
Especifica um nome de empresa para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyCompanyAttribute>.

É possível definir ou alterar o valor padrão de Empresa no registro. Procure pelo valor **RegisteredOrganization** na chave **Computer\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion** ou **Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion**, dependendo da sua versão do Windows.

**Remessa**\
Especifica um nome de produto para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyProductAttribute>.

**Internacionais**\
Especifica uma notificação de direitos autorais para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyCopyrightAttribute>.

**Registrada**\
Especifica uma marca registrada para o manifesto do assembly. Corresponde ao <xref:System.Reflection.AssemblyTrademarkAttribute>.

**Versão do assembly**\
Especifica a versão do assembly. Corresponde ao <xref:System.Reflection.AssemblyVersionAttribute>.

**Versão do arquivo**\
Especifica um número de versão que instrui o compilador a usar uma versão específica do recurso de versão de arquivo do Win32. Corresponde ao <xref:System.Reflection.AssemblyFileVersionAttribute>.

**VOLUME**\
Um GUID exclusivo que identifica o assembly. Ao criar um projeto, o Visual Studio gera um GUID para o assembly. Corresponde ao <xref:System.Guid>.

**Idioma neutro**\
Especifica a qual cultura o assembly dá suporte. Corresponde ao <xref:System.Resources.NeutralResourcesLanguageAttribute>. O padrão é **(nenhum)**.

**Tornar assembly COM-visível**\
Especifica se os tipos no assembly estarão disponíveis para o COM. Corresponde ao <xref:System.Runtime.InteropServices.ComVisibleAttribute>.

> [!NOTE]
> Para obter mais informações sobre como definir essas propriedades ao gerar um pacote NuGet em uma .NET Framework biblioteca de classes, consulte [Configurar propriedades do projeto para o pacote](/nuget/quickstart/create-and-publish-a-package-using-visual-studio-net-framework#configure-project-properties-for-the-package).

## <a name="see-also"></a>Confira também

- [Página de Aplicativo, Designer de Projeto (Visual Basic)](../../ide/reference/application-page-project-designer-visual-basic.md)
- [Atributos](/previous-versions/z0w1kczw(v=vs.140))