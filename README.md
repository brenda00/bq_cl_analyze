# 🚀 **Qwiklabs - Analise de logs do uso do ambiente com  o BigQuery e Cloud Logging com Looker para visualização**

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

## 🛠️ **Passos do Laboratório**

1. **Login no Console do GCP**
   - Acesse o [Google Cloud Console](https://console.cloud.google.com/).
   - Crie um projeto novo: Vá para a barra superior -> clique em "Novo Projeto" -> nomeie seu projeto -> clique em "Criar".

   📝 **Dica**: Se você já tem um projeto, verifique se ele está selecionado corretamente na barra superior.  
   ![Passo 1](https://github.com/user-attachments/assets/dd6a079d-3c3a-4900-9584-d724276e707d)

1. **Configurações iniciais**

   - Faça login no Console do [Google Cloud](https://console.cloud.google.com/).

   - Criar um novo projeto, na parte superior da barra de pesquisa conforme imagem abaixo, clique nele -> novo projeto -> coloque o nome do seu projeto -> clique no botão criar. 
   
PS: esses passos são necessarios apenas se você não tem um projeto criado.

PS1: caso você tenha mais de um projeto e queira criar um do zero, após a criação confira que realmente o novo projeto foi selecionado, conforme imagem.

![icone_criar_novo_projeto](https://github.com/user-attachments/assets/dd6a079d-3c3a-4900-9584-d724276e707d)

![criar_novo_projeto](https://github.com/user-attachments/assets/06877b0f-5842-4451-a724-0a1f59d41d2d)

![nomear_criar_novo_projeto](https://github.com/user-attachments/assets/e9feb640-1a00-411f-9bb1-a6b0412960fd)

Após criar o projeto verifique que você está nele, conforme imagem abaixo

![novo_projeto](https://github.com/user-attachments/assets/77e8b839-bdad-4f97-b30d-29586879978a)

- Ativar o Cloud Shell, na parte superior próximo a barra de pesquisar, conforme imagem, clique no icone do Cloud Shell. Com tudo correndo bem, você deve visualizar a tela do Cloud Shell conforme segunda imagem.
 
   ![icone_cloud_shell](https://github.com/user-attachments/assets/1ba10cf3-bca5-48b6-844e-4ed0453b593a)

  ![cloud_shell_ativo](https://github.com/user-attachments/assets/39356222-3bc6-4412-b835-d92e6e085525)

- Verifique o nome da conta ativa em utilização com o comando ´gcloud auth list´, ao escrever o primeiro comando no cloud shell ele pede autorização, apenas autorize, conforme imagem abaixo.
  
PS: gcloud é a ferramenta de linha de comando do Google Cloud. Não precisa se preocupar em instalar pois já vem pré-instalada.

```
gcloud auth list
```

![autorizacao_cloud_shell](https://github.com/user-attachments/assets/6c81b2e1-12f7-490c-bb2b-e90a3e8b4df5)

Com tudo correndo bem esse é o retorno da conta ativa.

![retorno_conta_ativa](https://github.com/user-attachments/assets/b2708794-60ab-4093-bcca-40e84c3cbeda)

- Verifique qual o ID do projeto para ter certeza que estamos no local correto com o comando ´gcloud config list project´

```
gcloud config list project
```

  ![retorno_do_id_projeto](https://github.com/user-attachments/assets/ff14c042-dbc6-4030-9e36-38b3ebc55482)

---

 2. **BigQuery**

    - No Console do Google Cloud, selecione o menu de navegação -> BigQuery, para isso, clique no icone de "sanduiche", conforme imagem, identifique o Bigquery e selecione, com isso você vai estar no Bigquery.
   
      ![icone_menu_navegacao](https://github.com/user-attachments/assets/7c10158c-ac52-4a19-8617-1bf59e39fbba)

      ![selecao_bigquery](https://github.com/user-attachments/assets/1f95a6ab-fe23-4edd-a4b1-a75b9e6a4849)

      ![visao_inicial_bigquery](https://github.com/user-attachments/assets/d873bd56-e9b5-40a2-bb72-0063f84107f1)

 ---     

3. **Criar um conjunto de dados**
   
   - Conforme imagem abaixo, clique nos três pontinhos e selecione ´Criar novo conjunto de dados´

   ![passos_para_criar_novo_conjunto_dados](https://github.com/user-attachments/assets/4dd6458d-4d3c-4d6e-88e4-4c7e627475a8)

   - De um nome para o seu conjunto de dados e clique em ´Criar conjunto de dados´
     
     ![criacao_de_um_novo_conjunto_dados](https://github.com/user-attachments/assets/43043b43-4e32-47c3-bab5-a1ebdc2cfa15)

  - Agora no nosso projeto ´devfestbqcl´ e possivel observar o conjunto de dados que criamos ´devfest_logs´

    ![conjunto_de_dados_criado](https://github.com/user-attachments/assets/696a09e8-edb5-4a6d-8228-bf2922dd30e5)

 ---   
    

4. **Executar uma consulta**

   - Abra o editor de consultas do bigquery, clique no icone de ´+´
     ![icone_editor_consultas](https://github.com/user-attachments/assets/824d0d12-fa17-4103-baf8-5c55bb49fbf3)

  - Execute clicando no botão ´Executar´

   ```
SELECT current_date
```
![execucao_da_query](https://github.com/user-attachments/assets/eab2df0a-19f4-46ee-9053-59fa0b8b63db)

- Você vai receber um retorno parecido com esse, pois a data vai variar com o dia da execução.
  
  ![retorno_query](https://github.com/user-attachments/assets/38b02593-14f0-436a-a28a-36cbf3543513)


---

5. **configurar a exportação de registros do Cloud Logging **
   
    O Cloud Loggins é o serviço do Google Cloud que permite coletar, armazenar e analisar registros (logs) de aplicativos e serviços na nuvem. Ele funciona como um repositório centralizado para capturar logs gerados por recursos do Google Cloud, como VMs, BigQuery, Kubernetes e outros, bem como logs personalizados de seus próprios aplicativos.

- Conforme a imagem, na barra de pesquisar procure por **logging** clique na opção **Gerenciamento e análise de registros** conforme imagem

![image](https://github.com/user-attachments/assets/e6fb3df4-7c47-4b74-8d60-e6f78e44225f)

![image](https://github.com/user-attachments/assets/fdb5cd72-6ee6-4094-bd03-d52ec78eed7f)


- Caso você receba a mensagem a seguir, clique em **SAIR**
  ![image](https://github.com/user-attachments/assets/1f95b174-f585-4a89-85cb-26dfa093bb4e)

-  Na parte superior encontre o botão 'todos os recursos', filtre por **Bigquery** e clique em aplicar
  ![image](https://github.com/user-attachments/assets/391cc5de-1635-4f4b-afb1-2f8802b7560a)

- Agora clique em 'executar consulta', no canto superior direito
  
![image](https://github.com/user-attachments/assets/70c1538f-c270-402f-969b-ea8b19cafa52)

- Com tudo correndo bem, você deve ter um retorno parecido com o da imagem abaixo
  ![image](https://github.com/user-attachments/assets/099e0e55-3818-4412-9b57-24e37386f936)

- Nesse retorno de consulta procure o que contém a palavra "jobcompleted", clique na setá a esquerda para verificar as informações, o retorno é um json contendo diversas informações sobre a execução.

PS: o termo jobcompleted está associado a eventos registrados quando um job no Google Cloud é concluído. No contexto do BigQuery, por exemplo, um evento jobcompleted indica que uma tarefa ou job submetido ao BigQuery (como uma consulta SQL, carga de dados ou exportação) foi finalizado com sucesso ou falha.

Informações disponíveis no log:

ID do job: Identifica exclusivamente o job executado.
Tipo do job: Pode ser uma consulta (QUERY), carga de dados (LOAD), exportação (EXPORT), entre outros.
Timestamp: Marca o momento em que o job foi concluído.
Estatísticas: Dados sobre o tempo de execução, volume de dados processados e custos associados.
Status final: Sucesso ou falha.

![image](https://github.com/user-attachments/assets/94e49c34-da62-4497-aff0-49d50663849b)

- Identifique o botão de 'Entradas semelhantes' e selecione **Mostrar entradas semelhantes**, você deve ter um retorno parecido com a imagem dois

  ![image](https://github.com/user-attachments/assets/b834e541-74b3-464d-a6e1-5cf09bd4bcfd)

![image](https://github.com/user-attachments/assets/cff51038-4fdb-4f1e-8766-7254d4ef83ee)

---

6. ** Criando um coletor/sink**
   PS:  recurso de configuração do Cloud Logging usado para exportar logs de um repositório central para outro destino. Ele permite enviar logs gerados pelos serviços do GCP para outras ferramentas para armazenamento, análise ou monitoramento.

   - Ainda no logging, localize o menu suspenso o botão de "mais ações", clique em *criar coletor*
   ![image](https://github.com/user-attachments/assets/8c386749-f2d9-43d9-aaab-e8c7edce6d83)

- De um nome para o seu coletor e clique em proximo
  ![image](https://github.com/user-attachments/assets/4f15cd26-ef0b-4354-816d-7aae0aefcbae)

- selecione o destino do coletor, aqui estamos falando que vamos mandar para o bigquery e o conjunto de dados é o inicial que criamos o 'devfest_logs', clique em 'criar coletor', com isso, todas as proximas entrada de registros do bigquery serão exportadas para uma tabela no conjunto de dados criado, no nosso caso o *devfest_logs*
  ![image](https://github.com/user-attachments/assets/dabd349f-5f53-4cf5-b83f-afd962bc25ef)


---

7. ** Mão na massa, execute **
    Vamos executar algumas querys aleatorias para gerar logs no nosso ambiente, fique avontade para explorar as possibilidades, aqui vamos usar as bases de dados publicas disponiveis, vamos executar pelo cloud shell.

- Média de pontuação das perguntas:   
```
bq query --nouse_legacy_sql \
"SELECT AVG(score) as average_score 
 FROM \`bigquery-public-data.stackoverflow.posts_questions\`"
```

- Posts criados por ano:   
```
bq query --nouse_legacy_sql \
"SELECT EXTRACT(YEAR FROM creation_date) as year, COUNT(*) as total_posts 
 FROM \`bigquery-public-data.stackoverflow.posts_questions\` 
 GROUP BY year 
 ORDER BY year DESC"
```

- Usuários com maior reputação:   
```
bq query --nouse_legacy_sql \
"SELECT display_name, reputation 
 FROM \`bigquery-public-data.stackoverflow.users\` 
 ORDER BY reputation DESC 
 LIMIT 10"
```

- Total de perguntas sem respostas:   
```
bq query --nouse_legacy_sql \
"SELECT COUNT(*) as unanswered_questions 
 FROM \`bigquery-public-data.stackoverflow.posts_questions\` 
 WHERE answer_count = 0"
```

- Top 5 usuários mais ativos:   
```
bq query --nouse_legacy_sql \
"SELECT owner_user_id, COUNT(*) as post_count 
 FROM \`bigquery-public-data.stackoverflow.posts_questions\` 
 WHERE owner_user_id IS NOT NULL 
 GROUP BY owner_user_id 
 ORDER BY post_count DESC 
 LIMIT 5"

```

-  Repositórios mais populares:  
```
bq query --nouse_legacy_sql \
"SELECT repo_name, COUNT(*) as commits 
 FROM \`bigquery-public-data.github_repos.sample_commits\` 
 GROUP BY repo_name 
 ORDER BY commits DESC 
 LIMIT 10"
```

-  Total de commits por ano:  
```
bq query --nouse_legacy_sql \
"SELECT EXTRACT(YEAR FROM committer.date) as year, COUNT(*) as total_commits 
 FROM \`bigquery-public-data.github_repos.sample_commits\` 
 GROUP BY year 
 ORDER BY year DESC"

```
E por ai vai, esses são só alguns exemplos que você pode reproduzir para gerarmos os logs de execução, exemplo do retorno da execução da ultima consulta

![image](https://github.com/user-attachments/assets/67e021fe-eed1-4b06-aba4-4685b5a5ac8d)

---

8. ** Exibindo os registros no bigquery**

   - Volte para o bigquery -> expanda o projeto conforme a imagem abaixo -> identifique o conjunto de dados criado -> expanda também e se tudo correu certo você vai visualizar a tabela *cloudaudit_googleapis_*
     
PS: A tabela cloudaudit_googleapis_com_data_access é uma tabela de logs no Google Cloud Logging que registra eventos relacionados ao acesso a dados em recursos do Google Cloud. Esses eventos incluem operações como leitura, gravação, exclusão ou consulta de dados em serviços como BigQuery, Cloud Storage, Firestore, entre outros.
PS1: Caso a tabela não apareça, feche o cloud shell, abra novamente, reexecute as querys.
PS2: Os logs de acesso a dados estão desativados por padrão em muitos serviços, para evitar custos adicionais. Eles precisam ser ativados explicitamente nas configurações de Cloud Logging ou pelo IAM Policy.
PS3: **Cuidado com Custos**, o volume de logs pode ser significativo dependendo do número de operações no ambiente. Para otimizar custos:
- Configure filtros para exportar apenas os logs relevantes.
- Defina políticas de retenção para logs antigos.

   ![image](https://github.com/user-attachments/assets/bfe49e3b-0120-4716-a022-27ccb1f87ac1)

- Clique no nome dessa nova tabela, você vai conseguir visualizar uma grande quantidade de campos

  ![image](https://github.com/user-attachments/assets/9a2ea7aa-9555-4187-b2f5-ef604b645c58)

---

9. ** Deixando a tabela mais 'utilizavel' **

    - Vamos criar um visualização,  que extrai um subconjunto de campos e realiza alguns cálculos a fim de derivar uma métrica para o tempo de consulta.
    - Para identificar o ID do seu projeto, clique nos três pontinhos, e clique em *copiar id*


  ![image](https://github.com/user-attachments/assets/2d589854-6181-44c7-b6d6-c79a374df3d3)

 ```
CREATE OR REPLACE VIEW
  devfest_logs.v_querylogs AS
SELECT
  resource.labels.project_id,
  protopayload_auditlog.authenticationInfo.principalEmail,
  protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobConfiguration.query.query,
  protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobConfiguration.query.statementType,
  protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatus.error.message,
  protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.startTime,
  protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.endTime,
  TIMESTAMP_DIFF(protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.endTime,           protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.startTime, MILLISECOND)/1000 AS run_seconds,
  protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.totalProcessedBytes,
  protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.totalSlotMs,
  ARRAY(SELECT as STRUCT datasetid, tableId FROM UNNEST(protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.referencedTables)) as tables_ref,
  protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.totalTablesProcessed,
  protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobStatistics.queryOutputRowCount,
  severity
FROM
  `<ID_DO_SEU_PROJETO>`
ORDER BY
  startTime
``` 
- Clique em *executar*, tudo correndo bem você vai receber esse retorno:
  ![image](https://github.com/user-attachments/assets/ac75ffa9-d649-44d4-93b1-ff6dc9e2ec0f)

---

10. ** Visualizando a 'visualização' **
    - Execute a seguinte consulta
      
```
SELECT * FROM bq_logs.v_querylogs
```


![image](https://github.com/user-attachments/assets/aba042e0-4c68-4b50-9929-7f82fb83885f)

Descrição dos campos

resource.labels.project_id

Retorna o ID do projeto associado ao recurso onde a consulta foi executada.
Ajuda a identificar o projeto em um ambiente com múltiplos projetos.
protopayload_auditlog.authenticationInfo.principalEmail

Mostra o e-mail do usuário ou serviço que executou a query.
Útil para auditoria e rastreamento de quem executou consultas.
protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobConfiguration.query.query

Contém o texto da query executada.
Permite revisar as consultas para entender o comportamento ou depurar erros.
protopayload_auditlog.servicedata_v1_bigquery.jobCompletedEvent.job.jobConfiguration.query.statementType

Indica o tipo de instrução SQL executada:
Exemplos: SELECT, INSERT, CREATE, MERGE.
Ajuda a categorizar as consultas realizadas.
protopayload_auditlog.servicedata_v1_bigquery.job.jobStatus.error.message

Mostra a mensagem de erro, caso a query tenha falhado.
Útil para identificar e resolver problemas nas consultas.
protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.startTime

Marca o timestamp de início da execução da query.
Usado para calcular duração ou analisar picos de uso.
protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.endTime

Marca o timestamp de término da execução da query.
Combinado com startTime, permite calcular a duração da consulta.
TIMESTAMP_DIFF(protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.endTime, protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.startTime, MILLISECOND)/1000 AS run_seconds

Calcula o tempo total de execução da query em segundos.
Ajuda a identificar consultas lentas ou gargalos de desempenho.
protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.totalProcessedBytes

Retorna o número total de bytes processados pela consulta.
Essencial para monitorar custos no BigQuery, já que cobranças estão atreladas ao volume processado.
protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.totalSlotMs

Mostra o número total de milissegundos de slot usados pela consulta.
Mede o consumo de recursos computacionais (slots) durante a execução.
ARRAY(SELECT AS STRUCT datasetId, tableId FROM UNNEST(protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.referencedTables)) AS tables_ref

Lista as tabelas referenciadas pela consulta, com os campos:
datasetId: Nome do dataset.
tableId: Nome da tabela.
Útil para mapear dependências e identificar o impacto da consulta em outros recursos.
protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.totalTablesProcessed

Indica o número total de tabelas processadas durante a execução da query.
Relevante para consultas que combinam dados de várias tabelas.
protopayload_auditlog.servicedata_v1_bigquery.job.jobStatistics.queryOutputRowCount

Mostra o número total de linhas de saída geradas pela query.
Ajuda a avaliar a eficiência da consulta, especialmente para análises ou pipelines.
severity

Indica o nível de severidade do evento:
Valores comuns: INFO, ERROR, WARNING.
Útil para priorizar problemas ou identificar logs importantes.

11. ** Looker Studio **

    - Ainda no bigquery, localize o botão de 'explorar dados', clique nele e selecione *explorar com o looker studio*
      ![image](https://github.com/user-attachments/assets/e7d56dd0-6878-48af-955a-7c4b6dfd6527)

- A proxima tela que você vai vai é a do *looker studio*, que já vem com algumas coisinhas na tela
  
![image](https://github.com/user-attachments/assets/f8b3455a-5c3f-40f7-ac77-aac99df9e143)

- Agora vamos criar alguns gráficos para gerar o nosso relatorio, sempre visando em entregar valor de forma rapida e simplificada,
- 
  



## 📖 **Documentação e Recursos**

- [BigQuery Documentation](https://cloud.google.com/bigquery/docs)
- [Google Cloud Logging](https://cloud.google.com/logging/docs)
- [Looker Studio](https://datastudio.google.com)
- [CLI gcloud](https://cloud.google.com/sdk/gcloud)

---

