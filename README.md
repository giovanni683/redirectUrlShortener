# Redirect URL Shortener

Esta aplicação é uma API para redirecionamento de URLs encurtadas, implementada utilizando AWS Lambda, S3 e Java. A aplicação valida se a URL ainda é válida e redireciona o usuário ou informa se a URL expirou.

## Tecnologias Utilizadas

- **Java 17**
- **AWS Lambda** para execução serverless
- **AWS S3** para armazenamento dos dados das URLs
- **Jackson** para manipulação de JSON
- **Lombok** para reduzir boilerplate no código
- **Maven** para gerenciamento de dependências e build

## Estrutura do Projeto

- **Main.java**: Contém a lógica principal para o redirecionamento da URL.
- **UrlData.java**: Classe que representa os dados da URL armazenados no S3.
- **pom.xml**: Configurações e dependências do projeto.

## Como Funciona

1. **Input**: O código da URL encurtada é passado na URL da requisição.
2. **Processamento**:
   - A aplicação busca os dados correspondentes no bucket do S3.
   - Verifica se a URL ainda é válida.
3. **Output**:
   - Redireciona o usuário para a URL original caso seja válida.
   - Retorna um código HTTP `410` (Gone) caso tenha expirado.

## Como Configurar

1. **Pré-requisitos**:
   - Java 17 instalado.
   - Configuração do AWS CLI com permissões para acessar o bucket S3.

2. **Instalação**:
   - Clone o repositório:
     ```bash
     git clone https://github.com/giovanni683/redirectUrlShortener.git
     cd redirectUrlShortener
     ```

   - Compile o projeto com Maven:
     ```bash
     mvn clean package
     ```

3. **Deploy no AWS Lambda**:
   - Empacote a aplicação como um arquivo JAR.
   - Faça o upload do JAR no AWS Lambda e configure o handler como:
     ```
     com.rocketseat.creatUrlShortener.Main::handleRequest
     ```

4. **Configuração do Bucket S3**:
   - Crie um bucket S3 com o nome `url-short-stg`.
   - Armazene os arquivos JSON no formato:
     ```json
     {
       "originalUrl": "https://example.com",
       "expirationTime": 1700000000
     }
     ```

## Testes Locais

- Execute a aplicação localmente (requer um ambiente que simule o AWS Lambda).
