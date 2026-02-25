# 🤖 TCC-DSA-Helper: Chatbot RAG para Assistência de TCC
**Curso:** MBA em Data Science e Analytics - USP ESALQ

Este projeto consiste na implementação de um chatbot inteligente utilizando a arquitetura **RAG (Retrieval-Augmented Generation)** no **Azure AI Foundry**. O objetivo é auxiliar na organização e consulta de referências bibliográficas e diretrizes do meu TCC.

## 🚀 Tecnologias Utilizadas
* **Azure AI Foundry:** Orquestração do projeto de IA.
* **Azure OpenAI:** Modelos `gpt-4o` (Chat) e `text-embedding-3-large` (Embeddings).
* **Azure AI Search:** Indexação e busca vetorial (Vector Search).
* **Azure Blob Storage:** Armazenamento dos documentos base.
* **App Service:** Hospedagem da interface web do chatbot.

## 🛠️ Passo a Passo da Implementação

### 1. Provisionamento de Infraestrutura
Configurei o ambiente no Azure garantindo que todos os recursos estivessem na mesma região para evitar latência e erros de validação.
* **Storage Account:** `chatdata9`
* **AI Search:** `diolabs9` (Tier Basic para suporte a vetores).

### 2. Gestão de Dados e Permissões (IAM)
Um dos pontos cruciais foi a configuração de **Managed Identities** para garantir a segurança sem exposição de chaves de API.
* Atribuição da Role **Storage Blob Data Contributor** para o projeto e para o serviço de busca.
> *Insira aqui a sua imagem [image_16781c.jpg] mostrando as permissões configuradas.*

### 3. Ingestão e Indexação Vetorial
Realizei o upload dos documentos para o contêiner `blob-storage` e configurei a indexação.
* **Busca Vetorial:** Utilizei o modelo `text-embedding-3-large` para transformar os documentos em vetores, permitindo uma busca semântica mais precisa.
> *Insira aqui a sua imagem [image_15f87d.png] da configuração de Vector Search.*

### 4. Deploy do Modelo e Playground
Implementei o modelo `gpt-4o` e validei a capacidade de resposta do bot utilizando a técnica de RAG no Playground do Azure.
> *Insira aqui a sua imagem [image_15f191.png] dos deployments ativos.*

## 📈 Resultados
O chatbot é capaz de responder perguntas complexas sobre o conteúdo do meu TCC, citando as fontes exatas armazenadas no Azure Blob Storage, garantindo respostas baseadas em fatos e reduzindo alucinações da IA.
