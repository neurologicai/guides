Ruby
====

Este guia de estilo Ruby recomenda as melhores práticas para que os programadores Ruby do mundo real possam escrever código que possa ser mantido por outros programadores Ruby do mundo real.

- [Formatação e espaçamento](#formatação-e-espaçamento)
  - Formatação de arquivo
  - Espaços e Chaves
  - Chamadas de método
  - Linhas em branco
  - Literais de string

- [Nomenclatura](#nomenclatura)
  - Métodos Booleanos com Ponto de Interrogação
  - Prefixo para Métodos Booleanos
  - Capitalização
  - Variável de instância memorizada

- [Coleções](#coleções)
  - `%w`
  - `%i`
  - Hashes de várias linhas
  - Sem vírgula à direita do Array
  - Alinhamento de Arrays em Múltiplas Linhas
  - Símbolos como Chaves
  - Sintaxe de dois pontos em hash em vez de "foguete" (`=>`)

- [Operadores e Fluxo de Controle](#operadores-e-fluxo-de-controle)
  - Não use `and` ou `or`
  - Não deve haver espaço depois do `!` (beng) _ponto de exclamação_
  - Dupla Negação
  - Operador ternário (`?:`) vs `if`
  - `case` ao invés de `if-elsif`
  - Retornando Resultado do `if/case`
  - `unless` em vez de `if`
  - Não use o `unless` com o `else`
  - Loop Infinito
  - Evite o `return`

---------------------------------------------

# Formatação e espaçamento
## Formatação de arquivo
* Use recuo de 2 espaços (sem tabulações).
* Mantenha cada linha de código em um comprimento legível. A menos que você tenha um motivo para isso, mantenha as linhas com menos de 120 caracteres.
* Nunca deixe espaços em branco à direita.
* Termine cada arquivo com uma nova linha em branco.

## Espaços e chaves

Sem espaços após `(`, `[` ou antes de `]`, `)`.

```ruby
# ruim
some( arg ).other
[ 1, 2, 3 ].each{|e| puts e}

# bom
some(arg).other
[1, 2, 3].each { |e| puts e }
```

Para literais de hash, use espaços ao redor de `{` e antes de `}`.
```ruby
# good
{ one: 1, two: 2 }
```

Com expressões interpoladas, não use espaços ao redor de `{` e antes de `}`.

```ruby
# ruim
"From: #{ user.first_name }, #{ user.last_name }"

# bom
"From: #{user.first_name}, #{user.last_name}"
```

## Chamadas de método

Nunca coloque um espaço entre o nome de um método e o parêntese de abertura.

```ruby
# ruim
puts (3 + 2) + 1

# bom
puts(3 + 2) + 1
```

## Linhas vazias

Insira linhas vazias entre definições de método e entre parágrafos lógicos dentro de um método.

```ruby
# ruim
def do_something
  do_something_else
end
def do_something_else
  2 + 2
end

# bom
def do_something
  do_something_else
end

def do_something_else
  2 + 2
end

# ruim
def do_something
  @foo = 'foo'
  @bar = 'bar'
  if @foo == @bar
    puts 'foo is bar'
  else
    puts 'foo is not bar'
  end
  2 + 2
end

# bom
def do_something
  @foo = 'foo'
  @bar = 'bar'

  if @foo == @bar
    puts 'foo is bar'
  else
    puts 'foo is not bar'
  end

  2 + 2
end
```

Além disso, evite linhas vazias consecutivas.

```ruby
# ruim
def do_something
  do_something_else
end


def do_something_else
  2 + 2
end

# bom
def do_something
  do_something_else
end

def do_something_else
  2 + 2
end
```

## Literais de string

Prefira strings com aspas simples quando não precisar de interpolação de strings ou símbolos especiais como `\t`, `\n`, `'`, etc.

```ruby
# ruim
name = "Bozhidar"

name = 'De\'Andre'

# bom
name = 'Bozhidar'

name = "De'Andre"
```
Prefira aspas duplas, a menos que sua string literal contenha `"` ou caracteres de escape que você deseja suprimir.

```ruby
# ruim
name = 'Bozhidar'

sarcasm = "I \"like\" it."

# bom
name = "Bozhidar"

sarcasm = 'I "like" it.'
```

# Nomenclatura
## Métodos Booleanos com Ponto de Interrogação

Os nomes dos métodos predicados (métodos que retornam um valor booleano) devem terminar com um ponto de interrogação (ou seja, `Array#empty?`). Métodos que não retornam um booleano não devem terminar em ponto de interrogação.

## Prefixo de Métodos Booleanos

Evite prefixar métodos predicados com verbos auxiliares como `is`, `does` ou `can`. Essas palavras são redundantes e inconsistentes com o estilo dos métodos booleanos na biblioteca principal do Ruby, como `empty?` e `include?`.

```ruby
# ruim
class Person
  def is_tall?
    true
  end

  def can_play_basketball?
    false
  end

  def does_like_candy?
    true
  end
end

# bom
class Person
  def tall?
    true
  end

  def basketball_player?
    false
  end

  def likes_candy?
    true
  end
end
```

## Capitalização

1. **snake_case** 
* Para métodos e variáveis
* Para nomear diretórios, por exemplo: `lib/hello_world/hello_world.rb`.
* Para nomear arquivos, por exemplo: `hello_world.rb`.

2. Uma classe por arquivo
* Procure ter apenas uma única classe/módulo por arquivo de origem. Nomeie o nome do arquivo como classe/módulo, mas substituindo **CapitalCase** por **snake_case**.

3. **CamelCase** 
* Para Classes e módulos. (Mantenha siglas como HTTP, RFC, XML em maiúsculas.)

```ruby
# ruim
class Someclass
  # some code
end

class Some_Class
  # some code
end

class SomeXml
  # some code
end

class XmlSomething
  # some code
end

# bom
class SomeClass
  # some code
end

class SomeXML
  # some code
end

class XMLSomething
  # some code
end
```

4. **SCREAMING_SNAKE_CASE**
* Para outras constantes.

```ruby
# ruim
SomeConst = 5

# bom
SOME_CONST = 5
```

## Variável de instância memorizada

A variável de instância memorizada deve corresponder ao nome do método, para evitar confusão e bugs.

Em Ruby, a utilização de variáveis de instância memorizadas é comum em situações em que o cálculo ou a recuperação de um valor é custoso em termos de processamento ou tempo, mas o valor permanece constante ao longo do tempo. Em vez de recalcular o valor cada vez que ele é necessário, a variável é armazenada em cache na instância da classe e recuperada quando necessário.

```ruby
# ruim
def foo
  @something ||= calculate_expensive_thing
end

# ruim
def _foo
  @foo ||= calculate_expensive_thing
end

# ruim
def foo
  @_foo ||= calculate_expensive_thing
end

# bom
def foo
  @foo ||= calculate_expensive_thing
end
```

# Coleções

## `%w`

Prefira `%w` à sintaxe de array literal quando precisar de um array de palavras (strings não vazias sem espaços e caracteres especiais). Aplique esta regra apenas a arrays com dois ou mais elementos.

```ruby
# ruim
STATES = ['draft', 'open', 'closed']

# bom
STATES = %w[draft open closed]
```

## `%i`

Prefira `%i` à sintaxe de array literal quando precisar de um array de símbolos (e não precisar manter compatibilidade com Ruby 1.9). Aplique esta regra apenas a arrays com dois ou mais elementos.

```ruby
# ruim
STATES = [:draft, :open, :closed]

# bom
STATES = %i[draft open closed]
```

## Hashes de várias linhas

Use hashes de várias linhas quando tornar o código mais legível e use vírgulas à direita para garantir que as alterações de parâmetro não causem linhas de comparação estranhas quando a lógica não foi alterada.

```ruby
hash = {
  protocol: 'https',
  only_path: false,
  controller: :users,
  action: :set_password,
  redirect: @redirect_url,
  secret: @secret,
}
```

## Sem vírgula à direita do Array

Evite vírgula após o último item de um Array ou Hash literal, especialmente quando os itens não estiverem em linhas separadas.

```ruby
# ruim - é mais fácil de mover/adicionar/remover itens, mas não é indicado
VALUES = [
           1001,
           2020,
           3333,
         ]

# ruim
VALUES = [1001, 2020, 3333, ]

# bom
VALUES = [1001, 2020, 3333]
```

## Alinhamento de Arrays em Múltiplas Linhas

Alinhar os elementos de literais de arrays que abrangem várias linhas.

```ruby
# ruim - recuo simples
menu_item = %w[Spam Spam Spam Spam Spam Spam Spam Spam
  Baked beans Spam Spam Spam Spam Spam]

# bom
menu_item = %w[
  Spam Spam Spam Spam Spam Spam Spam Spam
  Baked beans Spam Spam Spam Spam Spam
]

# bom
menu_item =
  %w[Spam Spam Spam Spam Spam Spam Spam Spam
     Baked beans Spam Spam Spam Spam Spam]
```

## Símbolos como Chaves

Preferir símbolos em vez de strings como chaves de hash.

```ruby
# ruim
hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

# bom
hash = { one: 1, two: 2, three: 3 }
```

## Sintaxe de dois pontos em hash em vez de "foguete" (`=>`)

Preferir a sintaxe de hashcolon para definição de hashes quando cada chave é um símbolo. Use a sintaxe de hashrocket se pelo menos uma chave não for um símbolo.

```ruby
# ruim
hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

# ruim
hash = { twenty: 20, "twenty-one" => 21 }

# bom
hash = { one: 1, two: 2, three: 3 }

# também é bom, os símbolos não podem usar hífens
hash = { "twenty" => 20, "twenty-one" => 21 }
```

# Operadores e Fluxo de Controle

## Não use `and` ou `or`
`and` e `or` apesar de funcionar, evite usa-las. Elas não são um sinônimo dos operadores `&&` e `||`, então não devem ser usadas dessa maneira. Para expressões booleanas, use **sempre** `&&` e `||`.

```ruby
# ruim
# e/ou em condições (sua precedência é baixa, pode produzir resultado inesperado)
if got_needed_arguments and arguments_valid
  # ...body omitted
end

# no cálculo da expressão lógica
ok = got_needed_arguments and arguments_valid

# bom
# &&/|| em condicionais
if got_needed_arguments && arguments_valid
  # ...body omitted
end
# no cálculo da expressão lógica
ok = got_needed_arguments && arguments_valid

```

## Não deve haver espaço depois do `!`

Sem espaço após `!`.

```ruby
#ruim
# Verifica se o array não está vazio
if ! array.empty?
  puts "O array tem #{array.size} elementos"
end

# bom
# Verifica se o array não está vazio
if !array.empty?
  puts "O array tem #{array.size} elementos"
end

```

## Dupla Negação

Evite o uso de `!!`.

`!!` converte um valor para booleano, mas você não precisa dessa conversão explícita na condição de uma expressão de controle; usá-la só torna sua intenção mais complexa. Se você quer fazer uma verificação de `nil`, use `nil?` em vez disso.

```ruby
# ruim
x = 'test'
# cheque nulo obscuro
if !!x
  # body omitted
end

# bom
x = 'test'
if x
  # body omitted
end
```

## Operador ternário (`?:`) vs `if`

Prefira o operador ternário (`?:`) sobre as construções `if/then/else/end`. É mais comum e obviamente mais conciso.

`condição ? expressão_se_verdadeira : expressão_se_falsa`

Aqui está um exemplo de como usar o operador ternário para determinar se um número é par ou ímpar:

```ruby
# ruim
if num % 2 == 0
  "par"
else
  "ímpar"
end

# O mesmo exemplo usando operador ternário:

# bom
num % 2 == 0 ? "par" : "ímpar"

```

## `case` ao invés de `if-elsif`

Prefira o uso de `case` ao invés de `if-elsif` quando o valor comparado é o mesmo em cada cláusula.

```ruby
# ruim
if status == :active
  perform_action
elsif status == :inactive || status == :hibernating
  check_timeout
else
  final_action
end

# bom
case status
when :active
  perform_action
when :inactive, :hibernating
  check_timeout
else
  final_action
end
```
## Retornando Resultado do `if/case`

Aproveite o fato de que if e case são expressões que retornam um resultado.

```ruby
# ruim
if condition
  result = x
else
  result = y
end

# bom
result = if condition
           x
         else
           y
         end

# ruim
case x
when 1
  result = "x is equal to 1"
when 2
  result = "x is equal to 2"
when 3
  result = "x is equal to 3"
else
  result = "x is not 1, 2, or 3"
end

# bom
result = case x
         when 1
          "x is equal to 1"
         when 2
          "x is equal to 2"
         when 3
          "x is equal to 3"
         else
          "x is not 1, 2, or 3"
         end
```

## `unless` em vez de `if`

Preferir `unless` em vez de `if` para condições negativas (ou fluxo de controle `||`).

```ruby
# ruim
do_something if !some_condition

# ruim
do_something if not some_condition

# ruim
if !x.nil? && !x.empty?

# bom
do_something unless some_condition

# bom
unless x.nil? || x.empty?

# outra boa opçao
some_condition || do_something

```

## Não use o `unless` com o `else`

Não use o unless com o else. Reescreva esses casos com o caso positivo primeiro.

```ruby
# ruim
unless success?
  puts 'failure'
else
  puts 'success'
end

# bom
if success?
  puts 'success'
else
  puts 'failure'
end
```
## Loop Infinito

Use Kernel#loop ao invés de while/until quando você precisa de um loop infinito.

```ruby
# ruim
while true
  do_something
end

until false
  do_something
end

# bom
loop do
  do_something
end
```

## Evite `return`

Evite o `return` onde não for necessário para o fluxo de controle.

```ruby
# ruim
def some_method(some_arr)
  return some_arr.size
end

# bom
def some_method(some_arr)
  some_arr.size
end
```