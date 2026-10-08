# 🤖 Bot de Monitoramento Diário: Concursos DF & Entorno

Este projeto consiste em uma automação inteligente e totalmente independente desenvolvida no **n8n** e hospedada localmente via **Docker**. O fluxo consome dados em tempo real de portais de notícias locais, utiliza a API do **Google Gemini (2.5 Flash)** para filtragem cognitiva e formatação dos textos, e envia alertas diários estruturados diretamente para o **Telegram**.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas

* **Hospedagem:** Docker Desktop (Contêiner isolado do n8n)
* **Orquestração de Fluxo:** n8n (Automação baseada em nós em linha)
* **Inteligência Artificial:** Google Gemini API (`models/gemini-2.5-flash`)
* **Interface de Saída:** Telegram Bot API

---

## 📋 Documentação do Processo de Configuração

### 1. Ambiente Local (Docker)
O painel do n8n foi inicializado e roda continuamente em segundo plano em um contêiner Docker local, garantindo baixo consumo de hardware (estabilizado em ~0.17% de CPU) e funcionamento 24/7 sem dependência de servidores de terceiros.

### 2. Captação de Dados (HTTP Requests)
O fluxo executa requisições do tipo `GET` em portais agregadores regionais (como o canal de feed da *globo.com* e o portal *Ache Concursos DF*). O nó de busca foi estruturado em sequência linear para otimizar o processamento e a paginação de dados.

### 3. Inteligência Artificial (Google AI Studio)
Cadastramos uma credencial segura utilizando uma chave de API gratuita gerada no Google AI Studio. 
* **Prompt Engenharia:** O modelo foi treinado com regras rígidas para ignorar termos de desenvolvimento (ex: "com base no HTML fornecido"), focar puramente em editais com lotação ou provas no Distrito Federal e municípios do Entorno (Goiás), e padronizar o layout com emojis visuais (💰 para salários e 🔗 para links de editais).

### 4. Entrega dos Alertas (Telegram)
Utilizando o `@BotFather`, criamos a identidade visual e o token do bot (`@ConcursosDFAgente_bot`). Através do `@userinfobot`, extraímos o ID numérico de chat exclusivo do administrador para garantir o envio direto e privado dos informativos todas as manhãs.

---

## 🔒 Notas de Segurança

* **Isolamento de Credenciais:** Este repositório é totalmente seguro. O n8n remove automaticamente todos os Tokens de Acesso do Telegram e API Keys do Google Gemini ao exportar o arquivo de fluxo. 
* **Execução Segura:** Caso vá rodar o fluxo em produção, lembre-se de nunca expor suas chaves privadas no código-fonte ou no histórico de commits.
