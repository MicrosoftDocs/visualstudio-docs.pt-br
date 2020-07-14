---
title: Visualizar dados de exemplo em uma interface do usuário XAML
titleSuffix: Blend for Visual Studio
ms.date: 03/06/2018
ms.topic: conceptual
ms.assetid: 87d31b6c-4607-4121-bb7d-cfc80390ab93
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bd48ac8f5753521240ed3feb6003d945786820a3
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329083"
---
# <a name="display-data-in-blend-for-visual-studio"></a>Exibir dados no Blend para Visual Studio

É possível exibir dados de exemplo no designer ao personalizar o layout de páginas. É possível gerar dados de exemplo do zero ou usando uma classe existente. Você também pode se conectar aos *Dados dinâmicos* que aparecem no aplicativo quando você o executa.

> [!NOTE]
> O painel de **dados** no Blend tem suporte apenas para projetos direcionados .NET Framework. Não há suporte para projetos UWP ou projetos destinados ao .NET Core.

## <a name="generate-sample-data"></a>Gerar dados de exemplo

Para gerar dados de exemplo, abra um documento XAML. No painel **Dados**, escolha o botão **Criar dados de exemplo** ![Ícone Criar dados de exemplo](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png) e, em seguida, escolha **Novos Dados de Exemplo**.

Defina a estrutura dos dados no painel **Dados** e, então, associe-a aos elementos de interface do usuário em qualquer página.

![Painel de dados](../designers/media/496d7ebc-fe46-42f6-95a8-57b0e5be5d49.png)

Caso deseje que os dados de exemplo apareçam nas páginas quando o aplicativo for executado, escolha **Opções de fonte de dados** ![Ícone de Opções de fonte de dados](../designers/media/ae1fd260-4f84-420d-b196-45fde357d81d.png) e, em seguida, escolha **Habilitar ao Executar Aplicativo**.

![Item de menu Habilitar ao Executar Aplicativo](../designers/media/05d5356d-91bb-4e6b-b3f7-29b76852c4b3.png)

**Assista a um vídeo curto:** ![Ícone de reprodução](../designers/media/bldadminconsoleinitialconfigicon.PNG) [Criar dados de exemplo do zero](https://www.bing.com/videos/search?q=blend%20data&qs=n&form=QBVR&pq=blend%20data&sc=8-7&sp=-1&sk=#view=detail&mid=F8F2449A76956D480FD2F8F2449A76956D480FD2).

## <a name="generate-sample-data-from-a-class"></a>Gerar dados de exemplo de uma classe

Se você já tiver criado as classes que descrevem a estrutura dos dados, será possível gerar dados de exemplo com base nelas.

Para gerar dados de exemplo com base em uma classe, abra um documento XAML e, no painel **Dados**, clique no botão **Criar dados de exemplo** ![Ícone Criar dados de exemplo](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png) e, em seguida, clique em **Criar Dados de Exemplo da Classe**.

**Assista a um vídeo curto:** ![Ícone de reprodução](../designers/media/bldadminconsoleinitialconfigicon.PNG) [Mix up some data binding with Blend](https://www.youtube.com/watch?v=LSwPB6CAvjg) (Combinar algumas associações de dados com o Blend).

## <a name="see-also"></a>Veja também

- [Criar uma interface do usuário usando o Blend para Visual Studio](../xaml-tools/creating-a-ui-by-using-blend-for-visual-studio.md)
