# dashboard-mysql-azure
Projeto DIO Criando um Dashboard corporativo com integração com MySQL e Azure

# Criando um Dashboard Corporativo no Power BI com Integração MySQL e Azure

Este guia demonstra como criar um dashboard corporativo no Power BI utilizando dados de um banco de dados MySQL hospedado no Azure.  O dashboard exibirá informações cruciais para a tomada de decisões, com a flexibilidade de utilizar os recursos da nuvem Azure.

## Pré-requisitos

*   **Power BI Desktop:** Instale o Power BI Desktop (gratuito) no seu computador. [https://powerbi.microsoft.com/desktop/](https://powerbi.microsoft.com/desktop/)
*   **Conta Power BI Service:** Para publicar e compartilhar o dashboard, você precisará de uma conta no Power BI Service (uma conta gratuita pode ser suficiente).
*   **Banco de Dados MySQL no Azure:** Um banco de dados MySQL provisionado e hospedado no Azure. Você precisará das credenciais de acesso (servidor, banco de dados, usuário e senha).
*   **Azure Account (Opcional - Depende da fonte de dados no Azure):** Caso utilize outros serviços Azure como Data Lake Storage ou Azure SQL Database, será necessário uma conta com as permissões necessárias.
*   **Power BI Gateway (Opcional - Depende da configuração do MySQL):** Se o banco de dados MySQL no Azure estiver acessível apenas através de uma rede privada virtual (VPN) ou por trás de um firewall, você precisará configurar um Power BI Gateway para permitir que o Power BI Service acesse os dados.

## Passo a Passo

### 1. Conectar o Power BI Desktop ao Banco de Dados MySQL no Azure

1.  **Abrir o Power BI Desktop:** Inicie o Power BI Desktop.

2.  **Obter Dados:** Na guia "Página Inicial", clique em "Obter dados".

3.  **Selecionar MySQL Database:** Na lista de fontes de dados, procure e selecione "MySQL Database".

4.  **Configurar a Conexão:**
    *   **Servidor:** Digite o nome do servidor MySQL no Azure (ex: `your-server.mysql.database.azure.com`).
    *   **Banco de Dados (Opcional):** Se você souber o nome do banco de dados específico, digite-o. Caso contrário, você pode navegar pelos bancos de dados disponíveis após a conexão inicial.
    *   **Conectividade:** Selecione "Import" (importa os dados para o Power BI) ou "DirectQuery" (consulta o banco de dados diretamente a cada atualização).  **DirectQuery é recomendado para dados que mudam com frequência**, mas pode afetar o desempenho do dashboard.
    *   Clique em "OK".

5.  **Inserir Credenciais:** Digite o nome de usuário e a senha para acessar o banco de dados MySQL no Azure.  Selecione o nível ao qual as credenciais devem ser aplicadas.  Clique em "Conectar".

6.  **Selecionar Tabelas:** Navegue pelos bancos de dados e tabelas disponíveis. Selecione as tabelas que você deseja incluir no seu dashboard.

7.  **Carregar ou Transformar Dados:** Clique em "Carregar" para importar os dados diretamente ou "Transformar dados" para abrir o Power Query Editor e realizar transformações.  **Transformar os dados é fundamental para garantir a qualidade e organização dos dados.**

### 2. Transformar os Dados no Power Query Editor (Opcional, mas Recomendado)

O Power Query Editor permite limpar, transformar e modelar os dados antes de carregá-los no Power BI.

1.  **Remover Colunas Desnecessárias:** Selecione as colunas que não serão usadas no dashboard e clique em "Remover Colunas".

2.  **Alterar Tipos de Dados:** Verifique se os tipos de dados das colunas estão corretos (Data, Número, Texto, etc.). Use o dropdown "Tipo de dados" na guia "Transformar" para alterar o tipo, se necessário.

3.  **Renomear Colunas:** Clique duas vezes no cabeçalho de uma coluna para renomeá-la com um nome mais descritivo.

4.  **Filtrar Linhas:** Use a opção de filtro nas colunas para remover linhas indesejadas ou com dados inválidos.

5.  **Adicionar Colunas Calculadas:**
    *   Na guia "Adicionar Coluna", clique em "Coluna Personalizada".
    *   Digite um nome para a nova coluna.
    *   Use a linguagem Power Query M para criar a fórmula da coluna calculada.

6.  **Combinar Dados de Múltiplas Tabelas (Se Necessário):** Use "Mesclar Consultas" (joins) para combinar dados de diferentes tabelas com base em chaves comuns.

7.  **Fechar e Aplicar:** Após realizar as transformações desejadas, clique em "Fechar e Aplicar" na guia "Página Inicial".

### 3. Criar o Modelo de Dados (Relationships)

O Power BI usa o modelo de dados para relacionar as tabelas e permitir a criação de visualizações interativas.

1.  **Ir para a Exibição de Modelo:** Clique no ícone "Modelo" (parece um diagrama de banco de dados) na barra lateral esquerda.

2.  **Criar Relacionamentos:**
    *   Arraste um campo de uma tabela para o campo correspondente em outra tabela para criar um relacionamento.
    *   Certifique-se de que o tipo de relacionamento (um-para-muitos, um-para-um, muitos-para-muitos) esteja correto. O Power BI geralmente detecta automaticamente, mas verifique.

### 4. Criar Medidas e Cálculos (DAX)

As medidas são cálculos personalizados que você pode usar para agregar e analisar os dados. Elas são criadas usando a linguagem DAX (Data Analysis Expressions).

1.  **Ir para a Exibição de Relatório:** Clique no ícone "Relatório" na barra lateral esquerda.

2.  **Criar uma Nova Medida:**
    *   Clique com o botão direito em uma tabela no painel "Campos" e selecione "Nova Medida".
    *   Digite a fórmula DAX na barra de fórmulas.

    **Exemplos de Medidas:**

    *   **Total de Vendas:** `Total Vendas = SUM(Sales[SalesAmount])`
    *   **Média de Vendas:** `Média Vendas = AVERAGE(Sales[SalesAmount])`
    *   **Total de Clientes:** `Total Clientes = DISTINCTCOUNT(Customers[CustomerID])`
    *   **Vendas por Categoria de Produto:** `CALCULATE([Total Vendas], FILTER(Products, Products[Category] = SELECTEDVALUE(Categories[CategoryName])))`

### 5. Criar Visualizações para o Dashboard

1.  **Selecionar um Visual:** No painel "Visualizações", clique no ícone do visual desejado (gráfico de colunas, gráfico de linhas, gráfico de pizza, cartão, mapa, etc.).

2.  **Adicionar Campos:** Arraste os campos e medidas do painel "Campos" para as áreas apropriadas do visual (Eixo, Legenda, Valor, etc.).

    **Exemplos de Visualizações para um Dashboard Corporativo:**

    *   **Gráfico de Linhas:** Vendas ao longo do tempo (Eixo: Data, Valor: Total Vendas)
    *   **Gráfico de Colunas:** Vendas por região (Eixo: Região, Valor: Total Vendas)
    *   **Gráfico de Pizza:** Distribuição de vendas por categoria de produto (Legenda: Categoria de Produto, Valor: Total Vendas)
    *   **Cartões:** Métricas chave como Total de Vendas, Número de Clientes, Crescimento das Vendas
    *   **Mapa:** Vendas por país/estado (Localização: País/Estado, Valor: Total Vendas)
    *   **Tabela:** Detalhes de vendas por cliente ou produto

### 6. Configurar Interatividade (Filtros e Segmentações de Dados)

Adicionar filtros e segmentações de dados permite que os usuários explorem os dados e personalizem as visualizações.

1.  **Adicionar Segmentação de Dados (Slicer):**
    *   Selecione o visual "Segmentação de Dados" no painel "Visualizações".
    *   Arraste o campo que você deseja usar como filtro para o visual (ex: Data, Região, Categoria de Produto).

2.  **Configurar Filtros Visuais:**
    *   Selecione um visual.
    *   No painel "Filtros", você pode adicionar filtros específicos para aquele visual.

### 7. Design do Dashboard

1.  **Organizar as Visualizações:** Posicione as visualizações de forma lógica e visualmente agradável na tela. Priorize as informações mais importantes.

2.  **Usar Cores e Fontes Consistentes:** Escolha um esquema de cores e fontes que sejam consistentes com a identidade visual da sua empresa.

3.  **Adicionar Títulos e Descrições:** Crie títulos claros e concisos para cada visualização e para o dashboard como um todo. Adicione descrições para explicar o que cada visualização mostra.

4.  **Usar Imagens e Logotipos:** Inclua o logotipo da sua empresa e outras imagens relevantes para tornar o dashboard mais atraente.

### 8. Publicar o Dashboard no Power BI Service

1.  **Salvar o Arquivo .pbix:** Salve o arquivo do Power BI Desktop (.pbix) no seu computador.

2.  **Publicar:**
    *   Na guia "Página Inicial", clique em "Publicar".
    *   Faça login na sua conta do Power BI Service.
    *   Selecione o workspace onde você deseja publicar o dashboard.

### 9. Configurar Agendamento de Atualização de Dados no Power BI Service

Para manter o dashboard atualizado com os dados mais recentes do seu banco de dados MySQL no Azure, você precisa configurar um agendamento de atualização.

1.  **Gateway de Dados:**
    *   **Se o seu banco de dados MySQL no Azure estiver acessível diretamente através da internet**, você pode pular esta etapa.
    *   **Se o seu banco de dados estiver em uma rede privada ou por trás de um firewall**, você precisará instalar e configurar um Power BI Gateway no seu computador ou em um servidor. Consulte a documentação da Microsoft para obter instruções detalhadas: [https://docs.microsoft.com/power-bi/connect-data/service-gateway-onprem](https://docs.microsoft.com/power-bi/connect-data/service-gateway-onprem)

2.  **Configurar as Credenciais da Fonte de Dados:**
    *   No Power BI Service, vá para o seu workspace e selecione o dataset correspondente ao seu dashboard.
    *   Clique em "Configurações".
    *   Expanda a seção "Credenciais da fonte de dados".
    *   Clique em "Editar credenciais" e insira as credenciais de acesso ao seu banco de dados MySQL no Azure.
    *   Se você estiver usando um gateway, selecione o gateway que você configurou.

3.  **Agendar a Atualização:**
    *   Na seção "Agendamento de atualização", ative a opção "Agendamento de atualização".
    *   Defina a frequência desejada para as atualizações (diariamente, semanalmente, etc.) e os horários em que as atualizações devem ocorrer.

### 10. Compartilhar o Dashboard

1.  **Compartilhar com Usuários Individuais:**
    *   No Power BI Service, abra o dashboard.
    *   Clique em "Compartilhar" (canto superior direito).
    *   Digite os endereços de e-mail dos usuários com quem você deseja compartilhar o dashboard.
    *   Defina as permissões (Visualizar, Editar, etc.).

2.  **Compartilhar com Grupos (Power BI Pro ou Premium):**
    *   Crie um grupo no Power BI Service.
    *   Adicione os usuários ao grupo.
    *   Compartilhe o dashboard com o grupo.

3.  **Incorporar o Dashboard em um Site ou Aplicação (Power BI Embedded):**
    *   Utilize o Power BI Embedded para incorporar o dashboard em seu site ou aplicação. Isso requer uma licença Power BI Embedded.

## Dicas e Melhores Práticas

*   **Planeje o seu dashboard:** Antes de começar a criar o dashboard, defina claramente os seus objetivos, o público-alvo e as principais métricas que você deseja exibir.
*   **Mantenha o dashboard simples e focado:** Evite sobrecarregar o dashboard com muitas visualizações ou informações desnecessárias.
*   **Otimize o desempenho do dashboard:** Minimize o uso de cálculos complexos e dados desnecessários. Use DirectQuery com moderação.
*   **Monitore o desempenho do agendamento de atualização:** Verifique regularmente se as atualizações estão ocorrendo com sucesso e resolva quaisquer problemas que surgirem.
*   **Treine seus usuários:** Forneça treinamento aos usuários sobre como usar o dashboard e interpretar os dados.
*   **Obtenha feedback:** Solicite feedback dos usuários para identificar áreas de melhoria no dashboard.
*   **Governança de Dados:** Estabeleça políticas de governança de dados para garantir a qualidade, consistência e segurança dos dados utilizados no dashboard.
*   **Documentação:** Mantenha uma documentação detalhada do dashboard, incluindo as fontes de dados, as transformações, as medidas e os relacionamentos.

## Considerações de Segurança

*   **Credenciais:** Proteja as credenciais de acesso ao seu banco de dados MySQL no Azure. Não as armazene em arquivos de texto não criptografados. Use as funcionalidades de gerenciamento de segredos do Azure ou Power BI para armazenar as credenciais de forma segura.
*   **Acesso à Rede:** Limite o acesso ao seu banco de dados MySQL no Azure apenas aos endereços IP necessários.
*   **Criptografia:** Utilize criptografia para proteger os dados em trânsito entre o Power BI e o seu banco de dados MySQL no Azure.

Seguindo este guia, você poderá criar um dashboard corporativo poderoso e informativo no Power BI, integrando dados do seu banco de dados MySQL no Azure e aproveitando os recursos da plataforma Power BI para análise e visualização de dados.
