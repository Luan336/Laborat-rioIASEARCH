# Laborat-rioIASEARCH

Laboratório para Criar ferramenta do IA Search

Resultado da Pesquisa

![Uploading image.png…]()


Criar um recurso do Azure AI Search
Entre no portal do Azure.

Clique no botão + Criar um recurso, pesquise Azure AI Search e crie um recurso Azure AI Search com as seguintes configurações:

Assinatura: sua assinatura do Azure.
Grupo de recursos: selecione ou crie um grupo de recursos com um nome exclusivo.
Nome do serviço: um nome exclusivo.
Local: escolha qualquer região disponível. Se estiver no leste dos EUA, use "Leste dos EUA 2".
Tipo de preço: Básico
Selecione Examinar + criar e, depois de ver a resposta Validação bem-sucedida, selecione Criar.

Após a conclusão da implantação, selecione Ir para o recurso. Na página de visão geral do Azure AI Search, você pode adicionar índices, importar dados e pesquisar índices criados.

Criar um recurso de serviços de IA do Azure
Você precisará provisionar um recurso de serviços de IA do Azure que esteja no mesmo local que o recurso de Pesquisa de IA do Azure. Sua solução de pesquisa usará esse recurso para enriquecer os dados no armazenamento de dados com insights gerados por IA.

Retorne à home page do portal do Azure. Clique no botão +Criar um recurso e pesquise os serviços de IA do Azure. Selecione criar um plano de serviços de IA do Azure. Você será levado a uma página para criar um recurso de serviços de IA do Azure. Configure-o com as seguintes configurações:
Assinatura: sua assinatura do Azure.
Grupo de recursos: o mesmo grupo de recursos que o recurso do Azure AI Search.
Região: o mesmo local que o recurso do Azure AI Search.
Nome: Um nome exclusivo.
Tipo de preço: Standard S0
Ao marcar esta caixa, reconheço que li e entendi todos os termos abaixo: Selecionado
Selecione Examinar + criar. Depois de ver a resposta Validação aprovada, selecione Criar.

Aguarde a conclusão da implantação e exiba os detalhes da implantação.
Criar uma conta de armazenamento
Retorne à home page do portal do Azure e selecione o botão + Criar um recurso.

Pesquise a conta de armazenamento e crie um recurso de conta de armazenamento com as seguintes configurações:
Assinatura: sua assinatura do Azure.
Grupo de recursos: o mesmo grupo de recursos que os recursos do Azure AI Search e dos serviços de IA do Azure.
Nome da conta de armazenamento: um nome exclusivo.
Local: escolha qualquer local disponível.
Desempenho: Padrão
Redundância: LRS (armazenamento com redundância local)
Clique em Revisar e, em seguida, clique em Criar. Aguarde a conclusão da implantação e vá para o recurso implantado.

Na conta de Armazenamento do Azure que você criou, no painel de menu à esquerda, selecione Configuração (em Configurações).
Altere a configuração de Permitir acesso anônimo ao Blob para Habilitado e selecione Salvar.
Carregar documentos no Armazenamento do Azure
No painel de menu à esquerda, selecione Contêineres.

Captura de tela que mostra a página de visão geral do blob de armazenamento.

Selecione + Contêiner. Um painel no seu lado direito é aberto.

Insira as seguintes configurações e clique em Criar:
Nome: coffee-reviews
Nível de acesso público: contêiner (acesso de leitura anônimo para contêineres e blobs)
Avançado: sem alterações.
Em uma nova guia do navegador, baixe as avaliações de café compactadas de e extraia os arquivos para a pasta de avaliações.https://aka.ms/mslearn-coffee-reviews

No portal do Azure, selecione seu contêiner coffee-reviews. No contêiner, selecione Carregar.

Captura de tela que mostra o contêiner de armazenamento.

No painel Carregar blob, selecione Selecionar um arquivo.

Na janela Explorer, selecione todos os arquivos na pasta de revisões, selecione Abrir e, em seguida, selecione Carregar.

Captura de tela que mostra os arquivos carregados no contêiner do Azure.

