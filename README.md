# 🌐 "Googol" Full-Stack Search Platform

**Tecnologias:** Java RMI, Spring Boot, APIs REST, HTML/CSS/JavaScript, API da OpenAI, Ngrok, Jsoup

## Resumo do Projeto
O Googol é uma plataforma completa de motor de pesquisa distribuído, desenvolvida de raiz, que evoluiu de uma arquitetura backend distribuída para uma aplicação Web totalmente funcional. Inclui um sistema paralelo de Web Crawling, ordenação de resultados de pesquisa por popularidade e uma arquitetura multi-camada que comunica via RMI. 

Na sua evolução final, o Googol integra um servidor Web que permite aos utilizadores indexar URLs e efetuar pesquisas através de um navegador. Conta ainda com integrações REST com o Hacker News e a API da OpenAI para fornecer resumos de pesquisa inteligentes e indexar conteúdo externo popular.

---

## Arquitetura do Sistema
O software baseia-se numa arquitetura distribuída, utilizando o padrão MVC para o Servidor Web e RPC/RMI para a comunicação no backend:

1. **Gateway:** Atua como intermediário entre os clientes (tanto o Cliente RMI como o Servidor Web) e os Barrels. Gere uma fila de URLs à espera de processamento e distribui os pedidos dos clientes pelos Barrels ativos via RMI.
2. **Barrels (Armazenamento de Índice):** Os servidores centrais que armazenam o índice invertido (`processed`), ligando palavras-chave a URLs, e o índice de popularidade (`reachable`), que liga um URL a outros URLs que apontam para ele. Estes servidores processam a lógica de pesquisa e devolvem os resultados à Gateway. 
3. **Downloaders (Web Crawlers):** Trabalham em paralelo através de múltiplos terminais para analisar páginas web, extraindo texto e metadados (utilizando bibliotecas como o Jsoup), e enviando a informação processada de volta aos Barrels através da Gateway.
4. **Servidor Web:** Substitui o Cliente RMI (desktop) básico. Fornece uma interface moderna que permite aos utilizadores aceder às mesmas funcionalidades em diferentes dispositivos, lidando com pedidos de pesquisa e exibindo resultados ordenados por popularidade (agrupados de 10 em 10).

---

## Principais Funcionalidades
* **Indexação de URLs:** Introdução manual de um URL para ser analisado e indexado.
* **Web Crawling Recursivo:** Processa automaticamente as ligações (links) encontradas nas páginas visitadas usando uma fila de URLs.
* **Motor de Pesquisa:** Pesquisa de termos e devolução de resultados contendo o URL, o título e uma pequena citação de texto.
* **Ordenação por Popularidade:** Os resultados da pesquisa são ordenados com base no número de ligações de entrada (importância).
* **Consulta de Ligações de Entrada:** Visualização exata de quais as páginas conhecidas que apontam para um URL específico.
* **Integrações com APIs REST:** 
  * **Hacker News:** Indexação das principais notícias (top stories) do Hacker News que contenham os termos pesquisados.
  * **OpenAI (Resumos IA):** Geração de uma análise textual contextualizada baseada nos termos de pesquisa e nas citações dos resultados, utilizando a API Chat Completions da OpenAI.

---

## Como Executar o Projeto

**Pré-requisitos:** * Certifique-se de que o seu sistema operativo utiliza os carateres de fim de linha corretos para os scripts shell. Se estiver a usar o Windows, é altamente recomendável usar ficheiros `.cmd`.
* Modifique os endereços IP e os números das portas nos ficheiros de configuração se as predefinidas estiverem ocupadas.

**Passos de Execução:**
Abra janelas de terminal separadas para cada um dos seguintes passos:

1. **Compilar e Executar a Gateway:**
   Execute o script `build.sh` para compilar as classes. No mesmo terminal, execute `run-gateway.sh` para inicializar o servidor Gateway.
2. **Executar os Barrels:**
   Execute `run-barrel.sh` para inicializar o armazenamento do índice.
3. **Executar os Downloaders:**
   Execute `run-downloader.sh`. O downloader começará imediatamente a navegar pelas páginas web e a processar dados. *(Nota: Execute vários terminais downloader em simultâneo para aumentar a velocidade de rastreio e o tamanho do índice).*
4. **Executar o Cliente:**
   Execute `run-client.sh` para abrir a interface. Aqui pode pesquisar, adicionar novos URLs e consultar as ligações de entrada.
5.  **Aceder via Internet (Ngrok):**
    Para expor a sua plataforma e permitir o acesso externo, abra um novo terminal e utilize o ngrok apontando para a porta do seu servidor Web:
    ```cmd
    ngrok http 8080
    ```
    (Substitua `8080` pela porta que estiver a utilizar no seu sistema). Copie o URL público gerado (ex: `https://xyz.ngrok-free.app`) e abra-o no seu navegador.
---
