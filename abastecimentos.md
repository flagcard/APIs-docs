# Integração Flagcard - API Abastecimentos  
  
A Flagcard atende duas formas de integrações com sistemas parceiros/terceiros para sicronização de abastecimentos.  
  
## Flagcard envia abastecimento para sistema parceiro/terceiro  
Quando um abastecimento for concluído na máquina da Flagcard de forma imediata, com um delay de até 3 minutos,  a Flagcard enviará automaticamente o abastecimento para o sistema parceiro/terceiro via API requisição HTTP padrão REST. Geralmente, chamamos uma API do sistema parceiro passando os seguintes dados:  
  
```  
Metodo: POST  
Hader: Content-Type: application/json  
Data:  
{  
"user":"PHZ-5G08",  //Número do Cartão
"city":"Manaus",    // Cidade localizada o abastecimento
"plate":"PHZ5G08",  // Placa do veículo (abastecimento frota)
"mileage": 51431.00,   //KM do veículo
"average_consumption":"2.97 km/L",   //Consumo Médio
"driver":"FERNANDO PAIVA COSTA",   //Motorista
"driver_document":"38820612339",   //CPF do Motorista
"function":"-",  //Cargo do motorista
"store":"Auto Posto Aleixo 1",  // Posto de abastecimento
"employer":"ROBERT DOS SANTOS",  //Frentista
"price": 6.59,   //Preço
"quantity": 157.00,   //Volume em LT
"value": 1034.63,  //Subtoal em R$
"discount": 29.83,  //Desconto se houver em R$
"total": 1004.80,  //Total em R$
"product":"Óleo Diesel S-10",   //Produto
"department":"-",  // Departamento que o cartão está cadastrado
"center":"-",  //Centro de custo que o cartão está cadastrado
"date":"17/11/2022 06:47",   //Data e Hora do abastecimento
}
```

## Flagcard recebe chamada do sistema parceiro/terceiro
Neste caso, o sistema parceiro/terceiro que chama a Flagcard para recuperar os dados de abastecimentos de acordo com a própria política do sistema parceiro. Por exemplo, o sistema parceiro é configurado para todos os dias as 22h:00m ir no sistema Flagcard sincronizar os abastecimentos que ocorreram no dia. Geralmente, liberamos um acesso seguro para o sistema parceiro conseguir recuperar os dados. O sistema parceiro chama uma rota da Flagcard via API Rest e a Flagcard retorna uma resposta com uma lista de abastecimentos de acordo com os parâmetros enviado na requisição.

```  
Metodo: GET
Rota: /get_transactions?dateFrom=01_06_2020&dateTo=02_06_2020
Hader: Content-Type: application/json  
Response:  
[
{  
"user":"PHZ-5G08",  //Número do Cartão
"city":"Manaus",    // Cidade localizada o abastecimento
"plate":"PHZ5G08",  // Placa do veículo (abastecimento frota)
"mileage": 51431.00,   //KM do veículo
"average_consumption":"2.97 km/L",   //Consumo Médio
"driver":"FERNANDO PAIVA COSTA",   //Motorista
"driver_document":"38820612339",   //CPF do Motorista
"function":"-",  //Cargo do motorista
"store":"Auto Posto Aleixo 1",  // Posto de abastecimento
"employer":"ROBERT DOS SANTOS",  //Frentista
"price": 6.59,   //Preço
"quantity": 157.00,   //Volume em LT
"value": 1034.63,  //Subtoal em R$
"discount": 29.83,  //Desconto se houver em R$
"total": 1004.80,  //Total em R$
"product":"Óleo Diesel S-10",   //Produto
"department":"-",  // Departamento que o cartão está cadastrado
"center":"-",  //Centro de custo que o cartão está cadastrado
"date":"17/11/2022 06:47",   //Data e Hora do abastecimento
},
...
]
```


