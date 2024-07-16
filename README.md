# Estoque
Exemplo para testes

 Scripts de Testes Automatizados

 1. Backend (API)

python

    import requests 
     def test_create_entry():
     response = requests.post('http://api.exemplo.com/estoque', json={
        "data_entrada": "2023-06-01",
        "fornecedor": "Fornecedor Válido",
        "produto": "Produto A",
        "quantidade": 10,
        "lote": "Lote123",
        "perecivel": True,
        "data_validade": "2023-12-31"
    })
    assert response.status_code == 201
    assert response.json()['message'] == 'Entrada registrada com sucesso'


 2. Web (Front-End)
             
javascript 


      describe('Gerenciamento de Estoque', () => {
           it('Deve permitir a entrada de estoque com dados válidos', () => {
               cy.visit('/estoque');
               cy.get('#data_entrada').type('2023-06-01');
               cy.get('#fornecedor').select('Fornecedor Válido');
               cy.get('#produto').type('Produto A');
               cy.get('#quantidade').type('10');
               cy.get('#lote').type('Lote123');
               cy.get('#perecivel').check();
               cy.get('#data_validade').type('2023-12-31');
               cy.get('#salvar').click();
               cy.contains('Entrada registrada com sucesso');
           });
       });


 4. Mobile (Appium)

robot


      * Settings *
      Library    AppiumLibrary
      
      * Test Cases *
      Testar Entrada de Estoque em Mobile
          Open Application
          Input Data Entrada    2023-06-01
          Input Fornecedor    "Fornecedor Válido"
          Input Produto    "Produto A"
          Input Quantidade    10
          Input Lote    "Lote123"
          Select Produto Perecível
          Input Data Validade    2023-12-31
          Click Botão Salvar
          Should See Confirm Message    "Entrada registrada com sucesso"


---

 Testes Manuais

 Backend

1. Teste de Endpoint para Registro de Entrada
   - Verificar se o endpoint `/estoque` aceita dados válidos e retorna status 200.

2. Teste de Resposta com Dados Inválidos
   - Enviar dados com uma data de entrada futura e verificar se retorna erro 400.

 Frontend

1. Verificação da Interface de Estoque
   - Navegar até a página de gerenciamento de estoque e validar se todos os campos estão visíveis.

2. Teste de Funcionalidade do Botão Salvar
   - Preencher os campos e clicar em "Salvar", garantindo que a entrada é registrada corretamente.

---

 Utilização de SQL

 Consulta de Estoque

  sql
  
     SELECT * FROM estoque
     WHERE data_entrada < CURRENT_DATE
     ORDER BY data_entrada DESC;


 Script de Teste para Verificar Estoque

sql


    INSERT INTO estoque (data_entrada, fornecedor, produto, quantidade, lote, perecivel, data_validade)
    VALUES ('2023-06-01', 'Fornecedor Válido', 'Produto A', 10, 'Lote123', TRUE, '2023-12-31');

-- Verificar se o registro foi adicionado

    SELECT COUNT(*) FROM estoque WHERE produto = 'Produto A';
