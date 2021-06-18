---
title: Atualizar o Visual Studio usando um layout offline mínimo
description: Saiba como Atualizar Visual Studio usando um layout offline mínimo.
ms.date: 05/18/2021
ms.custom: seodec18
ms.topic: how-to
ms.assetid: ''
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 1c3a6254c3205038be3d56c64de091e659d2bbd5
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306729"
---
# <a name="update-visual-studio-using-a-minimal-offline-layout"></a>Atualizar o Visual Studio usando um layout offline mínimo

Para computadores que não estão conectados à Internet, a criação de um layout mínimo é a maneira mais fácil e rápida de atualizar suas instâncias Visual Studio offline.

A ferramenta de layout mínimo gera um layout adaptado especificamente às necessidades da sua equipe. Os administradores corporativos podem usar essa ferramenta para criar layouts de atualização para a maioria das versões Visual Studio 2017 e 2019. Ao contrário de um layout Visual Studio completo, um layout mínimo contém apenas os pacotes atualizados, portanto, é sempre menor e mais rápido para gerar e implantar. Você pode minimizar ainda mais o tamanho do layout de atualização especificando apenas os idiomas, cargas de trabalho e componentes desejados.

## <a name="how-to-generate-a-minimal-layout"></a>Como gerar um layout mínimo

> [!IMPORTANT]
> Essas instruções pressuem que você tenha criado e usado layouts anteriormente. Para obter mais informações sobre como fazer isso, consulte a página Atualizar uma instalação baseada [em Visual Studio](update-a-network-installation-of-visual-studio.md) rede.
>
> Para entender melhor o ciclo de vida Visual Studio, consulte a Visual Studio ciclo de vida e [manutenção do](/visualstudio/releases/2019/servicing) produto.
>

Essa ferramenta cria layouts de atualização Visual Studio 2017 (15.9) e em diante. O layout pode ser implantado em máquinas de rede/offline para atualizar Visual Studio instâncias. Durante [a criação de layout normal,](update-a-network-installation-of-visual-studio.md)todos os pacotes para essa versão específica são baixados. A criação de layout normal é necessária para reparar, desinstalar e outras operações padrão em Visual Studio instâncias. O layout mínimo baixa apenas pacotes atualizados, portanto, é menor e mais fácil de copiar para máquinas offline.

