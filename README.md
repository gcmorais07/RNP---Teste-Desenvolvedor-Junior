# Teste Desenvolvedor Junior

1. Foi criado o Diagrama de ER do banco Ecommerce disponivel no link:
  (https://cloud.uibakery.io/edit/ganymede-latlux/Pj1iYtcszN/datasource/home).

2. Acessei a plataforma da UI Bakery (cloud.uibakery), inseri as credencias de acesso: 
	
	Host: psql-mock-database-cloud.postgres.database.azure.com
	Port: 5432
	Username: abxiorxmlzidpnezwgdptjyw@psql-mock-database-cloud
	Password: saganvmeokugonwsebaqmevw
	Database name: ecom1689965783799dvyygsjqihmigmwm
	
# RESPOSTAS DOS ITENS DO CASE

# item 1
```bash
Criado o diagrama: 'Diagrama ER - Ecommerce - GUILHERME DO CARMO DE MORAIS.png'
```
# item 2

```bash
2. Crie um notebook no Databricks Community:
			(NÃO FOI POSSIVEL REALIZAR ESSA ATIVIDADE 
			O LINK: https://community.cloud.databricks.com/login.html não permitiu a alteração da senha de acesso)
```
# item 3.1

```bash
3.1 - Qual país possui a maior quantidade de itens cancelados:

	Resposta:{country: "Spain",total_itens: "605"}

Query:
		select distinct 
		c.country pais,
		sum(dos.quantity_ordered) TOTAL_ITENS
		from public.customers c 
		left join public.orders os on c.customer_number = os.customer_number
		join orderdetails dos on dos.order_number = os.order_number
		where os.status='Cancelled'
		group by c.country order by sum(dos.quantity_ordered) desc limit 1

```

# item 3.2
```bash
3.2 - Qual o faturamento da linha de produto mais vendido, considere os itens com status 'Shipped', 
      cujo pedido foi realizado no ano de 2005?
      
	  Resposta:{product_line: "Motorcycles",faturamento: "11503.14"}

Query:	  
		select 
		(select distinct product_line from public.products pp
		 where pp.product_code = dos.product_code) product_line,
		(dos.quantity_ordered * dos.price_each) as faturamento

		from public.customers c 
		left join public.orders os on c.customer_number = os.customer_number
		join orderdetails dos on dos.order_number = os.order_number
		where os.status='Shipped'
		and date_part('Year',os.order_date)=2005
		order by (dos.quantity_ordered * dos.price_each) desc limit 1	

```

# item 3.3
```bash
3.3 - Nome, sobrenome e e-mail dos vendedores do Japão, o local-part do e-mail deve estar mascarado.

        Resposta:
		[
			{
				employee_number: 1621,
				sobrenome: "Nishi Mami",
				email_mascara: "***sh*@class*c*odelcars.co*"
			},
			{
				employee_number: 1625,
				sobrenome: "Kato Yoshimi",
				email_mascara: "***to@cl*ssicmodelc*rs.com"
			}
		]
Query:
		select 
		e.employee_number,
		last_name||' '||first_name sobrenome,
		translate(email, substring(email,1,3), '***') as email_mascara
		from public.employees e join public.offices o
		on e.office_code = o.office_code
		and o.country='Japan'	

```

# 4. Salve os resultados em formato delta
```bash
Todas as ações foram documentadas no README.md, pois não foi possivel realizar o item 2.
```