Após a conclusão do carregamento, você pode fechar o painel Carregar blob. Seus documentos agora estão em seu contêiner de armazenamento de avaliações de café.
Indexar os documentos
Depois de ter os documentos armazenados, você pode usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um assistente de importação de dados. Com esse assistente, você pode criar automaticamente um índice e um indexador para fontes de dados com suporte. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.

No portal do Azure, navegue até o recurso do Azure AI Search. Na página Visão geral, selecione Importar dados.

Captura de tela que mostra o assistente de importação de dados.

Na página Conectar-se aos seus dados, na lista Fonte de Dados, selecione Armazenamento de Blobs do Azure. Preencha os detalhes do armazenamento de dados com os seguintes valores:
Fonte de dados: Armazenamento de Blobs do Azure
Nome da fonte de dados: coffee-customer-data
Dados a serem extraídos: conteúdo e metadados
Modo de análise: Padrão
Cadeia de conexão: *Selecione Escolher uma conexão existente. Selecione sua conta de armazenamento, selecione o contêiner coffee-reviews e clique em Selecionar.
Autenticação de identidade gerenciada: nenhuma
Nome do contêiner: essa configuração é preenchida automaticamente depois que você escolhe uma conexão existente.
Pasta Blob: deixe em branco.
Descrição: Comentários sobre Fourth Coffee shops.
Selecione Avançar: Adicionar habilidades cognitivas (opcional).

Na seção Anexar Serviços de IA, selecione o recurso de serviços de IA do Azure.

Na seção Adicionar enriquecimentos:
Altere o nome do conjunto de habilidades para coffee-skillset.
Marque a caixa de seleção Ativar OCR e mesclar todo o texto em merged_content campo.
Nota É importante selecionar Habilitar OCR para ver todas as opções de campo enriquecido.

Certifique-se de que o campo Dados de origem esteja definido como merged_content.
Altere o nível de granularidade de enriquecimento para Páginas (partes de 5000 caracteres).
Não selecione Habilitar enriquecimento incremental
Selecione os seguintes campos enriquecidos:

Habilidade cognitiva	Parâmetro	Nome do campo
Extrair nomes de locais	 	Locais
Extrair frases-chave	 	frases-chave
Detectar sentimento	 	sentimento
Gerar tags a partir de imagens	 	tags de imagem
Gerar legendas a partir de imagens	 	legenda da imagem
Em Salvar enriquecimentos em um repositório de conhecimento, selecione:
Projeções de imagem
Documentos
Páginas
Frases-chave
Entidades
Detalhes da imagem
Referências de imagem
Nota Um aviso solicitando uma Cadeia de Conexão da Conta de Armazenamento é exibido.

Captura de tela que mostra o aviso da tela de conexão da conta de armazenamento com 'Escolher uma conexão existente' selecionado.

Selecione Escolher uma conexão existente. Escolha a conta de armazenamento que você criou anteriormente.
Clique em + Contêiner para criar um novo contêiner chamado knowledge-store com o nível de privacidade definido como Privado e selecione Criar.
Selecione o contêiner de armazenamento de conhecimento e clique em Selecionar na parte inferior da tela.
Selecione Projeções de blob do Azure: Documento. Uma configuração para Nome do contêiner com o contêiner de armazenamento de conhecimento preenchido automaticamente é exibida. Não altere o nome do contêiner.

Selecione Avançar: Personalizar índice de destino. Altere o nome do índice para coffee-index.

Certifique-se de que a chave esteja definida como metadata_storage_path. Deixe o nome do Suggester em branco e o modo de pesquisa preenchido automaticamente.

Revise as configurações padrão dos campos de índice. Selecione filtrável para todos os campos que já estão selecionados por padrão. Os nomes de campo que precisam ser marcados como filtráveis incluem: conteúdo, locais, frases-chave, sentimento, merged_content, texto, layoutText, imageTags, imageCaption.

Captura de tela que mostra o painel de índice personalizado com o nome do índice inserido e 'Filtrável' selecionado para um campo de índice padrão.

Selecione Avançar: Criar um indexador.

Altere o nome do indexador para coffee-indexer.

Deixe o Agendamento definido como Uma vez.

Expanda as opções avançadas. Certifique-se de que a opção Chaves de Codificação de Base 64 esteja selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.

