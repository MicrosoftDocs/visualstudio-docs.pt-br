---
title: Workspaces R
description: Como controlar onde o código R é executado usando workspaces no Visual Studio.
ms.date: 01/24/2018
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: 11b5086c934b433d4e28095c1d50471ea44e15a8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49919293"
---
# <a name="control-where-r-code-runs-with-workspaces"></a>Controlar onde o código R é executado com workspaces

Um workspace nas RTVS (Ferramentas do R para Visual Studio) permite configurar onde uma sessão do R é executada, o que pode ocorrer em computadores locais e remotos. A meta é permitir que você trabalhe com uma experiência de usuário semelhante, que ofereça a capacidade de usufruir de computadores baseados em nuvem possivelmente mais poderosos.

Para abrir a janela **Workspaces**, use o comando **Ferramentas do R** > **Windows** > **Workspaces** ou pressione **Ctrl**+**9**.

![Janela de workspaces nas Ferramentas do R para Visual Studio (VS2017)](media/workspaces-window.png)

Nessa janela, a marca de seleção verde indica o workspace ativo ao qual as RTVS estão associadas. Selecionar uma seta azul define o workspace ativo. O ícone de configurações (engrenagem) à direita de cada workspace permite que você altere os argumentos de linha de comando, o local e o nome. O X vermelho remove um workspace adicionado manualmente.

## <a name="save-and-reset-a-workspace"></a>Salvar e redefinir um workspace

