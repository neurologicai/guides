Ruby
====

Este guia de estilo Ruby recomenda as melhores práticas para que os programadores Ruby do mundo real possam escrever código que possa ser mantido por outros programadores Ruby do mundo real.

- [Formatação e espaçamento](#formatação-e-espaçamento)
  - Formatação de arquivo
  - Espaços e Chaves
  - Chamadas de método
  - Linhas em branco

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
  - Não deve haver espaço depois do `!` (bang) _ponto de exclamação_
  - Dupla Negação
  - Operador ternário (`?:`) vs `if`
  - `case` ao invés de `if-elsif`
  - Retornando Resultado do `if/case`
  - `unless` em vez de `if`
  - Não use o `unless` com o `else`
  - Loop Infinito
  - Evite o `return`

- [Strings](#strings)
  - Concatenação de strings 
  - Interpolação de strings
  - Quotes

- [Condicionais](#condicionais)
  - Não use Modificadores `if` em várias linhas
  - Indentar Atribuição Condicional
  - Indentar quando usar `case`
  - Não use `then` em `if`/`case`
  - `if` como modificador

- [Comentários](#comentários)
  - Não use comentários
  - E se for necessario?
  - Escreva comentários em inglês
  - Evite comentários supérfluos
  - Formato de Palavra-Chave para Comentários

- [Blocks](#blocks)
  - Delimitadores de Blocos de Linha Única
  - Abreviação de Aplicação de Proc '`&:`'

- [Metodos](#metodos)
  - Método Perigoso com Sinal de Exclamação (bang)
  - Defina o seguro usando o inseguro
  - Métodos de uma linha
  - Não use parênteses

- [Classes e Modulos](#classes-e-modulos)
  - Consistência de Classes
  - Definição de Namespace
  - Indentação de `public`/`private`/`protected`
  - Evite o uso de variáveis de classe (`@@`)
  - Métodos de Classe `def self`
  - Classes em uma única linha
  - Arquivos de Classes


- [Outros](#outros)
  - Evite o uso do `self` onde não for necessário

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

# Strings

## Concatenação de strings

Evite usar `String#+` quando precisar construir grandes blocos de dados. Em vez disso, use `String#<<`. A concatenação modifica a instância de string no local e é sempre mais rápida que `String#+`, que cria vários novos objetos de string.

```ruby
# ruim
html = ''
html += '<h1>Page title</h1>'

paragraphs.each do |paragraph|
  html += "<p>#{paragraph}</p>"
end

# bom e mais performatico
html = ''
html << '<h1>Page title</h1>'

paragraphs.each do |paragraph|
  html << "<p>#{paragraph}</p>"
end
```

## Interpolação de strings

Prefira a interpolação e a formatação de strings à concatenação de strings:

```ruby
# ruim
email_with_name = user.name + ' <' + user.email + '>'

# bom
email_with_name = "#{user.name} <#{user.email}>"

# bom
email_with_name = format('%s <%s>', user.name, user.email)
```

## Quotes

Prefira strings com aspas simples quando não precisar de interpolação de strings ou símbolos especiais como `\t`, `\n`, `'`, etc.

```ruby
# ruim
name = "Bozhidar"

name = 'De\'Andre'

my_string = "This is \"My String\"!!!"

# bom
name = 'Bozhidar'

name = "De'Andre"

my_string = 'This is "My String"!!!'

```

# Condicionais

## Não use Modificadores `if` em várias linhas

Evite o uso de modificadores `if`/`unless` no final de um bloco de várias linhas não trivial.

```ruby
# ruim
10.times do
  # multi-line body omitted
end if some_condition

# bom
if some_condition
  10.times do
    # multi-line body omitted
  end
end
```

## Indentar Atribuição Condicional

Quando atribuir o resultado de uma expressão condicional a uma variável, preservar o alinhamento usual de seus ramos.

```ruby
# ruim - bastante complicado
kind = case year
when 1850..1889 then 'Blues'
when 1890..1909 then 'Ragtime'
when 1910..1929 then 'New Orleans Jazz'
when 1930..1939 then 'Swing'
when 1940..1950 then 'Bebop'
else 'Jazz'
end

result = if some_cond
  calc_something
else
  calc_something_else
end

# ruim
kind = case year
       when 1850..1889 then 'Blues'
       when 1890..1909 then 'Ragtime'
       when 1910..1929 then 'New Orleans Jazz'
       when 1930..1939 then 'Swing'
       when 1940..1950 then 'Bebop'
       else 'Jazz'
       end

result = if some_cond
           calc_something
         else
           calc_something_else
         end

# bom (e um pouco mais eficiente em termos de largura)
kind =
  case year
  when 1850..1889 then 'Blues'
  when 1890..1909 then 'Ragtime'
  when 1910..1929 then 'New Orleans Jazz'
  when 1930..1939 then 'Swing'
  when 1940..1950 then 'Bebop'
  else 'Jazz'
  end

result =
  if some_cond
    calc_something
  else
    calc_something_else
  end
```

## Indentar quando usar `case`

A recomendação refere-se à prática de programação que sugere que o conteúdo de cada `when` de uma estrutura `case` seja indentado. Essa prática torna o código mais legível e ajuda a visualizar a estrutura do `case`.

```ruby
# ruim
case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration > 120
    puts 'Too long!'
  when Time.now.hour > 21
    puts "It's too late"
  else
    song.play
end

# bom
case
when song.name == 'Misty'
  puts 'Not again!'
when song.duration > 120
  puts 'Too long!'
when Time.now.hour > 21
  puts "It's too late"
else
  song.play
end
```

## Não use `then` em `if`/`case`

Não use `then` para instruções de várias linhas em declarações `if`/`unless`.

```ruby
# ruim
if some_condition then
  # body omitted
end

# ruim
case foo
when bar then
  # body omitted
end

# bom
if some_condition
  # body omitted
end

# bom
case foo
when bar
  # body omitted
end

```

## `if` como modificador

Prefira o uso do modificador `if`/`unless` quando você tem um corpo de uma única linha. Outra boa alternativa é o uso dos operadores lógicos `&&`/`||` no fluxo de controle.

```ruby
# ruim
if some_condition
  do_something
end

# bom
do_something if some_condition

# outra boa opção
some_condition && do_something
```

# Comentários
## Não use comentários

Um bom código é a sua própria melhor documentação. Ao se preparar para adicionar um comentário, pergunte a si mesmo: "Como posso melhorar o código para que este comentário não seja necessário?". Melhore o código e, em seguida, documente-o para torná-lo ainda mais claro.

Essa prática sugere que, em vez de confiar em comentários para explicar o código, o código em si deve ser escrito de forma clara e fácil de entender. Ao se deparar com um trecho de código que requer um comentário para ser compreendido, o desenvolvedor deve se perguntar se há uma maneira melhor de escrever o código para que ele seja autoexplicativo. Em seguida, deve-se aprimorar o código e, se necessário, adicionar um comentário para tornar sua funcionalidade ainda mais clara. A ideia é que, ao escrever um código claro e fácil de entender, seja necessário menos comentários e, por consequência, o código se torne mais fácil de manter e modificar.

## E se for necessario?

As anotações geralmente devem ser escritas na linha imediatamente acima do código relevante.

Mantenha os comentários existentes atualizados. Um comentário desatualizado é pior do que nenhum comentário.

```ruby
# ruim
def bar
  baz(:quux) # FIXME: This has crashed occasionally since v3.2.1.
end

# bom
def bar
  # FIXME: This has crashed occasionally since v3.2.1.
  baz(:quux)
end
```

## Escreva comentários em inglês
```ruby
# ruim
# TODO: Desenvolver forma de servir templates de script sem depender de uma conta na base.

# bom
# TODO: Develop a way to serve script templates without relying on an account in the database.
```

## Evite comentários supérfluos

```ruby
# ruim
counter += 1 # Increments counter by one.

# Lead Deletion Scopes
scope :clicked, -> { where(clicked: false) }

# Constants
MAX_INTEGER = 2147483647

# Validations
validates :name, presence: true

# Write Attributes
def code=(val)

# Methods
def full_name

# Callbacks
before_create :set_main_company
```

## Formato de Palavra-Chave para Comentários

A palavra-chave de anotação é seguida por dois pontos e um espaço, depois uma nota descrevendo o problema.

```ruby
# ruim
def bar
  # FIXME This has crashed occasionally since v3.2.1.
  baz(:quux)
end

# bom
def bar
  # FIXME: This has crashed occasionally since v3.2.1.
  baz(:quux)
end
```

Se forem necessárias várias linhas para descrever o problema, as linhas subsequentes devem ser recuadas três espaços após o # (um geral mais dois para fins de recuo).

```ruby
def bar
  # FIXME: This has crashed occasionally since v3.2.1. It may
  #   be related to the BarBazUtil upgrade.
  baz(:quux)
end
```

as palavras-chaves são: `TODO`, `FIXME`, `OPTIMIZE`, `HACK`, `REVIEW`

## TODO
Use `TODO` para observar recursos ou funcionalidades ausentes que devem ser adicionados em uma data posterior.

## FIXME
Use `FIXME` para observar código quebrado que precisa ser corrigido.

## OPTIMIZE
Use `OPTIMIZE` para observar código lento ou ineficiente que pode causar problemas de desempenho.

## HACK
Use `HACK` para observar "code smells" onde práticas de codificação questionáveis foram utilizadas e devem ser refatoradas.

## REVIEW
Use `REVIEW` para observar qualquer coisa que deve ser verificada para confirmar se está funcionando conforme o pretendido. Por exemplo: 
```ruby
# REVIEW: Are we sure this is how the client does X currently?
```

***Use outras palavras-chave personalizadas de anotação se parecer apropriado, mas certifique-se de documentá-las no README ou em um documento semelhante do projeto.***

# Blocks

## Delimitadores de Blocos de Linha Única
```ruby
names = %w[Bozhidar Filipp Sarah]

# ruim
names.each do |name|
  puts name
end

# bom
names.each { |name| puts name }

# ruim
names.select do |name|
  name.start_with?('S')
end.map { |name| name.upcase }

# bom
names.select { |name| name.start_with?('S') }.map(&:upcase)
```

## Abreviação de Aplicação de Proc '`&:`'

Use a abreviação de chamada `Proc` quando o método chamado é a única operação de um bloco.

```ruby
# ruim
bluths.map { |bluth| bluth.occupation }
bluths.select { |bluth| bluth.blue_self? }

# bom
bluths.map(&:occupation)
bluths.select(&:blue_self?)
```

# Metodos

## Método Perigoso com Sinal de Exclamação (bang)

Os nomes de métodos potencialmente perigosos (ou seja, métodos que modificam o objeto ou seus argumentos, `exit!` (que não executa os finalizadores como o `exit` faz), etc) devem terminar com um ponto de exclamação se existir uma versão segura desse método perigoso.

```ruby
# ruim - Não há nenhum método 'seguro' correspondente.
class Person
  def update!
  end
end

# bom
class Person
  def update
  end
end

# bom
class Person
  def update!
  end

  def update
  end
end
```

## Defina o seguro usando o inseguro

Defina o método não-bang (seguro) em termos do método bang (perigoso) sempre que possível.

```ruby
# bad
class MyService
  def call!(id)
    MyModel.find(id)
  end

  def call(id)
    MyModel.find_by(id: id)
  end
end

# good
class MyService
  def call!(id)
    MyModel.find(id)
  end

  def call(id)
    call!(id)
  rescue ActiveRecord::RecordNotFound
    nil
  end
end
```

## Métodos de uma linha

Evite métodos de linha única que tenham um corpo.

```ruby
# ruim
def some_method; something; end

# bom
def some_method
  something
end
```

Evite definir métodos em várias linhas se eles não tiverem um corpo real.

```ruby
# ruim
def index
end

# bom
def index; end
```

## Não use parênteses

Use `def` com parênteses quando houver parâmetros. Omita os parênteses quando o método não aceitar nenhum parâmetro.

```ruby
# ruim
def some_method()
  # body omitted
end

# bom
def some_method
  # body omitted
end

# ruim
def some_method_with_parameters param1, param2
  # body omitted
end

# bom
def some_method_with_parameters(param1, param2)
  # body omitted
end
```

# Classes e Modulos
## Consistência nas classes

Use uma estrutura consistente em suas definições de classe.

```ruby
class Person
  # Estenda (extend) e inclua (include) vêm primeiro
  extend SomeModule
  include AnotherModule

  # Classes internas (StandardError)
  CustomError = Class.new(StandardError)

  # Constantes são as próximas
  SOME_CONSTANT = 20

  # Em seguida, temos atributos (se houver)
  attr_reader :name

  # Seguidos por validaçõe (se houver)
  validates :name

  # Métodos de classe públicos vêm em seguida
  def self.some_method
  end

  # Inicialização (initialize) vem entre métodos de classe e outros métodos de instância
  def initialize
  end

  # Seguido por outros métodos de instância públicos
  def some_method
  end

  # Métodos protegidos (protected) e privados (private) são agrupados no final.
  protected

  def some_protected_method
  end

  private

  def some_private_method
  end
end
```

## Definição de Namespace

Defina (e reabra) classes e módulos com namespace usando a aninhamento explícito.

```ruby
# ruim
class Utilities::Store
  # ...
end

# bom
module Utilities
  class WaitingList
    # ...
  end
end
```

## Indentação de `public`/`private`/`protected`

 Identar os métodos públicos, protegidos e privados tanto quanto as definições de métodos que se aplicam. Deixe uma linha em branco acima do modificador de visibilidade e uma linha em branco abaixo para enfatizar que se aplica a todos os métodos abaixo dele.

```ruby
# bom
class SomeClass
  def public_method
    # some code
  end

  def public_method_two
    # some code
  end

  private

  def private_method
    # some code
  end

  def another_private_method
    # some code
  end
end
```

## Evite o uso de variáveis de classe (`@@`)

Evite o uso de variáveis de classe (`@@`) devido ao seu comportamento "ruim" em relação à herança.

```ruby
class Parent
  @@class_var = 'parent'

  def self.print_class_var
    puts @@class_var
  end
end

class Child < Parent
  @@class_var = 'child'
end

Parent.print_class_var # => will print "child"
```

## Métodos de Classe `def self`

Use self.method para definir métodos de classe. Isso torna o código mais fácil de ser refatorado, já que o nome da classe não é repetido.

```ruby
class TestClass
  # ruim
  def TestClass.some_method
    # body omitted
  end

  # bom
  def self.some_other_method
    # body omitted
  end
end
```

## Classes em uma única linha

Prefira um formato de linha única, para definições de classe sem corpo. É mais fácil de ler, entender e modificar.

```ruby
# bom
class FooError < StandardError; end
```

## Arquivos de Classes

Não aninhe classes de várias linhas dentro de outras classes. Tente ter essas classes aninhadas cada uma em seu próprio arquivo em uma pasta nomeada como a classe contenedora.

```ruby
# ruim

# foo.rb
class Foo
  class Bar
    # 30 methods inside
  end

  class Car
    # 20 methods inside
  end

  # 30 methods inside
end

# bom

# foo.rb
class Foo
  # 30 methods inside
end

# foo/bar.rb
class Foo
  class Bar
    # 30 methods inside
  end
end

# foo/car.rb
class Foo
  class Car
    # 20 methods inside
  end
end
```

# Outros
## Evite o uso do `self` onde não for necessário

Evite o uso do `self` onde não for necessário. (Ele é necessário apenas ao chamar um acessador de gravação `self`, métodos com nome de palavras reservadas ou operadores sobrecarregáveis.)

```ruby
# ruim
def ready?
  if self.last_reviewed_at > self.last_updated_at
    self.worker.update(self.content, self.options)
    self.status = :in_progress
  end
  self.status == :verified
end

# bom
def ready?
  if last_reviewed_at > last_updated_at
    worker.update(content, options)
    self.status = :in_progress
  end
  status == :verified
end
```