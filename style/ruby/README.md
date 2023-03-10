Ruby
====

Este guia de estilo Ruby recomenda as melhores práticas para que os programadores Ruby do mundo real possam escrever código que possa ser mantido por outros programadores Ruby do mundo real.

- [Formatação e espaçamento](#formatação-e-espaçamento)
  - Formatação de arquivo
  - Espaços e Chaves
  - Chamadas de método
  - Linhas em branco
  - Literais de string

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

