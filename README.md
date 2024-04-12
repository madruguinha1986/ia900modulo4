# Passo a passso para a criação do modelo.

O [link](https://microsoftlearning-github-io.translate.goog/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html?_x_tr_sl=auto&_x_tr_tl=pt&_x_tr_hl=pt-BR), fornece o passo a passo de como fazer esse laboratório.Quando de sntir meio perdido olhe as imagens no tutorial, pois às vezes os nomes se diferenciam um pouco, no entanto, as imagens permanecem as mesmas, mas claro que não irei me deter a somente isso, iremos nos divertir com as respostas desta incrível ferramenta.

## Passo a passo para se configurar uma pesquisa (resumo):

1. **Crie um recurso do Azure AI Search**

   - Entre no [portal do Azure](https://portal.azure.com/).
   - Clique no botão **+ Criar um recurso**, pesquise Azure AI Search e crie um recurso Azure AI Search com as seguintes configurações:
     - **Assinatura**: sua assinatura do Azure.
     - **Grupo de recursos**: selecione ou crie um grupo de recursos com um nome exclusivo.
     - **Nome do serviço**: um nome exclusivo.
     - **Localização**: Escolha qualquer região disponível.
     - **Nível de preços**: Básico.
   - Selecione **Review + create** e depois de ver a resposta **Validation Success**, selecione **Create**.
   - Após a conclusão da implantação, selecione **Ir para o recurso**. Na página de visão geral do Azure AI Search, você pode adicionar índices, importar dados e pesquisar índices criados.

2. **Crie um recurso de serviços de IA do Azure**

   Você precisará provisionar um recurso de serviços de IA do Azure que esteja no mesmo local que seu recurso do Azure AI Search. Sua solução de pesquisa usará esse recurso para enriquecer os dados no armazenamento de dados com insights gerados por IA.

   - Retorne à página inicial do portal do Azure. Clique no botão **＋Criar um recurso** e pesquise os serviços de IA do Azure. Selecione criar um plano de serviços de IA do Azure. Você será levado a uma página para criar um recurso de serviços de IA do Azure. Configure-o com as seguintes configurações:
     - **Assinatura**: sua assinatura do Azure.
     - **Grupo de recursos**: O mesmo grupo de recursos que seu recurso do Azure AI Search.
     - **Região**: o mesmo local do recurso do Azure AI Search.
     - **Nome**: Um nome exclusivo.
     - **Nível de preços**: Padrão S0.
     - Ao marcar esta caixa, confirmo que li e compreendi todos os termos abaixo: Selecionado.
   - Selecione **Revisar + criar**. Depois de ver a resposta **Validation Passed**, selecione **Create**.
   - Aguarde a conclusão da implantação e visualize os detalhes da implantação.

3. **Crie uma conta de armazenamento**

   - Retorne à página inicial do portal do Azure e selecione o botão **+ Criar um recurso**.
   - Procure conta de armazenamento e crie um recurso de conta de armazenamento com as seguintes configurações:
     - **Assinatura**: sua assinatura do Azure.
     - **Grupo de recursos**: O mesmo grupo de recursos que os recursos do Azure AI Search e dos serviços Azure AI.
     - **Nome da conta de armazenamento**: um nome exclusivo.
     - **Localização**: Escolha qualquer localização disponível.
     - **Padrão de desempenho**.
     - **Redundância**: armazenamento localmente redundante (LRS).
   - Clique em **Revisar** e em **Criar**. Aguarde a conclusão da implantação e vá para o recurso implantado.
   - Na conta de Armazenamento do Azure que você criou, no painel de menu esquerdo, selecione **Configuração (em Configurações)**.
   - Altere a configuração de **Permitir acesso anônimo de Blob** para **Habilitado** e selecione **Salvar**.

4. **Carregar documentos para o armazenamento do Azure**

   - No painel do menu esquerdo, selecione **Containers**.
   - Captura de tela que mostra a página de visão geral do blob de armazenamento.
   - Selecione **+ Contêiner**. Um painel do seu lado direito é aberto.
   - Insira as seguintes configurações e clique em **Criar**:
     - **Nome**: Coffee-Reviews.
     - **Nível de acesso público**: Container (acesso de leitura anônimo para containers e blobs).
     - **Avançado**: sem alterações.
   - Em uma nova guia do navegador, baixe as avaliações de café compactadas em [link](https://aka.ms/mslearn-coffee-reviewse) e extraia os arquivos para a pasta de avaliações.
   - No portal do Azure, selecione o contêiner de avaliações de café. No contêiner, selecione **Carregar**.
   - Captura de tela que mostra o contêiner de armazenamento.
   - No painel **Carregar blob**, selecione **Selecionar um arquivo**.
   - Na janela do Explorer, selecione todos os arquivos na pasta de avaliações, selecione **Abrir** e, em seguida, selecione **Carregar**.
   - Captura de tela que mostra os arquivos carregados no contêiner do Azure.
   - Depois que o upload for concluído, você poderá fechar o painel **Upload blob**. Seus documentos estão agora em seu contêiner de armazenamento de avaliações de café.

5. **Indexar os documentos**

   Depois de armazenar os documentos, você poderá usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um assistente de importação de dados. Com este assistente, você pode criar automaticamente um índice e um indexador para fontes de dados suportadas. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.

   - No portal do Azure, navegue até o recurso Azure AI Search. Na página **Visão geral**, selecione **Importar dados**.
   - Captura de tela que mostra o assistente de importação de dados.
   - Na página **Conectar-se aos seus dados**, na lista **Fonte de Dados**, selecione **Azure Blob Storage**. Preencha os detalhes do armazenamento de dados com os seguintes valores:
     - **Fonte de dados**: Armazenamento de Blobs do Azure.
     - **Nome da fonte de dados**: coffee-customer-data.
     - **Dados a extrair**: Conteúdo e metadados.
     - **Modo de análise**: Padrão.
     - **Cadeia de conexão**: *Selecione Escolha uma conexão existente*. Selecione sua conta de armazenamento, selecione o contêiner de avaliações de café e clique em **Selecionar**.
     - **Autenticação de identidade gerenciada**: Nenhuma.
     - **Nome do contêiner**: esta configuração é preenchida automaticamente depois que você escolhe uma conexão existente.
     - **Pasta Blob**: deixe em branco.
     - **Descrição**: Avaliações sobre Fourth Coffee Shops.
   - Selecione **Próximo: Adicionar habilidades cognitivas (opcional)**.
   - Na seção **Anexar Serviços Cognitivos**, selecione o seu recurso de serviços Azure AI.
   - Na seção **Adicionar enriquecimentos**, altere o nome da qualificação para coffee-skillset.
   - Marque a caixa de seleção **Habilitar OCR e mesclar todo o texto no campo merged_content**.
   - Certifique-se de que o campo **Dados de origem** esteja configurado como merged_content.
   - Altere o nível de granularidade de enriquecimento para **Páginas (blocos de 5.000 caracteres)**.
   - Não selecione **Habilitar enriquecimento incremental**.
   - Selecione os seguintes campos enriquecidos:
  
   - 
     | Habilidade Cognitiva       | Parâmetro | Nome do campo   |
     |----------------------------|-----------|-----------------|
       | Extraia nomes de locais   |           | Localizações    |
       | Extraia frases-chave      |           | Frases Chave    |
       | Detectar sentimento       |           | Sentimento      |
       | Gerar tags de imagens     |           | ImagemTags      |
       | Gere legendas de imagens  |           | Legenda da Imagem|

   - Em **Salvar enriquecimentos em um armazenamento de conhecimento**, selecione:
     - Projeções de imagem
     - Documentos
     - Páginas
     - Frases chave
     - Entidades
     - Detalhes da imagem
     - Referências de imagem.

...

7. **Revise o armazenamento de conhecimento**

   Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o assistente Importar dados, você também criou um armazenamento de conhecimento. Dentro do armazenamento de conhecimento, você encontrará os dados enriquecidos extraídos pelas habilidades de IA que persistem na forma de projeções e tabelas.

   - No portal do Azure, navegue de volta para a sua conta de armazenamento do Azure.
   - No painel do menu esquerdo, selecione **Containers**. Selecione o contêiner de armazenamento de conhecimento.
   - Selecione qualquer um dos itens e clique no arquivo **objectprojection.json**.
   - Selecione **Editar** para ver o JSON produzido para um dos documentos do seu armazenamento de dados do Azure.
   - Selecione a localização atual do blob de armazenamento no canto superior esquerdo da tela para retornar à conta de armazenamento Containers.
   - Em **Containers**, selecione o contêiner **coffee-skillset-image-projection**. Selecione qualquer um dos itens.
   - Selecione qualquer um dos arquivos **.jpg**. Selecione **Editar** para ver a imagem armazenada no documento. Observe como todas as imagens dos documentos são armazenadas desta forma.
   - Selecione a localização atual do blob de armazenamento no canto superior esquerdo da tela para retornar à conta de armazenamento Containers.
   - Selecione **Navegador de armazenamento** no painel esquerdo e selecione **Tabelas**. Há uma tabela para cada entidade no índice. Selecione a tabela **coffeeSkillsetKeyPhrases**.

8. **Saiba mais:**
   [Saiba mais aqui](https://translate.google.com/website?sl=auto&tl=pt&hl=pt-BR&u=https://learn.microsoft.com/azure/search)



     






  

    



 



