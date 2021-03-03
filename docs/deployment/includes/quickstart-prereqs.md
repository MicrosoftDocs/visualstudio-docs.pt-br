---
ms.openlocfilehash: a33871a9a80dfcb6260f57e504c72ae2f72077bd
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101749956"
---
## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=vs-2019"

* [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) instalado com as cargas de trabalho apropriadas para a linguagem de sua escolha:
  * ASP.NET: **ASP.NET e desenvolvimento Web**
  * Python: **Desenvolvimento do Python**
  * Node.js: **suporte ao desenvolvimento em Node.js**
::: moniker-end
::: moniker range="vs-2017"
* [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) instalado com as cargas de trabalho apropriadas para a linguagem de sua escolha:
  * ASP.NET: **ASP.NET e desenvolvimento Web**
  * Python: **Desenvolvimento do Python**
  * Node.js: **suporte ao desenvolvimento em Node.js**
::: moniker-end

* Um projeto ASP.NET, ASP.NET Core, Python ou Node.js. Se você ainda não tiver um projeto, selecione uma opção abaixo:
  * ASP.NET Core: Siga o [início rápido: Use o Visual Studio para criar seu primeiro aplicativo web ASP.NET Core](../../ide/quickstart-aspnet-core.md)ou use as seguintes etapas:
    ::: moniker range=">=vs-2019"
    No Visual Studio 2019, escolha **criar um novo projeto** na janela iniciar. Se a janela iniciar não estiver aberta, escolha **arquivo**  >  **Iniciar janela**. Digite **aplicativo Web** na caixa de pesquisa, escolha **C#** como idioma, escolha **ASP.NET Core aplicativo Web (Model-View-Controller)** e, em seguida, escolha **Avançar**. Na próxima tela, nomeie o projeto **MyASPApp** e escolha **Avançar**.

    Escolha a estrutura de destino recomendada (.NET Core 3,1) ou .NET 5 e, em seguida, escolha **criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    No Visual Studio 2017, escolha **arquivo**  >  **novo projeto**, selecione **Visual C#**  >  **.NET Core** e, em seguida, selecione **ASP.NET Core aplicativo Web**. Quando solicitado, selecione o modelo **aplicativo Web (Model-View-Controller)**, verifique se **Sem autenticação** está selecionado e, em seguida, selecione **OK**.
    ::: moniker-end
  * Python: siga [Início Rápido: Criar seu primeiro aplicativo Web Python usando o Visual Studio](../../ide/quickstart-python.md) ou use **Arquivo** > **Novo projeto**, selecione **Python**, e, em seguida, **Projeto Web do Flask**.
  * Node.js: siga [Início Rápido: usar o Visual Studio para criar seu primeiro aplicativo Node.js](../../ide/quickstart-nodejs.md) ou use **Arquivo** > **Novo projeto**, selecione **JavaScript** e, em seguida, selecione **Aplicativo Web do Node.js em branco**.

* Certifique-se de criar o projeto usando o comando de menu **Criar > Criar solução** antes de seguir as etapas de implantação.