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

## Com vírgula à direita do Array

Por vírgula após o último item de um Array ou Hash literal, especialmente quando os itens estiverem em linhas separadas.

Quando forem de uma unica linha, não usar a virgula.

```ruby
# ruim
VALUES = [1001, 2020, 3333, ]

# bom - é mais fácil de mover/adicionar/remover itens
VALUES = [
           1001,
           2020,
           3333,
         ]
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
hash = { twenty: 20, twenty_one: 21 }
```
