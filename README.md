# 🚀 **Qwiklabs - Analise de logs do uso do ambiente com  o BigQuery e Cloud Logging com Looker studio para visualização**

Este laboratório guia você pelo processo de criação de um relatório de log usando o BigQuery, uma ferramenta poderosa de análise de dados do Google Cloud. O objetivo é aprender a integrar dados do Google Cloud Logging com o BigQuery para gerar insights úteis sobre a utilização do uso do ambiente no bigquery.

---


## 🛑 O que você precisa antes de começar
Antes de colocar a mão na massa, certifique-se de ter:

Uma conta no Google Cloud Platform (GCP).
Conhecimentos básicos sobre logs e SQL (não precisa ser expert, prometo!).
Familiaridade com o Console do GCP.

---

## 🎯 **Objetivo Final**

Ao completar este laboratório, você terá criado um relatório de log funcional, capaz de gerar insights a partir de dados de log do Google Cloud.

---

## 🛠️ **Passo a Passo do Laboratório**

### 1️⃣ **Configurações Iniciais**

1. **Login no Console do GCP**
   - Acesse o [Google Cloud Console](https://console.cloud.google.com/).
   - Crie um projeto novo: Na barra superior, clique em **"Novo Projeto"** -> Dê um nome ao seu projeto -> Clique em **"Criar"**.  
     ![Criar Projeto 1](https://github.com/user-attachments/assets/dd6a079d-3c3a-4900-9584-d724276e707d)  
     ![Criar Projeto 2](https://github.com/user-attachments/assets/06877b0f-5842-4451-a724-0a1f59d41d2d)  
     ![Criar Projeto 3](https://github.com/user-attachments/assets/e9feb640-1a00-411f-9bb1-a6b0412960fd)

2. **Verifique o Projeto Selecionado**
   - Após criar o projeto, confirme que ele está selecionado.  
     ![Selecionar Projeto](https://github.com/user-attachments/assets/77e8b839-bdad-4f97-b30d-29586879978a)

3. **Ative o Cloud Shell**
   - Na barra superior, clique no ícone do Cloud Shell (parece um terminal).  
     ![Ativar Cloud Shell 1](https://github.com/user-attachments/assets/1ba10cf3-bca5-48b6-844e-4ed0453b593a)  
   - Com tudo pronto, o terminal será exibido.  
     ![Ativar Cloud Shell 2](https://github.com/user-attachments/assets/39356222-3bc6-4412-b835-d92e6e085525)

4. **Configure o Ambiente**
   - Liste a conta ativa:
     ```bash
     gcloud auth list
     ```
     Autorize quando solicitado.  
     ![Autorizar Conta](https://github.com/user-attachments/assets/6c81b2e1-12f7-490c-bb2b-e90a3e8b4df5)

   - Verifique o ID do projeto:
     ```bash
     gcloud config list project
     ```
     ![Verificar Projeto](https://github.com/user-attachments/assets/ff14c042-dbc6-4030-9e36-38b3ebc55482)

---

### 2️⃣ **Configurando o BigQuery**

1. **Acesse o BigQuery**
   - No menu lateral, clique no ícone de "sanduíche" 🍔 -> Procure por **BigQuery**.  
     ![Menu de Navegação](https://github.com/user-attachments/assets/7c10158c-ac52-4a19-8617-1bf59e39fbba)  
     ![BigQuery](https://github.com/user-attachments/assets/1f95a6ab-fe23-4edd-a4b1-a75b9e6a4849)

2. **Crie um Conjunto de Dados**
   - Clique nos três pontinhos ao lado do projeto -> "Criar novo conjunto de dados".  
     ![Criar Conjunto de Dados](https://github.com/user-attachments/assets/4dd6458d-4d3c-4d6e-88e4-4c7e627475a8)  
   - Nomeie o conjunto como `devfest_logs` e clique em "Criar".  
     ![Nomear Conjunto](https://github.com/user-attachments/assets/43043b43-4e32-47c3-bab5-a1ebdc2cfa15)  

3. **Confirme o Conjunto de Dados Criado**
   - Você verá o conjunto `devfest_logs` listado no seu projeto.  
     ![Conjunto Criado](https://github.com/user-attachments/assets/696a09e8-edb5-4a6d-8228-bf2922dd30e5)

---

### 3️⃣ **Executando Consultas no BigQuery**

1. **Abra o Editor de Consultas**
   - Clique no ícone de `+` para abrir o editor.  
     ![Editor de Consultas](https://github.com/user-attachments/assets/824d0d12-fa17-4103-baf8-5c55bb49fbf3)

2. **Execute uma Query de Teste**
   - Insira a seguinte query e clique em "Executar":
     ```sql
     SELECT CURRENT_DATE AS today;
     ```
     ![Executar Query](https://github.com/user-attachments/assets/eab2df0a-19f4-46ee-9053-59fa0b8b63db)

3. **Confira o Retorno**
   - O resultado exibirá a data atual no retorno da consulta.  
     ![Resultado Query](https://github.com/user-attachments/assets/38b02593-14f0-436a-a28a-36cbf3543513)

---

### 4️⃣ **Configurando o Cloud Logging**

📝 **Dica**: O Cloud Loggins é o serviço do Google Cloud que permite coletar, armazenar e analisar registros (logs) de aplicativos e serviços na nuvem. Ele funciona como um repositório centralizado para capturar logs gerados por recursos do Google Cloud, como VMs, BigQuery, Kubernetes e outros, bem como logs personalizados de seus próprios aplicativos.  

1. **Acesse o Cloud Logging**
   - Na barra de pesquisa, procure por **Logging** e clique em "Gerenciamento e análise de registros", caso receber uma notificação de que o trabalho não foi salvo, clique em "sair".
     
     ![Logging 1](https://github.com/user-attachments/assets/e6fb3df4-7c47-4b74-8d60-e6f78e44225f)
     
     ![Logging 2](https://github.com/user-attachments/assets/fdb5cd72-6ee6-4094-bd03-d52ec78eed7f)
     
     ![notificacao_sair_projeto](https://github.com/user-attachments/assets/1f95b174-f585-4a89-85cb-26dfa093bb4e)
     
     
   - Na parte superior, clique no botão *Todos os Recursos*, filtre por *BigQuery* e clique em aplicar, e depois, *executar consulta*, tudo correndo bem você vai visualizar o retordo na filtragem feita.
     
      ![image](https://github.com/user-attachments/assets/391cc5de-1635-4f4b-afb1-2f8802b7560a)
     
      ![image](https://github.com/user-attachments/assets/70c1538f-c270-402f-969b-ea8b19cafa52)
     
      ![image](https://github.com/user-attachments/assets/099e0e55-3818-4412-9b57-24e37386f936)

   - Agora com a execução feita, busque pelo retorno que contém *Jobcompleted*, clique na seta a esquerda, o retorno é um json com diversas informações sobre a execução. Clique no botão *Entradas semelhantes* e selecione *Mostrar entradas semelhantes*
    
     📝 **Dica**: o termo **jobcompleted** está associado a eventos registrados quando um job no Google Cloud é concluído. No contexto do BigQuery, por exemplo, um evento jobcompleted indica que uma tarefa ou job submetido ao BigQuery (como uma consulta SQL, carga de dados ou exportação) foi finalizado com sucesso ou falha.
     
     📝 **Dica**: Informações disponíveis no log

                   - ID do job: Identifica exclusivamente o job executado.
                   - Tipo do job: Pode ser uma consulta (QUERY), carga de dados (LOAD), exportação (EXPORT), entre outros.
                   - Timestamp: Marca o momento em que o job foi concluído.
                   - Estatísticas: Dados sobre o tempo de execução, volume de dados processados e custos associados.
                   - Status final: Sucesso ou falha.

     ![image](https://github.com/user-attachments/assets/94e49c34-da62-4497-aff0-49d50663849b)
     ![image](https://github.com/user-attachments/assets/b834e541-74b3-464d-a6e1-5cf09bd4bcfd)
     ![image](https://github.com/user-attachments/assets/cff51038-4fdb-4f1e-8766-7254d4ef83ee)

2. **Crie um Coletor de Logs (Sink)**
   📝 **Dica**: O Sink é o recurso de configuração do Cloud Logging usado para exportar logs de um repositório central para outro destino. Ele permite enviar logs gerados pelos serviços do GCP para outras ferramentas para armazenamento, análise ou monitoramento.
   
   - Clique em "Mais ações" -> "Criar coletor".  
     ![Criar Coletor](https://github.com/user-attachments/assets/8c386749-f2d9-43d9-aaab-e8c7edce6d83)  
   - Nomeie o coletor, escolha **BigQuery** como destino e selecione o conjunto `devfest_logs`. Clique em **Criar coletor**, com isso, todas as proximas entrada de registros do bigquery serão exportadas para uma tabela no conjunto de dados criado, no nosso caso o devfest_logs. 

     ![Configurar Coletor](https://github.com/user-attachments/assets/dabd349f-5f53-4cf5-b83f-afd962bc25ef)

---

### 5️⃣ **Gerando Logs (Mão na Massa)**

1. No **Cloud Shell**, execute queries para gerar dados. Exemplos:
   - **Média de Pontuação das Perguntas:**
     ```bash
     bq query --nouse_legacy_sql \
     "SELECT AVG(score) AS average_score 
      FROM \`bigquery-public-data.stackoverflow.posts_questions\`"
     ```
   - **Total de Commits por Ano:**
     ```bash
     bq query --nouse_legacy_sql \
     "SELECT EXTRACT(YEAR FROM committer.date) AS year, COUNT(*) AS total_commits 
      FROM \`bigquery-public-data.github_repos.sample_commits\` 
      GROUP BY year 
      ORDER BY year DESC"
     ```
     - **Posts criados por ano:**
     ```bash
      bq query --nouse_legacy_sql \
      "SELECT EXTRACT(YEAR FROM creation_date) as year, COUNT(*) as total_posts 
       FROM \`bigquery-public-data.stackoverflow.posts_questions\` 
       GROUP BY year 
       ORDER BY year DESC"
     ```
      - **Usuários com maior reputação:**
     ```bash
      bq query --nouse_legacy_sql \
      "SELECT display_name, reputation 
       FROM \`bigquery-public-data.stackoverflow.users\` 
       ORDER BY reputation DESC 
       LIMIT 10"
     ```
      - **Total de perguntas sem respostas:**
     ```bash
      bq query --nouse_legacy_sql \
      "SELECT COUNT(*) as unanswered_questions 
       FROM \`bigquery-public-data.stackoverflow.posts_questions\` 
       WHERE answer_count = 0"
     ```
      - **Top 5 usuários mais ativos:**
     ```bash
      bq query --nouse_legacy_sql \
      "SELECT owner_user_id, COUNT(*) as post_count 
       FROM \`bigquery-public-data.stackoverflow.posts_questions\` 
       WHERE owner_user_id IS NOT NULL 
       GROUP BY owner_user_id 
       ORDER BY post_count DESC 
       LIMIT 5"
     ```
      - **Repositórios mais populares:**
     ```bash
      bq query --nouse_legacy_sql \
      "SELECT repo_name, COUNT(*) as commits 
       FROM \`bigquery-public-data.github_repos.sample_commits\` 
       GROUP BY repo_name 
       ORDER BY commits DESC 
       LIMIT 10"
     ```

   📝 **Dica**: Explore outras queries para criar um ambiente rico de logs, a imagem abaixo mostra o retorno da execução de uma query.  

   ![Exemplo Retorno](https://github.com/user-attachments/assets/67e021fe-eed1-4b06-aba4-4685b5a5ac8d)

---

### **6️⃣ Exibindo os registros no BigQuery**

1. **Acesse o BigQuery e visualize a tabela de logs**:
   - Volte ao BigQuery no Console do GCP.
   - Expanda o projeto no menu lateral esquerdo.
   - Localize o conjunto de dados que você criou (`devfest_logs`) e expanda-o.  
     Se tudo estiver configurado corretamente, você verá uma tabela com o nome `cloudaudit_googleapis_`.  

     ![Visualizar Projeto e Tabela](https://github.com/user-attachments/assets/bfe49e3b-0120-4716-a022-27ccb1f87ac1)

2. **Entenda a Tabela de Logs (`cloudaudit_googleapis_`)**:
   - Essa tabela é um registro de eventos relacionados ao acesso a dados, como:
     - Leituras
     - Escritas
     - Exclusões
     - Consultas em serviços como BigQuery, Cloud Storage e Firestore.  
   - 📝 **Dicas importantes**:
     - Caso a tabela não apareça, feche o Cloud Shell, reabra-o e reexecute as queries.
     - Logs de acesso a dados podem estar desativados. Ative-os nas configurações do Cloud Logging ou no IAM Policy.  
     - **Cuidado com custos!** O volume de logs pode ser significativo dependendo das operações.  
       **Como otimizar:**
       - Configure filtros para exportar apenas os logs relevantes.
       - Defina políticas de retenção para logs antigos.

3. **Visualize os campos da tabela**:
   - Clique no nome da tabela `cloudaudit_googleapis_` para exibir seus campos.  
     Você verá uma lista detalhada de informações como tipo de job, tempo de execução, bytes processados, entre outros.  
     ![Visualizar Campos da Tabela](https://github.com/user-attachments/assets/9a2ea7aa-9555-4187-b2f5-ef604b645c58)

---

### **7️⃣ Criando uma visualização para simplificar a tabela**

1. **Prepare o ambiente para criar uma visualização personalizada**:
   - Para criar a visualização no BigQuery, você precisará do **ID do projeto**.  
   - No menu lateral, clique nos três pontinhos ao lado do nome do projeto e selecione **Copiar ID do projeto**.  
     ![Copiar ID do Projeto](https://github.com/user-attachments/assets/2d589854-6181-44c7-b6d6-c79a374df3d3)

2. **Crie uma visualização com a query abaixo**:
   - Acesse o editor de consultas no BigQuery e cole o seguinte código:  
     ```sql
     CREATE OR REPLACE VIEW
       devfest_logs.v_querylogs AS
     SELECT
       resource.labels.project_id,
       protopayload_auditlog.authenticationInfo.principalEmail,
       protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobConfiguration.query.query,
       protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobConfiguration.query.statementType,
       protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatus.error.message,
       protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.startTime,
       protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.endTime,
       TIMESTAMP_DIFF(protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.endTime, 
                      protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.startTime, 
                      MILLISECOND)/1000 AS run_seconds,
       protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.totalProcessedBytes,
       protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.totalSlotMs,
       ARRAY(SELECT AS STRUCT datasetId, tableId 
             FROM UNNEST(protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.referencedTables)) AS tables_ref,
       protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.totalTablesProcessed,
       protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.queryOutputRowCount,
       severity
     FROM
       `<ID_DO_SEU_PROJETO>.cloudaudit_googleapis_*`
     ORDER BY
       startTime;
     ```

3. **Execute a query**:
   - Clique em **Executar** no editor de consultas.
   - Se tudo estiver correto, o retorno será semelhante ao da imagem abaixo:  
     ![Resultado da Visualização](https://github.com/user-attachments/assets/ac75ffa9-d649-44d4-93b1-ff6dc9e2ec0f)

---

### **8️⃣ Explorando a visualização criada**

1. **Execute uma consulta para explorar a visualização**:
   - Use a query abaixo para visualizar os dados processados:
     ```sql
     SELECT * FROM devfest_logs.v_querylogs;
     ```

     ![image](https://github.com/user-attachments/assets/aba042e0-4c68-4b50-9929-7f82fb83885f)

2. **Descrição dos Campos Importantes**:
   - **`resource.labels.project_id`**: ID do projeto associado à execução.
   - **`principalEmail`**: E-mail do usuário/serviço que executou a query.
   - **`query`**: Texto completo da query executada.
   - **`statementType`**: Tipo de comando SQL (SELECT, INSERT, etc.).
   - **`startTime` / `endTime`**: Timestamp de início e término da execução.
   - **`run_seconds`**: Tempo total de execução em segundos.
   - **`totalProcessedBytes`**: Bytes processados pela consulta (impacta custos).
   - **`tables_ref`**: Lista de tabelas referenciadas na consulta.
   - **`severity`**: Nível de severidade do evento (INFO, WARNING, ERROR).  

---


---

### 9️⃣ **Explorando com o Looker Studio**

1. No BigQuery, clique em "Explorar Dados" > "Explorar com Looker Studio".  

 ![image](https://github.com/user-attachments/assets/e7d56dd0-6878-48af-955a-7c4b6dfd6527)
---

---

### 1️⃣0️⃣ **Looker Studio**

1.  A proxima tela que você vai vai é a do *looker studio*, que já vem com algumas coisinhas na tela.  

 ![image](https://github.com/user-attachments/assets/f8b3455a-5c3f-40f7-ac77-aac99df9e143)
 
---

---

### 1️⃣1️⃣ **Looker Studio - gráficos**

1.  Usuários com Mais Consultas.  
- **Objetivo**: Identificar os usuários que executaram mais consultas.
- **Como Fazer**:
  - No Looker Studio, selecione "Gráfico de Barras".
    ![image](https://github.com/user-attachments/assets/fe2779bd-3995-408d-97b8-206fc41cda1a)
    
  - Arraste `principalEmail` para Dimensão e crie uma métrica calculada de contagem (COUNT) para o número de consultas.
    ![image](https://github.com/user-attachments/assets/dcdf4123-93b9-4b31-8ee7-daa1fe4f32c2)

 2. Quantidade de querys processadas por tipo de Query.
- **Objetivo**: Mostrar o volume de dados processados agrupados por tipo de comando SQL.
- **Como Fazer**:
  - Escolha "Tabela Dinâmica".
  - Arraste `statementType` para Linhas, `severity` para Colunas e `Contagem(statementType)` como Métrica.

  ![image](https://github.com/user-attachments/assets/64f2fb22-0ba7-4de8-a788-341bd54583ed)


 3. Queries que Consomem Mais Recursos de Processamento.
- **Objetivo**: Identificar as queries que consomem mais recursos em termos de bytes processados, ajudando a localizar possíveis gargalos ou operações custosas.
- **Como Fazer**:
  - Escolha "Gráfico de Barras".
  - Arraste `query` para Dimensão, `totalProcessedBytes ` para Métrica e configure a Ordenação para exibir os valores em ordem decrescente.

 ![image](https://github.com/user-attachments/assets/e36c3d51-217b-45a1-82ee-07ea0aac14d1)

4. Tabelas mais usadas.
- **Objetivo**: Identificar as tabelas mais usadas nas consultas.
- **Como Fazer**:
  - Escolha "Mapa de Árvore".
  - Arraste `tables_ref.tableID` e `tables_ref.datasetid` para Dimensão, em Métrica  `record count` como soma em *execução*.
 
![image](https://github.com/user-attachments/assets/261500c8-bb93-4abf-8981-7314dbf494bd)
    
---

## 📊 **Relatório Final**

Após configurar os gráficos acima, você terá um relatório como o exemplo abaixo.  

![Exemplo de Relatório Final](https://github.com/user-attachments/assets/fc01518f-fb2a-4442-9158-4c6203c86b8e)

---

## 🔍 **Possíveis Insights e Análises**

1. **Identificação de Usuários Mais Ativos**:
   - Descubra quais usuários estão consumindo mais recursos no BigQuery.
   - Monitore padrões de uso, como horários de pico e comportamento anômalo.

2. **Análise de Tipo de Queries**:
   - Avalie quais comandos SQL são mais utilizados (e.g., SELECT, INSERT, CREATE).
   - Relacione tipos de queries com severidades para encontrar potenciais gargalos ou erros.

3. **Identificação de Queries Custosas**:
   - Localize consultas que consomem muitos bytes processados.
   - Priorize a otimização de queries que impactam custos operacionais.

4. **Tabelas Mais Referenciadas**:
   - Identifique tabelas com alta carga de leitura ou escrita.
   - Ajude a planejar estratégias de particionamento ou indexação.

5. **Distribuição por Severidade**:
   - Monitore logs de severidade para detectar falhas ou alertas frequentes.

6. **Tendências de Consumo**:
   - Analise o crescimento do volume de logs ao longo do tempo.
   - Planeje capacidade com base no uso histórico.

---

  



## 📖 **Documentação e Recursos**

- [BigQuery Documentation](https://cloud.google.com/bigquery/docs)
- [Google Cloud Logging](https://cloud.google.com/logging/docs)
- [Looker Studio](https://datastudio.google.com)
- [CLI gcloud](https://cloud.google.com/sdk/gcloud)

---