Por padrão, as RTVS não salvam o estado do workspace quando você fecha e reabre um projeto. No entanto, você pode alterar esse comportamento por meio das [Opções de workspace](options-for-r-tools-in-visual-studio.md#workspace).

O comando **Ferramentas do R** > **Sessão** > **Redefinir** e o botão de barra de ferramentas de redefinição na janela interativa também redefinem o estado do workspace a qualquer momento. Com workspaces remotos, a redefinição exclui o perfil do usuário criado na primeira conexão com o servidor remoto, o que exclui efetivamente todos os arquivos que foram acumulados lá.

## <a name="local-workspaces"></a>Workspaces locais

A lista de workspaces locais exibe todos os interpretadores de R instalados em seu computador. 

Quando o Visual Studio é iniciado, ele tenta detectar automaticamente todas as versões do R que você instalou, examinando a chave do Registro **HKEY_LOCAL_MACHINE\Software\R-Core\\**. Como essa verificação é feita apenas na inicialização, você precisará reiniciar o Visual Studio se instalar um novo interpretador de R.

As RTVS não podem detectar um interpretador de R que é instalado de maneira não padrão (por exemplo, simplesmente ao copiar arquivos para uma pasta em vez de executar um instalador). Nesse caso, crie manualmente um novo Workspace do R local da seguinte maneira:

1. Selecione o botão **Adicionar** na janela de workspaces.
1. Insira um nome para o novo Workspace.
1. Insira o caminho para a pasta raiz do R, que é aquela que contém a pasta *bin* com o interpretador, juntamente com todos os argumentos de linha de comando opcionais a serem passados para o interpretador quando as RTVS o iniciarem.
1. Selecione **Salvar** quando terminar.

![Adicionando um novo workspace](media/workspaces-add-new.png)

## <a name="remote-workspaces"></a>Workspaces remotos

Os workspaces remotos permitem que você se conecte a uma sessão do R em um computador remoto. (Confira [Configurar workspaces remotos](setting-up-remote-r-workspaces.md) para saber como configurar um computador para essa finalidade.)

O Visual Studio não detecta os workspaces remotos automaticamente, você deve adicioná-los manualmente usando o botão **Adicionar** na janela Workspaces, conforme descrito na seção anterior. Nesse caso, insira o URI do computador remoto, em vez de um caminho local.

> [!Important]
> Workspaces remotos são identificados por um URI que *deve usar o protocolo HTTPS* para garantir a privacidade e a integridade da comunicação com o computador remoto. O Visual Studio não pode se conectar a um computador remoto que não dá suporte a HTTPS.

> [!Note]
> Os workspaces remotos estão efetivamente na visualização. Estamos trabalhando em uma implementação melhor do problema de sincronização de arquivo para uma versão futura e são bem-vindas suas ideias e comentários.

## <a name="remote-workspace-logon"></a>Logon em Workspace Remoto

Você deve usar um nome de usuário e senha para fazer logon no workspace remoto.

### <a name="logon-to-windows-workspace"></a>Logon no workspace do Windows

Se seu computador remoto estiver configurado para usar a conta de domínio, você poderá usar o logon do domínio para acessar um workspace remoto. Se não estiver, você deverá usar o formato `machine-name\username` para fazer logon com uma conta de computador no computador remoto.

### <a name="logon-to-linux-workspace"></a>Logon em workspace do Linux

Para fazer logon em uma conta do Linux, use o formato `<<unix>>\username`. Por exemplo, se você tem uma conta com o nome `ruser`, você deverá digitar o nome de usuário como `<<unix>>\ruser`.

## <a name="switch-between-workspaces"></a>Alternar entre workspaces

As RTVS estão associadas a apenas um workspace por vez. O workspace associado é indicado por uma marca de seleção verde pequena na janela de Workspaces. Por padrão, as RTVS são associadas ao último workspace local aberto em uma sessão anterior.

Para alterar o workspace ativo, selecione a seta azul ao lado do workspace desejado. Isso avisa para salvar sua sessão, encerra o workspace atual e alterna para o novo.

> [!Tip]
> Para desabilitar prompt de salvamento, selecione o comando **Ferramentas do R** > **Opções** e defina a opção **Mostrar caixa de diálogo de confirmação antes de alternar entre workspaces** como `No`. Consulte [Opções de workspace](options-for-r-tools-in-visual-studio.md#workspace).

Se você tentar mudar para um workspace local que foi desinstalado ou para um workspace remoto indisponível, as RTVS podem não ser associadas a nenhum workspace. Como resultado, você pode ver um erro ao inserir o código na janela interativa ou tentar executar o código de outro modo:

![Erro quando não há nenhum workspace associado às RTVS](media/workspaces-disconnected-interactive-window.png)

Para corrigir isso, mude para outro workspace na janela Workspaces. Se não houver nenhum workspace disponível, você precisará instalar um interpretador de R. Você também poderá tentar reiniciar o Visual Studio se ele estava em execução quando você instalou um interpretador.

### <a name="switch-to-a-remote-workspace"></a>Alternar para um workspace remoto

As RTVS solicitam credenciais quando você se conecta pela primeira vez a um workspace remoto, em seguida, armazena em cache as credenciais (usando o Cofre de Credenciais seguro do Windows) para as sessões posteriores. A comunicação com o servidor remoto, em seguida, é feita com segurança em HTTPS (o que é necessário).

Dependendo da configuração do servidor, você verá um aviso de certificado ao conectar-se dizendo "O certificado de segurança apresentado pelos serviços remotos do R não permite provar que você realmente está conectado ao computador (nome)."

![Aviso do certificado autoassinado ao conectar-se a um workspace remoto](media/workspaces-remote-self-signed-certificate-warning.png)

O certificado é um documento apresentado às RTVS pelo computador ao qual você está tentando se conectar. O certificado contém um campo que identifica o URI do computador. O aviso é exibido quando as RTVS detectam uma incompatibilidade entre o URI no certificado e o URI usado para se conectar ao computador, indicando que segurança do servidor pode ter sido comprometida.

No entanto, esse aviso também será exibido se um *certificado autoassinado* tiver sido usado para habilitar o HTTPS no computador remoto em vez de usar outro de um provedor confiável. Para obter mais informações, confira [Configurar workspaces remotos](setting-up-remote-r-workspaces.md).

## <a name="directories-on-local-and-remote-computers"></a>Diretórios em computadores locais e remotos

Por padrão, quando você inicia um novo interpretador de R em um workspace local, o diretório de trabalho atual é *%userprofile%\Documents*. Você pode alterar o diretório a qualquer momento usando os comandos **Ferramentas do R** > **Diretório de Trabalho** ou clicando com o botão direito do mouse em um projeto no Gerenciador de Soluções do Visual Studio e selecionando comandos como **Definir Diretório de Trabalho Aqui**.

Quando você se conecta pela primeira vez a um computador remoto, as RTVS criam automaticamente um perfil do usuário com base em suas credenciais, o que configura o diretório de trabalho para a pasta *Documentos* nesse perfil. Essa pasta será usada para todas as sessões remotas subsequentes que usam as mesmas credenciais.

Como resultado, o local exato em que seu código é executado pode diferir entre workspaces locais e remotos. No seu código, sempre use caminhos relativos para os arquivos de dados e assim por diante para que seu código seja portátil entre os workspaces.

Observe também que com os workspaces remotos, todos os arquivos no diretório de trabalho permanecerão em vigor em sessões para o mesmo perfil do usuário. Conforme observado anteriormente, você pode excluir esses arquivos usando o comando **Ferramentas do R** > **Sessão** > **Redefinir** (ou no botão Redefinir na janela interativa) ao usar um workspace remoto. Novamente, esse comando exclui o perfil do usuário do servidor, que é recriado quando você se conecta novamente.

## <a name="copy-project-files-to-remote-workspaces"></a>Copiar arquivos de projeto para workspaces remotos

Ao trabalhar com projetos R no Visual Studio, o computador local sempre tem os arquivos de projeto mais recentes, mesmo quando você está usando um workspace remoto. Ou seja, quando você abre um projeto no Visual Studio (que normalmente significa abrir uma solução que contém o projeto), as RTVS supõem que o conteúdo do projeto reside inteiramente no computador local. O workspace remoto é, na verdade, apenas um host temporário para os arquivos do projeto e as saídas do código. Isso significa, por exemplo, que ao carregar um arquivo usando `source` na janela interativa, esse arquivo já deve estar no computador remoto no caminho fornecido ou deve estar no diretório de trabalho atual do interpretador de R remoto (definido com a função `setwd()`).

Os arquivos são copiados para o servidor remoto da seguinte maneira:

- Para trabalhar com arquivos remotamente usando a janela interativa, primeiro é necessário copiá-los manualmente clicando com o botão direito do mouse nesses arquivos (ou no projeto) no Gerenciador de Soluções e selecionando **Origem Selecionada**. Para arquivos individuais, eles são copiados para o diretório de trabalho no servidor. Ao copiar um projeto, as RTVS criam uma pasta para o projeto.

- Você também pode copiar arquivos selecionando-os no Gerenciador de Soluções e escolhendo **Arquivos de Origem Selecionados**. Essa ação os carrega na janela interativa e os executa lá. Se a sessão está conectada a um computador remoto, os arquivos são copiados lá primeiro.

- Quando as RTVS estiverem associadas a um workspace remoto e você pressionar **F5**, selecionar **Depurar** > **Iniciar Depuração** ou iniciar a execução do código de outro modo, as RTVS, por padrão, copiarão o arquivo do projeto para o workspace remoto automaticamente (veja abaixo como controlar esse comportamento).

- Todos os arquivos que já existem no servidor são substituídos.

> [!Note]
> Como as RTVS não podem interceptar todas as chamadas de função do R com confiança, as chamadas de funções como `source()` ou `runApp()` (para aplicativos Shiny) na janela interativa *não* copiam arquivos para o workspace remoto.

As [Propriedades do projeto](r-projects-in-visual-studio.md#project-properties) controlam se o RTVS copia arquivos quando o projeto é executado e exatamente quais arquivos são copiados. Para abrir esta página, selecione o comando de menu **Projeto** > **Propriedades do (nome)** ou clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Propriedades**.

![Guia de execução de propriedades do projeto com configurações de transferência de arquivo](media/workspaces-remote-file-transfer-filter-settings.png)

Aqui, a propriedade **Transferir arquivos em execução** determina se as RTVS copiam os arquivos do projeto automaticamente. O valor de **Arquivos para transferir** filtra exatamente quais arquivos são transferidos. O padrão é copiar somente os arquivos *.R*, *.Rmd*, *.sql*, *.md* e *.cpp*. Esse comportamento é feito para evitar a cópia acidental de grandes arquivos de dados para o servidor em todas as execuções. 

## <a name="copy-files-from-a-remote-workspace"></a>Copiar arquivos de um workspace remoto

Se o seu script R gera arquivos no servidor, você pode copiar esses arquivos de volta para o cliente usando a função `rtvs::fetch_file`. Essa função aceita, no mínimo, o caminho remoto para o arquivo que você deseja copiar para o computador e, opcionalmente, o caminho de destino em seu computador. Se você não especificar um caminho, o arquivo será copiado na pasta *%userprofile%\Downloads*.
