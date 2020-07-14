---
title: Como instalar assemblies de interoperabilidade primária do Office
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies [Office development in Visual Studio], installing
- Office primary interop assemblies, installing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b6f90b568f98abe5026525a60723efb59f737235
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544775"
---
# <a name="how-to-install-office-primary-interop-assemblies"></a>Como instalar assemblies de interoperabilidade primária do Office
  Instale os assemblies de interoperabilidade primária (PIAs) do Microsoft Office ao instalar o Office.

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-install-the-pias-when-you-install-office"></a>Para instalar os PIAs ao instalar o Office

1. Certifique-se de que você tenha uma versão do .NET Framework 2.0 ou posterior.

2. Instale o Microsoft Office e certifique-se de que o recurso de **suporte de programação .net** esteja selecionado para os aplicativos que você deseja estender (esse recurso está incluído na instalação padrão).

    > [!WARNING]
    > Por padrão, o PIA é inserido em sua solução quando você o cria para que você não precise distribuir PIAs aos usuários como um pré-requisito para usar seu suplemento ou personalização do VSTO.

## <a name="see-also"></a>Confira também
- [Assemblies de interoperabilidade primária do Office](../vsto/office-primary-interop-assemblies.md)
- [Como: direcionar aplicativos do Office por meio de assemblies de interoperabilidade primária](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Como configurar um computador para desenvolver soluções do Office](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [Como instalar o Ferramentas do Visual Studio para o Office Runtime Redistributable](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [Visão geral do desenvolvimento de soluções do Office &#40;&#41;VSTO](../vsto/office-solutions-development-overview-vsto.md)
- [Introdução &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
