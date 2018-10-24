
1. Feche e reabra o Console de gerenciamento do IIS para mostrar as opções de configuração atualizadas na interface do usuário.

2. No IIS, clique com botão direito do **Site padrão**, escolha **implantar** > **configurar Web implantar publicação**.

    ![Definir a configuração de implantação da Web](../../deployment/media/tutorial-configure-web-deploy-publishing.png)

3. No **configurar Web implantar publicação** caixa de diálogo caixa, examine as configurações.

4. Clique em **instalação**.

    No **resultados** painel, a saída mostra que os direitos de acesso é concedida ao usuário especificado e que um arquivo com um *publishsettings* extensão de arquivo foi gerada no local mostrado na caixa de diálogo caixa.

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

    Dependendo da configuração do Windows Server e o IIS, você verá diferentes valores no arquivo XML. Aqui estão alguns detalhes sobre os valores que você vê:

   * O *msdeploy.axd* arquivo referenciado no `publishUrl` atributo é um arquivo de manipulador HTTP gerado dinamicamente para a implantação da Web. (Para fins de teste `http://myhostname:8172` geralmente funciona bem.)
   * O `publishUrl` porta é definida para a porta 8172, que é o padrão para a implantação da Web.
   * O `destinationAppUrl` porta é definida para a porta 80, que é o padrão para o IIS.
   * Se você não conseguir se conectar ao host remoto no Visual Studio usando o nome do host (em etapas posteriores), teste o endereço IP no lugar do nome de host.

     > [!NOTE]
     > Se você estiver publicando para IIS em execução em uma VM do Azure, você deve abrir as portas do IIS e a implantação da Web no grupo de segurança de rede. Para obter informações detalhadas, consulte [instalar e executar o IIS](/azure/virtual-machines/windows/quick-create-portal#open-port-80-for-web-traffic).

5. Copie esse arquivo para o computador onde você está executando o Visual Studio.
