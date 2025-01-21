# Criação de um Banco de dados relacional de um modelo de E-commerce

## Estrutura desenvolvida como desafio de projeto do *Bootcamp* Suzano - Análise de Dados com Power BI - DIO


## Objetivo

O script apresentado abaixo SQL cria um banco de dados relacional para um sistema de e-commerce. As tabelas criadas armazenam informações sobre **clientes, produtos, fornecedores, vendedores, pedidos, estoques**, e os relacionamentos necessários para a operação do sistema. 

## Estrutura do Banco de Dados 

### Banco de Dados

-   **`ecommerce`**: O banco de dados principal criado para armazenar todas as tabelas relacionadas ao sistema.

### Tabelas

1.  **`clients`**
    -   **Descrição**: Armazena informações sobre os clientes do sistema.
    -   **Colunas**:
        -   `idClient`: Chave primária única (incremental).
        -   `Fname`, `Minit`, `Lname`: Nome completo do cliente.
        -   `CPF`: Cadastro de Pessoa Física, único e obrigatório.
        -   `Address`: Endereço do cliente.
    -   **Constraints**:
        -   `NOT NULL`: O CPF não pode ser nulo.
        -   `UNIQUE`: Garantia de que o CPF é único.

2.  **`product`**
    -   **Descrição**: Armazena informações sobre os produtos disponíveis.
    -   **Colunas**:
        -   `idProduct`: Chave primária única (incremental).
        -   `Pname`: Nome do produto.
        -   `classification_kids`: Indica se é voltado para crianças.
        -   `category`: Enum com as categorias possíveis do produto.
        -   `size`: Tamanho do produto.
    -   **Constraints**:
        -   `NOT NULL`: Categoria e nome são obrigatórios.
        -   Valores padrão: `classification_kids` inicia como falso.

3.  **`payments`**
    -   **Descrição**: Relaciona métodos de pagamento de cada cliente.
    -   **Colunas**:
        -   `idClient`: Relaciona-se ao cliente.
        -   `idPayment`: Identifica o método de pagamento.
        -   `typePayment`: Enum dos tipos de pagamento.
        -   `limitAvailable`: Limite de crédito disponível.
    -   **Chave Primária**: Combinação de `idClient` e `idPayment`.

4.  **`orders`**
    -   **Descrição**: Representa pedidos feitos pelos clientes.
    -   **Colunas**:
        -   `idOrder`: Chave primária única.
        -   `idOrderClient`: Relaciona-se ao cliente.
        -   `orderStatus`: Status do pedido.
        -   `orderDescription`: Descrição do pedido.
        -   `sendValue`: Valor de envio, padrão `10`.
        -   `paymentCash`: Indica pagamento em dinheiro.
    -   **Constraints**:
        -   `FOREIGN KEY`: Relaciona-se à tabela `clients`.

5.  **`productStorage`**
    -   **Descrição**: Gerencia o estoque dos produtos.
    -   **Colunas**:
        -   `idProdStorage`: Chave primária.
        -   `storageLocation`: Local de armazenamento.
        -   `quantity`: Quantidade de produtos disponíveis.

6.  **`supplier`**
    -   **Descrição**: Armazena informações sobre fornecedores.
    -   **Colunas**:
        -   `idSupplier`: Chave primária única.
        -   `SocialName`: Nome social do fornecedor.
        -   `CNPJ`: Cadastro Nacional de Pessoa Jurídica, único.
        -   `contact`: Contato do fornecedor.
    -   **Constraints**:
        -   `UNIQUE`: Garante que o CNPJ não seja duplicado.

7.  **`seller`**
    -   **Descrição**: Armazena informações sobre vendedores.
    -   **Colunas**:
        -   `idSeller`: Chave primária única.
        -   `SocialName`, `AbstName`: Nome social e abreviado.
        -   `CNPJ`, `CPF`: Identificação única para vendedores.
        -   `location`, `contact`: Localização e contato.
    -   **Constraints**:
        -   `UNIQUE`: Garante unicidade do CNPJ e CPF.

### Tabelas de Relacionamento

1.  **`productSeller`**
    
    -   Relaciona produtos com vendedores.
    -   Chave primária composta por `idPseller` e `idPproduct`.
2.  **`productOrder`**
    
    -   Relaciona produtos com pedidos.
    -   Chave primária composta por `idPOproduct` e `idPOorder`.
3.  **`storageLocation`**
    
    -   Relaciona produtos com locais de armazenamento.
    -   Chave primária composta por `idLproduct` e `idLstorage`.
    - 
4.  **`productSupplier`**
    
    -   Relaciona produtos com fornecedores.
    -   Chave primária composta por `idPsSupplier` e `idPsProduct`.

## Diagrama de Esquema Relacional

- O esquema relacional pode ser refletido em diagramas visuais para melhor entendimento dos relacionamentos.  
- **Relatórios Pendentes:** Finalizar o diagrama para refletir todas as tabelas e suas relações.

## Considerações Finais

Este banco de dados oferece suporte às principais operações de um sistema de e-commerce. Ele inclui validações robustas com **constraints** para garantir a consistência dos dados. Ainda há espaço para melhorias e extensões, como:

1.  **Implementação de triggers** para atualizar o estoque automaticamente.
2.  **Criação de índices** para melhorar a performance de consultas frequentes.
3.  **Documentação visual** para facilitar o entendimento da estrutura do banco.
