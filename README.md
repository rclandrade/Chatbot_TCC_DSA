# 🤖 TCC-DSA-Helper: Assistente Inteligente com RAG (Azure AI)
**MBA em Data Science e Analytics - USP ESALQ**

Este repositório documenta a implementação de um sistema de **Retrieval-Augmented Generation (RAG)** hospedado no Azure. O projeto foi desenvolvido para atuar como um assistente técnico na organização e consulta de referências para o meu TCC.

## 🚀 Arquitetura da Solução
A solução utiliza uma abordagem de **Busca Vetorial (Vector Search)** para garantir que as respostas do modelo sejam fundamentadas em documentos específicos (Grounding), minimizando alucinações da IA.

### 📋 Pré-requisitos e Infraestrutura
* **Azure AI Services:** Modelos `gpt-4o` e `text-embedding-3-large`.
* **Azure AI Search:** Gerenciamento de índices e busca semântica.
* **Azure Blob Storage:** Repositório dos documentos brutos.

---

## 🛠️ Passo a Passo da Implementação

### 1. Governança e Segurança (IAM)
A segurança foi configurada via **Managed Identity**, eliminando a necessidade de chaves de API expostas no código. Atribui a função de *Storage Blob Data Contributor* para permitir que o serviço de IA acesse os documentos de forma segura.

![Configuração de Permissões](./img/Role_Assignments.jpeg)
*Figura 1: Atribuição de funções IAM garantindo acesso via Identidade Gerenciada ao recurso de armazenamento.*

### 2. Armazenamento de Dados
Criei um contêiner privado no **Azure Blob Storage** para servir como a base de conhecimento (Knowledge Base) do assistente.

![Estrutura de Contêineres](./img/Container.jpeg)
*Figura 2: Contêiner 'blob-storage' contendo os arquivos PDF/DOCX que alimentam o chatbot.*

### 3. Indexação e Busca Vetorial
O processo de ingestão converteu os documentos em vetores numéricos utilizando o modelo de embedding. Isso permite que o sistema entenda o contexto das perguntas, não apenas palavras-chave.

![Configuração do Índice](./img/MLIndex.jpeg)
*Figura 3: Criação do índice de busca integrando o Azure AI Search com suporte a Vector Search.*

### 4. Orquestração de Modelos
Utilizei o **Azure AI Foundry** para gerenciar os deployments. O sistema utiliza dois modelos em paralelo: um para processar o chat e outro para processar os vetores de busca.

![Modelos Implantados](./img/Model_deployments.jpeg)
*Figura 4: Status dos deployments para os modelos GPT-4o e Text-Embedding-3-Large.*

### 5. Validação no Playground
Antes da integração final, o sistema foi validado no ambiente de testes do Azure para garantir que o fluxo de recuperação de dados (Retrieval) estava funcionando corretamente.

![Ambiente de Testes](./img/Playground.jpeg)
*Figura 5: Interface de configuração do Chat Playground no Azure AI Foundry.*

---

## 📈 Resultados: Chatbot em Ação (RAG)
O resultado final demonstra a IA respondendo perguntas complexas sobre o TCC, apresentando **citações diretas** dos documentos armazenados.

![Resposta com RAG](./img/Chat_response_RAG.jpeg)
*Figura 6: Demonstração da IA gerando respostas baseadas nos documentos (Grounding) com citações de fonte.*

---

## ⚙️ Desafios Superados
Durante o desenvolvimento, enfrentei restrições de permissão de Tenant no Microsoft Entra ID. A solução foi focar na robustez do pipeline de dados e na validação via Playground, garantindo que a inteligência do sistema estivesse 100% funcional independente da interface de publicação.