Selecione Enviar para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
Mapeia os campos extraídos para o índice.
Retorne à página de recursos do Azure AI Search. No painel esquerdo, em Gerenciamento de Pesquisa, selecione Indexadores. Selecione o indexador de café recém-criado. Aguarde um minuto e selecione &orarr; Atualize até que o Status indique sucesso.

Selecione o nome do indexador para ver mais detalhes.

Captura de tela que mostra o indexador de café Indexador criado com êxito.

Consultar o índice
Use o Gerenciador de pesquisa para escrever e testar consultas. O gerenciador de pesquisa é uma ferramenta integrada ao portal do Azure que oferece uma maneira fácil de validar a qualidade do índice de pesquisa. Você pode usar o Gerenciador de Pesquisa para escrever consultas e revisar resultados em JSON.

Na página Visão geral do serviço de Pesquisa, selecione Gerenciador de pesquisa na parte superior da tela.

Captura de tela de como encontrar o explorador de pesquisa.

Observe como o índice selecionado é o índice de café que você criou. Abaixo do índice selecionado, altere a exibição para a exibição JSON.

Captura de tela do explorador de pesquisa.

No campo Editor de consultas JSON, copie e cole:

código
{
    "search": "*",
    "count": true
}
Selecione Pesquisar. A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo @odata.count. O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.

Agora vamos filtrar por localização. No campo Editor de consultas JSON, copie e cole:
código
{
 "search": "locations:'Chicago'",
 "count": true
}
Selecione Pesquisar. A consulta pesquisa todos os documentos no índice e filtra as revisões com um local de Chicago. Você deve ver no campo.3@odata.count

Agora vamos filtrar por sentimento. No campo Editor de consultas JSON, copie e cole:
código
{
 "search": "sentiment:'negative'",
 "count": true
}
Selecione Pesquisar. A consulta pesquisa todos os documentos no índice e filtra as revisões com um sentimento negativo. Você deve ver no campo.1@odata.count

Nota Veja como os resultados são classificados por . Esta é a pontuação atribuída pelo mecanismo de pesquisa para mostrar o quão próximos os resultados correspondem à consulta fornecida.@search.score

Um dos problemas que podemos querer resolver é por que pode haver certas revisões. Vamos dar uma olhada nas frases-chave associadas à avaliação negativa. Qual você acha que pode ser a causa da revisão?
Examinar o repositório de conhecimento
Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o assistente para Importar dados, você também criou um repositório de conhecimento. Dentro do repositório de conhecimento, você verá que os dados enriquecidos extraídos pelas habilidades de IA persistem na forma de projeções e tabelas.

No portal do Azure, navegue de volta para sua conta de armazenamento do Azure.

No painel de menu à esquerda, selecione Contêineres. Selecione o contêiner de armazenamento de conhecimento.

Captura de tela do contêiner do repositório de conhecimento.

Você verá uma lista de pastas. Há uma pasta para todos os metadados de cada documento de revisão. Selecione qualquer uma das pastas. Na pasta, clique no arquivo objectprojection.json.

Captura de tela do objectprojection.json.

Selecione Editar para ver o JSON produzido para um dos documentos do armazenamento de dados do Azure.

Captura de tela de como encontrar o botão de edição.

Selecione a trilha de navegação do blob de armazenamento na parte superior esquerda da tela para retornar aos Contêineres da conta de armazenamento.

Captura de tela da trilha de navegação do blob de armazenamento.

Em Contêineres, selecione o contêiner coffee-skillset-image-projection. Selecione qualquer um dos itens.

Captura de tela do contêiner do conjunto de habilidades.

Selecione qualquer um dos .jpg arquivos. Selecione Editar para ver a imagem armazenada do documento. Observe como todas as imagens dos documentos são armazenadas dessa maneira.

Captura de tela da imagem salva.

Selecione a trilha de navegação do blob de armazenamento na parte superior esquerda da tela para retornar aos Contêineres da conta de armazenamento.

Selecione Navegador de armazenamento no painel esquerdo e selecione Tabelas. Há uma tabela para cada entidade no índice. Selecione a tabela coffeeSkillsetKeyPhrases.