### <a name="installing-the-minimal-layout-tool"></a>Instalando a ferramenta de layout mínima

 1. Primeiro, baixe a ferramenta de layout mínima localizada [aqui](https://aka.ms/vs/installer/minimallayout). Escolha Salvar **quando** solicitado e, em seguida, selecione **Executar**.

     ![Salvar a ferramenta de layout mínima](media/save-minimal-layout.png)

 2. Em seguida, aceite o prompt Controle de Conta de Usuário clicando **em Sim.**

     ![Aceitar controle de conta de usuário](media/accept-user-account-control.png)

 3. A ferramenta de layout mínima será instalada no `C:\Program Files (x86)\Microsoft Visual Studio\MinimalLayout` .

### <a name="how-to-use-the-minimal-layout-tool"></a>Como usar a ferramenta de layout mínima

`MinimalLayout.exe` usa os comandos e opções a seguir para gerar o layout. Pelo menos um comando é necessário para executar a ferramenta. Veja como você executará a ferramenta:

```MinimalLayout.exe [command] <options>...```

#### <a name="commands"></a>Comandos

* **Versão** prévia: use este comando para visualizar quantos pacotes serão baixados e o espaço total usado para criar esse layout.
* **Gerar**: use este comando para gerar o layout mínimo para atualizar Visual Studio.
* **Regenerar:** use este comando para regenerar um layout usando um arquivo de resposta de layout mínimo existente. Cada layout mínimo produz um `MinimalLayout.json` arquivo de resposta, que contém os parâmetros de entrada de layout mínimo originais. Você pode usar o **comando Regenerar** e um arquivo `MinimalLayout.json` de resposta para regenerar o layout mínimo. Isso será útil se você quiser criar um layout mínimo para uma nova Visual Studio com base no arquivo de resposta do layout mínimo anterior.

   Para esse comando, é necessário um caminho de arquivo de `MinimalLayout.json` um layout já gerado.

   ```shell
   MinimalLayout.exe regenerate --filePath C:\MinimalLayout\MinimalLayout.json
   ```

* **Verificar**: use este comando para determinar se a pasta de layout está corrompida.
* **Correção:** use este comando para corrigir uma pasta de layout corrompida, incluindo a substituição de todos os pacotes ausentes da pasta de layout.

#### <a name="options"></a>Opções

::: moniker range=">=vs-2019"

| Opções                                             | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                 | Obrigatório/Opcional               | Exemplo                                                                                                                                                          |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --targetLocation &lt; dir&gt;                        | Especifica um diretório no qual criar um layout offline mínimo.                                                                                                                                                                                                                                                                                                                                                                          | Obrigatório                        | --targetLocation c:\VSLayout\                                                                                                                                    |
| --baseVersion &lt; version&gt;                       | O layout offline mínimo será gerado a partir desta versão.                                                                                                                                                                                                                                                                                                                                                                    | Obrigatório                        | --baseVersion 16.4.0                                                                                                                                             |
| --targetVersion &lt; version&gt;                     | O layout offline mínimo será gerado até e incluindo esta versão.                                                                                                                                                                                                                                                                                                                                                              | Obrigatório                        | --targetVersion 16.4.4                                                                                                                                           |
| --languages                                         | Especifica os idiomas a incluir no layout offline mínimo. Vários valores podem ser especificados, separados por espaços.                                                                                                                                                                                                                                                                                                                    | Obrigatório                        | --languages en-US fr-FR                                                                                                                                          |
| --productIds &lt; uma ou mais IDs de produto&gt;        | As IDs dos produtos dos quais o layout offline mínimo será gerado, separados por vírgulas. <br> <ul><li>Microsoft.VisualStudio.Product.Enterprise</li><li>Microsoft.VisualStudio.Product.Professional</li><li>Microsoft.VisualStudio.Product.BuildTools</li><li>Microsoft.VisualStudio.Product.TestAgent</li><li>Microsoft.VisualStudio.Product.TestController</li><li>Microsoft.VisualStudio.Product.TeamExplorer</li></ul> | Obrigatório                        | --productIds Microsoft.VisualStudio.Product.Enterprise,Microsoft.VisualStudio.Product.Professional                                                               |
| --filePath                                          | O caminho do arquivo MinimalLayout.jsno arquivo de um layout já criado. Essa opção só é usada com o comando Regenerar.                                                                                                                                                                                                                                                                                                          | Necessário para gerar novamente o comando | --filePath C:\VSLayout\minimalLayout.json <br><br> **Observe que o comando Regenerar só aceita --filePath como uma opção.**                                      |
| --add &lt; one or more workload or component IDs&gt; | Especifica uma ou mais IDs de carga de trabalho ou de componente a adicionar. Componentes adicionais podem ser adicionados globalmente usando --includeRecommended e/ou <br> –-includeOptional. Várias cargas de trabalho ou IDs de componente podem ser especificadas, separadas por um espaço.                                                                                                                                                                                                   | Opcional                        | --add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb Component.GitHub.VisualStudio                                        |
| --includeRecommended                                | Inclui os componentes recomendados para as cargas de trabalho que estão instaladas, mas não os componentes opcionais.                                                                                                                                                                                                                                                                                                                                  | Opcional                        | Para uma carga de trabalho específica: <br> --add Microsoft.VisualStudio.Workload. ManagedDesktop;includeRecommended <br><br> Para aplicar a todas as cargas de trabalho: --includeRecommended |
| --includeOptional                                   | Inclui os componentes opcionais para todas as cargas de trabalho instaladas, incluindo os componentes recomendados.                                                                                                                                                                                                                                                                                                                                | Opcional                        | Para uma carga de trabalho específica: <br>--add Microsoft.VisualStudio.Workload. ManagedDesktop;includeOptional <br><br> Para aplicar a todas as cargas de trabalho: --includeOptional         |

::: moniker-end

::: moniker range="vs-2017"

| Opções                                             | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                 | Obrigatório/Opcional               | Exemplo                                                                                                                                                          |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --targetLocation &lt; dir&gt;                        | Especifica um diretório no qual criar um layout offline mínimo.                                                                                                                                                                                                                                                                                                                                                                          | Obrigatório                        | --targetLocation c:\VSLayout\                                                                                                                                    |
| --baseVersion &lt; version&gt;                       | O layout offline mínimo será gerado a partir desta versão.                                                                                                                                                                                                                                                                                                                                                                    | Obrigatório                        | --baseVersion 15.0.0                                                                                                                                             |
| --targetVersion &lt; version&gt;                     | O layout offline mínimo será gerado até e incluindo esta versão.                                                                                                                                                                                                                                                                                                                                                              | Obrigatório                        | --targetVersion 15.9.31                                                                                                                                          |
| --languages                                         | Especifica os idiomas a incluir no layout offline mínimo. Vários valores podem ser especificados, separados por espaços.                                                                                                                                                                                                                                                                                                                    | Obrigatório                        | --languages en-US fr-FR                                                                                                                                          |
| --productIds &lt; uma ou mais IDs de produto&gt;        | As IDs dos produtos dos quais o layout offline mínimo será gerado, separados por vírgulas. <br> <ul><li>Microsoft.VisualStudio.Product.Enterprise</li><li>Microsoft.VisualStudio.Product.Professional</li><li>Microsoft.VisualStudio.Product.BuildTools</li><li>Microsoft.VisualStudio.Product.TestAgent</li><li>Microsoft.VisualStudio.Product.TestController</li><li>Microsoft.VisualStudio.Product.TeamExplorer</li></ul> | Obrigatório                        | --productIds Microsoft.VisualStudio.Product.Enterprise,Microsoft.VisualStudio.Product.Professional                                                               |
| --filePath                                          | O caminho do arquivo MinimalLayout.jsno arquivo de um layout já criado. Essa opção só é usada com o comando Regenerar.                                                                                                                                                                                                                                                                                                          | Necessário para gerar novamente o comando | --filePath C:\VSLayout\minimalLayout.json <br><br> **Observe que o comando Regenerar só aceita --filePath como uma opção.**                                      |
| --add &lt; one or more workload or component IDs&gt; | Especifica uma ou mais IDs de carga de trabalho ou de componente a adicionar. Componentes adicionais podem ser adicionados globalmente usando --includeRecommended e/ou <br> –-includeOptional. Várias cargas de trabalho ou IDs de componente podem ser especificadas, separadas por um espaço.                                                                                                                                                                                                   | Opcional                        | --add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb Component.GitHub.VisualStudio                                        |
| --includeRecommended                                | Inclui os componentes recomendados para as cargas de trabalho que estão instaladas, mas não os componentes opcionais.                                                                                                                                                                                                                                                                                                                                  | Opcional                        | Para uma carga de trabalho específica: <br> --add Microsoft.VisualStudio.Workload. ManagedDesktop;includeRecommended <br><br> Para aplicar a todas as cargas de trabalho: --includeRecommended |
| --includeOptional                                   | Inclui os componentes opcionais para todas as cargas de trabalho instaladas, incluindo os componentes recomendados.                                                                                                                                                                                                                                                                                                                                | Opcional                        | Para uma carga de trabalho específica: <br>--add Microsoft.VisualStudio.Workload. ManagedDesktop;includeOptional <br><br> Para aplicar a todas as cargas de trabalho: --includeOptional         |

::: moniker-end

### <a name="generating-a-minimal-layout"></a>Gerando um layout mínimo

> [!IMPORTANT]
> Essas instruções pressuem que você criou anteriormente um layout de instalação de rede. Para obter mais informações sobre como fazer isso, consulte a página Criar [uma instalação de Visual Studio](create-a-network-installation-of-visual-studio.md) rede.

Crie um layout mínimo usando o **comando generate** para o intervalo de versões especificado. Você também precisará saber a productId, os idiomas e as cargas de trabalho específicas necessárias. Esse layout mínimo atualizará qualquer Visual Studio da versão base até e incluindo a versão de destino.

Antes de criar o layout, você pode descobrir o tamanho total do download e o número de pacotes incluídos usando o comando **preview.** Esse comando tem as mesmas opções que **o comando generate** e os detalhes são gravados no console.

Vamos ver alguns exemplos de como visualizar, gerar e regenerar um layout mínimo:

::: moniker range=">=vs-2019"

* Primeiro, aqui está um exemplo de como visualizar um layout para Visual Studio Enterprise versões 16.4.0 a 16.4.4 somente para inglês.

  ```shell
  MinimalLayout.exe preview --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --languages en-US
  ```

* Veja como gerar esse mesmo layout com uma carga de trabalho.

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US
  ```

* E veja como regenerar um layout offline mínimo usando um arquivo de resposta existente.

  ```shell
  MinimalLayout.exe regenerate -filepath c:\VSLayout\MinimalLayout.json
  ```

Alguns outros exemplos usando o **comando generate:**

* Veja como adicionar uma carga de trabalho adicional e incluir apenas os pacotes recomendados.

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Professional --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb;includeRecommended --languages en-US
  ```

* Você também pode gerar um layout offline mínimo que dá suporte a vários produtos.

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise,Microsoft.VisualStudio.Product.Professional --baseVersion 16.4.0 --targetVersion 16.4.4 --languages en-US
  ```

* E, por fim, veja como você incluiria vários idiomas em seu layout mínimo.

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US fr-FR
  ```

::: moniker-end

::: moniker range="vs-2017"

* Primeiro, aqui está um exemplo de como visualizar um layout para Visual Studio Enterprise versões 15.0.0 a 15.9.31 somente para inglês.

  ```shell
  MinimalLayout.exe preview --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 15.0.0 --targetVersion 15.9.31 --languages en-US
  ```

* Veja como gerar esse mesmo layout com uma carga de trabalho.

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 15.0.0 --targetVersion 15.9.31 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US
  ```

* E veja como regenerar um layout offline mínimo usando um arquivo de resposta existente.

  ```shell
  MinimalLayout.exe regenerate -filepath c:\VSLayout\MinimalLayout.json
  ```

Alguns outros exemplos usando o **comando generate:**

* Veja como adicionar uma carga de trabalho adicional e incluir apenas os pacotes recomendados.

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Professional --baseVersion 15.0.0 --targetVersion 15.9.31 --add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb;includeRecommended --languages en-US
  ```

* Você também pode gerar um layout offline mínimo que dá suporte a vários produtos.

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise,Microsoft.VisualStudio.Product.Professional --baseVersion 15.0.0 --targetVersion 15.9.31 --languages en-US
  ```

* E, por fim, veja como você incluiria vários idiomas em seu layout mínimo.

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 15.0.0 --targetVersion 15.9.31 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US fr-FR
  ```

::: moniker-end

### <a name="how-to-maintain-a-minimal-layout"></a>Como manter um layout mínimo

Use os **comandos verificar** **e corrigir** para manter o layout mínimo depois que ele é criado. O **comando verify** determina se há pacotes corrompidos ou ausentes no layout mínimo. Se você encontrar problemas depois de executar o **comando verify,** use o comando **de correção** para corrigir os pacotes ausentes ou corrompidos.

* Veja como verificar se um layout tem pacotes corrompidos ou ausentes:

  ```shell
  MinimalLayout.exe Verify --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop --includeRecommended --languages en-US
  ```

* E veja como corrigir esse layout:

  ```shell
  MinimalLayout.exe fix --targetLocation C:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeRecommended --languages en-US
  ```

>[!NOTE]
> Esse layout não pode ser usado para reparar uma Visual Studio instalação. Para reparar uma instância existente do Visual Studio, consulte [Reparar Visual Studio](repair-visual-studio.md).
>

### <a name="how-to-use-a-minimal-offline-layout-to-update-an-existing-installation-of-visual-studio"></a>Como usar um layout offline mínimo para atualizar uma instalação existente do Visual Studio

Depois de gerar um layout mínimo, você pode copiar toda a pasta de layout mínima para um computador cliente. Isso será necessário se o computador não tiver acesso à pasta de layout mínima em seu local original.

Navegue até a pasta e identifique o nome do aplicativo bootstrapper. O nome do aplicativo bootstrapper depende do valor ProductId especificado durante a geração do layout mínimo. Consulte a tabela abaixo para ver exemplos comuns.

| Valor de ProductId                             | Nome do aplicativo    |
|---------------------------------------------|---------------------|
| Microsoft.VisualStudio.Product.Enterprise   | vs_enterprise.exe   |
| Microsoft.VisualStudio.Product.Professional | vs_professional.exe |
| Microsoft.VisualStudio.Product.BuildTools   | vs_buildtools.exe   |

A atualização é aplicada a uma instância do Visual Studio em duas etapas. Comece atualizando o Instalador do Visual Studio e, em seguida, atualize o Visual Studio.

::: moniker range="vs-2017"

1. **Atualizar o Instalador do Visual Studio**

    Execute o comando a seguir, substituindo `vs_enterprise.exe`  pelo nome do aplicativo bootstrapper correto, se necessário.

    ```shell
    vs_enterprise.exe --quiet --update --offline C:\VSLayout\vs_installer.opc
    ```

2. **Atualizar o aplicativo do Visual Studio**

    Para atualizar o Visual Studio, você precisa especificar o installPath da instância do Visual Studio que deseja atualizar. Se várias instâncias do Visual Studio estiverem instaladas, cada uma precisará ser atualizada separadamente. É altamente recomendável que você especifique a `–noWeb` opção com o comando de atualização para impedir a instalação de componentes que não estão no layout mínimo. Isso impede que você deixe o Visual Studio em um estado inutilizável.

    Execute o comando a seguir, substituindo adequadamente o parâmetro de linha de comando installPath. Certifique-se de usar também o nome do aplicativo bootstrapper correto.

    ```shell
    vs_enterprise.exe update --noWeb --quiet --installpath "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise"
    ```

::: moniker-end

::: moniker range="vs-2019"

1. **Atualizar o Instalador do Visual Studio**

    Execute o comando a seguir, substituindo `vs_enterprise.exe`  pelo nome do aplicativo bootstrapper correto, se necessário.

    ```shell
    vs_enterprise.exe --quiet --update --offline C:\VSLayout\vs_installer.opc
    ```

2. **Atualizar o aplicativo do Visual Studio**

    Para atualizar o Visual Studio, você precisa especificar o installPath da instância do Visual Studio que deseja atualizar. Se várias instâncias do Visual Studio estiverem instaladas, cada uma precisará ser atualizada separadamente. É altamente recomendável que você especifique a `–noWeb` opção com o comando de atualização para impedir a instalação de componentes que não estão no layout mínimo. Isso impede que você deixe o Visual Studio em um estado inutilizável.

    Execute o comando a seguir, substituindo adequadamente o parâmetro de linha de comando installPath. Certifique-se de usar também o nome do aplicativo bootstrapper correto.

    ```shell
    vs_enterprise.exe update --noWeb --quiet --installpath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise"
    ```

::: moniker-end

::: moniker range=">=vs-2022"

1. **Atualizar o Instalador do Visual Studio**

    Execute o comando a seguir, substituindo `vs_enterprise.exe`  pelo nome do aplicativo bootstrapper correto, se necessário.

    ```shell
    vs_enterprise.exe --quiet --update --offline C:\VSLayout\vs_installer.opc
    ```

2. **Atualizar o aplicativo do Visual Studio**

    Para atualizar o Visual Studio, você precisa especificar o installPath da instância do Visual Studio que deseja atualizar. Se várias instâncias do Visual Studio estiverem instaladas, cada uma precisará ser atualizada separadamente. É altamente recomendável que você especifique a `–noWeb` opção com o comando de atualização para impedir a instalação de componentes que não estão no layout mínimo. Isso impede que você deixe o Visual Studio em um estado inutilizável.

    Execute o comando a seguir, substituindo adequadamente o parâmetro de linha de comando installPath. Certifique-se de usar também o nome do aplicativo bootstrapper correto.

    ```shell
    vs_enterprise.exe update --noWeb --quiet --installpath "C:\Program Files\Microsoft Visual Studio\2022\Enterprise"
    ```

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [Ferramentas para detectar e gerenciar instâncias do Visual Studio](tools-for-managing-visual-studio-instances.md)
* [Como definir as configurações em um arquivo de resposta](automated-installation-with-response-file.md)
* [Atualizações de controle para implantações do Visual Studio com base em rede](controlling-updates-to-visual-studio-deployments.md)
* [Ciclo de vida do produto Visual Studio e manutenção](/visualstudio/releases/2019/servicing/)
