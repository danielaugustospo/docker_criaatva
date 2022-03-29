## SISTEMA DE GERENCIAMENTO FINANCEIRO COM LARAVEL 5.8


Para facilitar o desenvolvimento, adicionei o projeto no Docker, entretanto, a partir deste arcabouço é possível vislumbrar uma integração contínua e evoluir ainda mais em uma melhor forma para desenvolver e para o deploy da aplicação. 

Criei esta imagem com o PHP 7.3.33 + MySQL e PHPMyAdmin

**Comandos para levantar e/ou parar os containeres**
**Criar e levantar os containers**
docker-compose up -d

**Iniciar o container Docker**
docker-compose start

**Parar o container Docker**
docker-compose stop

**Parar e remover containers da máquina**
docker-compose down

**Acesso localhost**
```txt
http://localhost:4500
```

**Acesso phpMyAdmin**
```txt
http://localhost:8080

login: root
senha: root
```


# COMANDOS PARA INICIAR A APLICAÇÃO


php artisan make:migration create_users_table --create=users

Foi criado um link simbólico para a pasta storage em public. Para gerar esse comando no servidor, execute:

php artisan storage:link

CASO PRECISE FORÇAR UMA NOVA MIGRAÇÃO, O COMANDO ABAIXO É BEM ÚLTIL. AVISO: USE SOMENTE SE NECESSÁRIO! 
php artisan migrate --force

//ZERAR AS TABELAS
php artisan migrate:refresh

php artisan db:seed --class=PermissionTableSeeder
php artisan db:seed --class=CreateAdminUserSeeder

//ZERAR OS SEEDS...
php artisan migrate:refresh --seed


# OBSERVAÇÃO
O cliente tinha o seu sistema no MS Access. Dito isto, foi realizado um procedimento de importação de dados. Isto é detalhado com mais ênfase no arquivo Procedimentos.txt
----------------------------------------------------------------------------------------------------------------------------
## Instalação Validador Docs

No arquivo `composer.json`, adicione validator-docs como dependência do seu projeto:

```
"require": {
    "geekcom/validator-docs" : "^3.3"
 },
```

Depois execute:

```
composer install
```

Ou simplesmente execute o comando:

```
composer require geekcom/validator-docs
```

----------------------------------------------------------------------------------------------------------------------------

## Validações disponíveis

Agora, você terá os métodos de validação validator docs Brasil disponíveis.

* **cpf** - Verifica se um CPF é valido.

```php
$this->validate($request, [
    'cpf' => 'required|cpf',
]);
```

* **cnpj** - Verifica se um CNPJ é valido.

```php
$this->validate($request, [
    'cnpj' => 'required|cnpj',
]);
```

* **cnh** - Verifica se uma CNH (Carteira Nacional de Habilitação) é válida.

```php
$this->validate($request, [
    'cnh' => 'required|cnh',
]);
```

* **titulo_eleitor** - Verifica se um Título de Eleitor é válido.

```php
$this->validate($request, [
    'titulo_eleitor' => 'required|titulo_eleitor',
]);
```

* **cpf_cnpj** - Verifica se um CPF ou CNPJ é válido.

```php
$this->validate($request, [
    'cpf_cnpj' => 'required|cpf_cnpj',
]);
```

* **nis** - Verifica se um PIS/PASEP/NIT/NIS é válido.

```php
$this->validate($request, [
    'nis' => 'required|nis',
]);
```

* **cns** - Verifica se um Cartão Nciona de Saúde (CNS) é válido.

```php
$this->validate($request, [
    'cns' => 'required|cns',
]);
```

* **certidao** - Verifica se uma certidão de nascimento/casamento/óbito é válida.

```php
$this->validate($request, [
    'certidao' => 'required|certidao',
]);
```

* **formato_cnpj** - Verifica se o formato de um CNPJ é válida. ( 99.999.999/9999-99 )

```php
$this->validate($request, [
    'formato_cnpj' => 'required|formato_cnpj',
]);
```

* **formato_cpf** - Verifica se o formato de um CPF é válido. ( 999.999.999-99 )

```php
$this->validate($request, [
    'formato_cpf' => 'required|formato_cpf',
]);
```

* **formato_cpf_cnpj** - Verifica se o formato de um CPF ou um CNPJ é válido. ( 999.999.999-99 ) ou ( 99.999.999/9999-99 )

```php
$this->validate($request, [
    'formato_cpf_cnpj' => 'required|formato_cpf_cnpj',
]);
```

* **formato_nis** - Verifica se o formato de um PIS/PASEP/NIT/NIS é válido. ( 999.99999-99.9 )

```php
$this->validate($request, [
    'formato_nis' => 'required|formato_nis',
]);
```

* **formato_certidao** - Verifica se o formato de uma certidão é válida. ( 99999.99.99.9999.9.99999.999.9999999-99 ou 99999 99 99 9999 9 99999 999 9999999 99)

```php
$this->validate($request, [
    'formato_certidao' => 'required|formato_certidao',
]);
```
----------------------------------------------------------------------------------------------------------------------------

## Combinando validação e formato

No exemplo abaixo, fazemos um teste onde verificamos a formatação e a validade de um CPF ou CNPJ, para os casos onde a informação deve ser salva em um mesmo atributo:

```php
$this->validate($request, [
    'cpf_or_cnpj' => 'formato_cpf_cnpj|cpf_cnpj',
]);
```

----------------------------------------------------------------------------------------------------------------------------

## Exemplo de uso em um controller

Método de validação de exemplo em um controller com todas as possibilidades de validação

```php
public function store(Request $request)
{
    $data = $request->all();

    $this->validate($request, [
        'cpf' => 'required|cpf',
        'cnpj' => 'required|cnpj',
        'cnh' => 'required|cnh',
        'titulo_eleitor' => 'required|titulo_eleitor',
        'nis' => 'required|nis',
        'cns' => 'required|cns',
    ]);

    dd($data);
}
```
## Documentação select2
https://select2.org/configuration

----------------------------------------------------------------------------------------------------------------------------

## Geradores de documentos para testes

* **CNH** - http://4devs.com.br/gerador_de_cnh
* **TÍTULO ELEITORAL** - http://4devs.com.br/gerador_de_titulo_de_eleitor
* **CNPJ** - http://www.geradorcnpj.com/
* **CPF** - http://geradordecpf.org
* **NIS** - https://www.4devs.com.br/gerador_de_pis_pasep
* **CNS** - https://geradornv.com.br/gerador-cns/
* **CERTIDÃO** - https://www.treinaweb.com.br/ferramentas-para-desenvolvedores/gerador/certidao

