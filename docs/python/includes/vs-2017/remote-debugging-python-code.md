---
title: Depurar o código Python em computadores Linux remotos
description: Use o Visual Studio para depurar o código Python em execução em computadores Linux remotos, incluindo as etapas de configuração necessárias, segurança e solução de problemas.
ms.date: 12/06/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 82c22143f70bc53a358cd25e6ff2ad91eff1e2e9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541058"
---
O Visual Studio pode iniciar e depurar aplicativos Python localmente e remotamente em um computador Windows (consulte [depuração remota](../../../debugger/remote-debugging.md)). Ela também pode depurar remotamente em um dispositivo ou sistema operacional diferente ou em uma implementação Python que não seja o CPython usando a [biblioteca ptvsd](https://pypi.python.org/pypi/ptvsd).

Ao usar a ptvsd, o código do Python que está sendo depurado hospeda o servidor de depuração ao qual o Visual Studio pode se anexar. Essa hospedagem exige uma pequena modificação no código para importar e habilitar o servidor e pode exigir configurações de rede ou de firewall no computador remoto para permitir conexões TCP.

|   |   |
|---|---|
| ![ícone de câmera para vídeo](../../../install/media/video-icon.png "Assistir a um vídeo") | Para obter uma introdução à depuração remota, consulte [aprofundamento: depuração remota de plataforma cruzada](https://youtu.be/y1Qq7BrV6Cc) (YouTube.com, 6m22s), que se aplica ao Visual Studio 2015 e 2017. |

## <a name="set-up-a-linux-computer"></a>Configurar um computador Linux

Os itens a seguir são necessários para acompanhar esse passo a passo:

- Um computador remoto que execute o Python em um sistema operacional como o Mac OSX ou Linux.
- A porta 5678 (entrada) aberta no firewall desse computador, que é o padrão para a depuração remota.

Crie com facilidade uma [máquina virtual do Linux no Azure](/azure/virtual-machines/linux/creation-choices) e [acesse-a usando a Área de Trabalho Remota](/azure/virtual-machines/linux/use-remote-desktop) no Windows. Ter o Ubuntu para a VM é conveniente, pois o Python é instalado por padrão. Caso contrário, veja a lista em [Instalar um interpretador do Python de sua escolha](../../installing-python-interpreters.md) para obter mais locais de download do Python.

Para obter detalhes sobre como criar uma regra de firewall para uma VM do Azure, confira [Abrir portas para uma VM no Azure usando o portal do Azure](/azure/virtual-machines/windows/nsg-quickstart-portal).

## <a name="prepare-the-script-for-debugging"></a>Preparar o script para depuração

1. No computador remoto, crie um arquivo do Python chamado *guessing-game.py* com o seguinte código:

    ```python
    import random

    guesses_made = 0
    name = input('Hello! What is your name?\n')
    number = random.randint(1, 20)
    print('Well, {0}, I am thinking of a number between 1 and 20.'.format(name))

    while guesses_made < 6:
        guess = int(input('Take a guess: '))
        guesses_made += 1
        if guess < number:
            print('Your guess is too low.')
        if guess > number:
            print('Your guess is too high.')
        if guess == number:
            break
    if guess == number:
        print('Good job, {0}! You guessed my number in {1} guesses!'.format(name, guesses_made))
    else:
        print('Nope. The number I was thinking of was {0}'.format(number))
    ```

1. Instale o pacote `ptvsd` no ambiente usando `pip3 install ptvsd`.
   >[!NOTE]
   >É uma boa ideia registrar a versão do ptvsd instalada caso ela seja necessária para solução de problemas; a [listagem ptvsd](https://pypi.python.org/pypi/ptvsd) também mostra as versões disponíveis.

1. Habilite a depuração remota adicionando o código abaixo ao primeiro ponto possível de *guessing-game.py*, antes de outros códigos. (Embora esse não seja um requisito estrito, é impossível depurar os threads em segundo plano gerados antes que a função `enable_attach` seja chamada.)

   ```python
   import ptvsd
   ptvsd.enable_attach()
   ```

1. Salve o arquivo e execute `python3 guessing-game.py`. A chamada para `enable_attach` é executada em segundo plano e aguarda as conexões de entrada enquanto você interage com o programa de outra maneira. Se desejado, a função `wait_for_attach` pode ser chamada após `enable_attach` para bloquear o programa até que o depurador seja anexado.

> [!Tip]
> Além de `enable_attach` e `wait_for_attach`, o ptvsd também fornece uma função auxiliar `break_into_debugger`, que serve como um ponto de interrupção programático, caso o depurador seja anexado. Também há uma função `is_attached` que retorna `True` se o depurador é anexado (observe que não há necessidade de verificar esse resultado antes de chamar outras funções `ptvsd`).

## <a name="attach-remotely-from-python-tools"></a>Anexar remotamente por meio das Ferramentas Python

Nestas etapas, definiremos um ponto de interrupção simples para interromper o processo remoto.

1. Crie uma cópia do arquivo remoto no computador local e abra-a no Visual Studio. Não importa a localização do arquivo, mas o nome deve corresponder ao nome do script no computador remoto.

1. (Opcional) Para ter o IntelliSense para ptvsd no computador local, instale o pacote de ptvsd em seu ambiente de Python.

1. Selecione **depuração**  >  **anexar ao processo**.

1. No diálogo **Anexar ao Processo** que será exibido, configure o **Tipo de Conexão** como **Python remoto (ptvsd)**. (Em versões anteriores do Visual Studio, esses comandos são denominados **Transporte** e **Depuração remota do Python**.)

1. No campo **Destino da Conexão** (**Qualificador** em versões anteriores), insira `tcp://<ip_address>:5678`, em que `<ip_address>` é o do computador remoto (que pode ser um endereço explícito ou um nome como myvm.cloudapp.net) e `:5678` é o número da porta de depuração remota.

1. Pressione **Enter** para preencher a lista de processos de ptvsd disponíveis nesse computador:

    ![Inserir o destino da conexão e listar processos](../../media/remote-debugging-qualifier.png)

    Se outro programa for iniciado no computador remoto após a lista ser populada, selecione o botão **Atualizar**.

1. Selecione o processo a ser depurado e, em seguida, **Anexar** ou clique duas vezes no processo.

1. Então, o Visual Studio alternará para o modo de depuração enquanto o script continuará a ser executado no computador remoto, fornecendo todos os recursos normais de [depuração](../../debugging-python-in-visual-studio.md). Por exemplo, defina um ponto de interrupção na linha `if guess < number:` e, em seguida, mude para o computador remoto e insira outra tentativa. Após fazer isso, o Visual Studio do seu computador local parará no ponto de interrupção, mostrará variáveis locais e assim por diante:

    ![O Visual Studio pausa a depuração quando um ponto de interrupção é atingido](../../media/remote-debugging-breakpoint-hit.png)

1. Ao interromper a depuração, o Visual Studio se desanexa do programa, que continua a ser executado no computador remoto. O ptvsd também continua a escuta para anexar depuradores, assim, é possível anexá-los novamente ao processo a qualquer momento.

### <a name="connection-troubleshooting"></a>Solução de problemas de conexão

1. Verifique se você selecionou **Python remoto (ptvsd)** para o **Tipo de Conexão** (**Depuração remota do Python** de **Transporte** em versões anteriores).
1. Verifique se o segredo no **Destino de Conexão** (ou **Qualificador**) corresponde exatamente ao segredo no código remoto.
1. Verifique se o endereço IP no **Destino de Conexão** (ou **Qualificador**) corresponde ao do computador remoto.
1. Verifique se a porta de depuração remota foi aberta no computador remoto e se o sufixo da porta foi incluído no destino de conexão, como `:5678`.
    - Se for necessário usar uma porta diferente, será possível especificá-la na chamada `enable_attach` usando o argumento `address`, como em `ptvsd.enable_attach(address = ('0.0.0.0', 8080))`. Nesse caso, abra a porta específica no firewall.
1. Verifique na tabela a seguir se a versão do ptvsd instalada no computador remoto conforme retornado por `pip3 list` corresponde àquela utilizada pela versão das ferramentas do Python usadas no Visual Studio. Se necessário, atualize o ptvsd no computador remoto.

    | Versão do Visual Studio | Versão das ferramentas do Python/ptvsd |
    | --- | --- |
    | 2017 15.8 | 4.1.1a9 (depurador herdado: 3.2.1.0) |
    | 2017 15.7 | 4.1.1a1 (depurador herdado: 3.2.1.0) |
    | 2017 15.4, 15.5, 15.6 | 3.2.1.0 |
    | 2017 15.3 | 3.2.0 |
    | 2017 15.2 | 3.1.0 |
    | 2017 15.0, 15.1 | 3.0.0 |
    | 2015 | 2.2.6 |
    | 2013 | 2.2.2 |
    | 2012, 2010 | 2.1 |

## <a name="using-ptvsd-3x"></a>Usar ptvsd 3.x

As informações a seguir aplicam-se apenas à depuração remota com o ptvsd 3.x, que contém alguns recursos que foram removidos do ptvsd 4.x.

1. Com o ptvsd 3.x, a função `enable_attach` exigia que você passasse um "segredo" como o primeiro argumento que restringe o acesso para o script em execução. Você insere o segredo ao anexar o depurador remoto. Embora não seja recomendado, é possível permitir que qualquer pessoa se conecte, use `enable_attach(secret=None)`.

1. A URL de destino de conexão é `tcp://<secret>@<ip_address>:5678`, em que `<secret>` é a cadeia de caracteres passada, `enable_attach`, no código do Python.

Por padrão, a conexão com o servidor de depuração remota ptvsd 3.x é protegida somente pelo segredo e todos os dados são passados em texto sem formatação. Para obter uma conexão mais segura, o ptvsd 3.x dá suporte ao uso do SSL com o protocolo `tcsp`, que você configura da seguinte maneira:

1. No computador remoto, gere certificados autoassinados separados e arquivos de chave usando o openssl:

    ```command
    openssl req -new -x509 -days 365 -nodes -out cert.cer -keyout cert.key
    ```

    Quando solicitado, use o nome do host ou endereço IP (o que você usa para se conectar) no **Nome Comum** quando solicitado pelo openssl.

    (Consulte [Certificados autoassinados](https://docs.python.org/3/library/ssl.html#self-signed-certificates) nos documentos de módulo `ssl` do Python para obter mais detalhes. Observe que o comando nesses documentos gera apenas um único arquivo combinado.)

1. No código, modifique a chamada para `enable_attach` a fim de incluir os argumentos `certfile` e `keyfile` usando os nomes de arquivo como valores (esses argumentos têm o mesmo significado que a função padrão `ssl.wrap_socket` do Python):

    ```python
    ptvsd.enable_attach(secret='my_secret', certfile='cert.cer', keyfile='cert.key')
    ```

    Também é possível fazer essa mesma alteração no arquivo de código no computador local, porém, como esse código não é executado, isso não é realmente necessário.

1. Reinicie o programa de Python no computador remoto, deixando-o pronto para depuração.

1. Proteja o canal adicionando o certificado à AC Raiz Confiável no computador Windows com o Visual Studio:

    1. Copie o arquivo de certificado do computador remoto para o computador local.
    1. Abra o **Painel de Controle** e navegue para **Ferramentas Administrativas** > **Gerenciar certificados de computador**.
    1. Na janela exibida, expanda **Autoridades de Certificação Confiáveis** no lado esquerdo, clique com o botão direito do mouse em **Certificados** e selecione **Todas as Tarefas** > **Importar**.
    1. Navegue para o arquivo *.cer* copiado do computador remoto, selecione-o e, em seguida, clique nas caixas de diálogo para concluir a importação.

1. Agora, repita o processo de anexação no Visual Studio, conforme descrito anteriormente, usando `tcps://` como protocolo para o **Destino de Conexão** (ou **Qualificador**).

    ![Escolhendo o transporte de depuração remota com SSL](../../media/remote-debugging-qualifier-ssl.png)

1. O Visual Studio o avisará sobre possíveis problemas de certificado ao se conectar via SSL. É possível ignorar os avisos e continuar, porém, embora o canal ainda esteja criptografado contra interceptação, ele pode estar aberto a ataques man-in-the-middle.

    1. Se você vir o **certificado remoto não é** um aviso de confiança abaixo, isso significa que você não adicionou corretamente o certificado à autoridade de certificação raiz confiável. Verifique essas etapas e tente novamente.

        ![Aviso de certificado SSL confiável](../../media/remote-debugging-ssl-warning.png)

    1. Se você vir o **nome do certificado remoto não corresponder ao** aviso de hostname abaixo, isso significa que você não usou o nome de host ou endereço IP adequado como o **common name** ao criar o certificado.

        ![Aviso de nome de host do certificado SSL](../../media/remote-debugging-ssl-warning2.png)
