
1. Feche e reabra o Console de gerenciamento do IIS para mostrar opções de configuração atualizadas na interface do usuário.

2. No IIS, clique com o botão direito do mouse em **Site Padrão**, escolha **Implantar** > **Configurar publicação da Implantação da Web**.

    ![Definir a configuração da Implantação da Web](../../deployment/media/tutorial-configure-web-deploy-publishing.png)

3. Na caixa de diálogo **Configurar publicação da Implantação da Web**, examine as configurações.

4. Clique em **Configuração**.

    No painel **Resultados**, a saída mostra que os direitos de acesso foram concedidos ao usuário especificado e que um arquivo com uma extensão *.publishsettings* foi gerado na localização mostrada na caixa de diálogo.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <publishData>
      <publishProfile
        publishUrl="https://myhostname:8172/msdeploy.axd"
        msdeploySite="Default Web Site"
        destinationAppUrl="http://myhostname:80/"
        mySQLDBConnectionString=""
        SQLServerDBConnectionString=""
        profileName="Default Settings"
        publishMethod="MSDeploy"
        userName="myhostname\myusername" />
    </publishData>
    ```

    Dependendo da configuração do Windows Server e do IIS, você verá diferentes valores no arquivo XML. Veja alguns detalhes sobre os valores que você vê:

   * O arquivo *msdeploy.axd* referenciado no atributo `publishUrl` é um arquivo de manipulador HTTP gerado dinamicamente para a Implantação da Web. (Para fins de teste `http://myhostname:8172` geralmente também funciona).
   * A porta `publishUrl` é definida como a porta 8172, que é a padrão para a Implantação da Web.
   * A porta `destinationAppUrl` é definida como a porta 80, que é a padrão para o IIS.
   * Se você não conseguir se conectar ao host remoto no Visual Studio usando o nome do host (nas etapas posteriores), teste o endereço IP no lugar do nome de host.

     > [!NOTE]
     > Se você estiver publicando no IIS em execução em uma VM do Azure, será necessário abrir as portas do IIS e da Implantação da Web no grupo de Segurança de Rede. Para obter informações detalhadas, confira [Instalar e executar o IIS](/azure/virtual-machines/windows/quick-create-portal#open-port-80-for-web-traffic).

5. Copie esse arquivo para o computador em que você está executando o Visual Studio.
