# Documentação em Python

Este repositório apresenta um resumo do curso [Documenting Python Code: A Complete Guide](https://realpython.com/documenting-python-code/), com foco em práticas recomendadas para documentação em Python. Ele serve como uma referência rápida para tirar dúvidas e orientar a documentação de projetos futuros.

## Por que Documentar seu Código?

O código frequentemente é mais lido do que escrito, o que significa que, ao escrever código, você alcança dois públicos principais:
1. Seus usuários
2. Seus desenvolvedores

Isso torna a documentação bem-feita de extrema importância. Afinal, quem nunca codificou algo e, ao rever tempos depois, pensou: "Meu Deus, o que eu fiz aqui?". Independentemente de quão bom seja seu software, sem uma documentação adequada, ele dificilmente será utilizado ou compreendido.

## Comentar vs Documentar Código

**Comentar** é descrever seu código para desenvolvedores, ajudando outros (ou você mesmo no futuro) a entender o propósito de design de determinada parte do código.

**Documentar** o código, por outro lado, é descrever o uso e funcionalidade para seus usuários. Embora também seja útil no desenvolvimento, o público-alvo aqui são os usuários.

## Noções Básicas de Comentários de Código

Em Python, os comentários são criados com o símbolo `#`, e devem ser breves, idealmente com até 72 caracteres, conforme o PEP 8. Se um comentário ultrapassar esse limite, recomenda-se usar várias linhas.

```python
def hello_world():
    # Um simples comentário antes de um print
    print("Hello World!")
```

## Os principais objetivos ao comentar o código incluem:

Planejamento e revisão: Usar comentários para estruturar o código.
```
# Primeiro passo
# Segundo passo
# Terceiro passo
```
Descrição do código: Explicar a intenção de certas partes do código.
```
# Esta seção realiza x tarefa
```
Descrição Algorítmica: Explicar algoritmos complexos ou específicos.
```
# Explicação do algoritmo de Quick Sort
```
Marcação: Usar para destacar problemas ou melhorias futuras.
```
# TODO: Adicionar condição para...
```

## Quatro Regras Essenciais para Comentar (por Jeff Atwood)
* Mantenha os comentários próximos ao código que descrevem.
* Use uma formatação clara e direta.
* Evite informações redundantes.
* Estruture seu código para se autoexplicar o máximo possível.

## Documentando seu Código Python com Docstrings
Em Python, a documentação é centrada em docstrings – strings internas que, quando bem configuradas, facilitam a documentação e usabilidade do seu projeto.

Como tudo em Python é um objeto, ao examinar o diretório de um objeto (dir()), há uma propriedade interessante chamada __doc__, onde as docstrings são armazenadas.

### Convenções de Docstrings (PEP 257)
No mínimo, uma docstring deve oferecer um resumo rápido sobre o que descreve, contido em uma única linha:
```
"""Resumo rápido sobre o objeto."""
```

Docstrings multilinha são usadas para elaborações adicionais e devem seguir esta estrutura:
* Uma linha de resumo
* Uma linha em branco
* Qualquer explicação adicional
* Outra linha em branco antes do código continuar
```
"""Exemplo de docstring

Aqui há uma elaboração adicional. Observe a importância das linhas em branco.
"""
# O código continua aqui, após uma linha em branco
```
Principais Categorias de Docstrings
Class Docstrings: Para classes e métodos de classe.
Docstrings de Pacotes e Módulos: Para pacotes, módulos e funções.
Script Docstrings: Para scripts e funções específicas.
Comentar e documentar o código não só torna seu trabalho mais acessível para outros desenvolvedores e usuários, mas também ajuda você mesmo a lembrar e entender seu próprio código ao longo do tempo.

## Guia de Docstrings em Python

Docstrings são strings de documentação colocadas logo após definições de classes, métodos, pacotes, módulos e scripts para descrever sua funcionalidade. Elas devem ter o mesmo comprimento máximo de caracteres que os comentários, 72 caracteres por linha.

## Categorias Principais de Docstrings

1. **Docstrings de Classe**: Usadas para classes e métodos de classe.
2. **Docstrings de Pacotes e Módulos**: Usadas em pacotes, módulos e funções.
3. **Docstrings de Script**: Usadas em scripts e funções principais.

### Docstrings de Classe

Docstrings de classe são colocadas logo após a definição da classe ou de qualquer método de classe. Elas devem conter:

- Um resumo da finalidade e comportamento da classe.
- Métodos públicos e uma breve descrição.
- Atributos e propriedades da classe.
- Interfaces para subclasses, se aplicável.

Parâmetros do construtor (`__init__`) devem ser documentados dentro da docstring do método `__init__`, e cada método deve ter sua própria docstring com:

- Descrição breve do método.
- Argumentos, destacando quais são opcionais ou possuem valor padrão.
- Efeitos colaterais.
- Exceções levantadas.
- Restrições para o uso do método.

### Exemplo de Docstring de Classe

```python
class Animal:
    """
    Classe usada para representar um Animal.

    Atributos
    ----------
    says_str : str
        String formatada para mostrar o som que o animal faz.
    name : str
        Nome do animal.
    sound : str
        Som que o animal emite.
    num_legs : int
        Número de patas do animal (padrão é 4).

    Métodos
    -------
    says(sound=None)
        Imprime o nome do animal e o som que ele faz.
    """

    says_str = "A {name} says {sound}"

    def __init__(self, name, sound, num_legs=4):
        """
        Parâmetros
        ----------
        name : str
            Nome do animal.
        sound : str
            Som emitido pelo animal.
        num_legs : int, opcional
            Número de patas do animal (padrão é 4).
        """

        self.name = name
        self.sound = sound
        self.num_legs = num_legs

    def says(self, sound=None):
        """Imprime o nome do animal e o som que ele faz.

        Caso `sound` não seja informado, usa-se o som padrão do animal.

        Parâmetros
        ----------
        sound : str, opcional
            Som emitido pelo animal (padrão é None).

        Exceções
        ------
        NotImplementedError
            Se o som não for definido nem passado como parâmetro.
        """

        if self.sound is None and sound is None:
            raise NotImplementedError("Animais silenciosos não são suportados!")

        out_sound = self.sound if sound is None else sound
        print(self.says_str.format(name=self.name, sound=out_sound))
```

## Guia de Docstrings para Pacotes, Módulos e Scripts em Python

### Docstrings de Pacotes

As docstrings de pacotes devem ser inseridas no topo do arquivo `__init__.py` do pacote e devem listar os módulos e subpacotes exportados.

### Docstrings de Módulos

Docstrings de módulos são similares às de classe, mas documentam o módulo e suas funções. Elas devem ser colocadas no início do arquivo antes de qualquer importação e devem incluir:
- Breve descrição do módulo e sua finalidade.
- Lista de classes, exceções, funções e outros objetos exportados pelo módulo.

Docstrings de função dentro do módulo devem conter:
- Descrição da função e seu propósito.
- Argumentos obrigatórios e opcionais.
- Efeitos colaterais, exceções levantadas e restrições.

### Docstrings de Scripts

Docstrings de scripts devem ser colocadas no topo do arquivo e documentadas para que os usuários entendam como usá-lo. Elas devem incluir:
- Uma breve explicação do que o script faz e de como usá-lo.
- Dependências externas e bibliotecas personalizadas.
- Mensagem de uso e ajuda para parâmetros de entrada.

Se o script usa `argparse`, as docstrings dos parâmetros podem ser omitidas, desde que `argparse.ArgumentParser` seja documentado no `help`.

### Exemplo de Docstring de Script

```python
"""Impressora de Colunas de Planilha

Este script permite que o usuário imprima no console todas as colunas
da planilha. Supõe-se que a primeira linha da planilha contenha os
títulos das colunas.

Aceita arquivos .csv, .xls e .xlsx.

Este script requer `pandas` instalado no ambiente Python.

Este arquivo também pode ser importado como um módulo e contém as
seguintes funções:

    * get_spreadsheet_cols - retorna os títulos das colunas do arquivo
    * main - a função principal do script
"""

import argparse
import pandas as pd

def get_spreadsheet_cols(file_loc, print_cols=False):
    """Obtém e imprime as colunas de cabeçalho da planilha

    Parâmetros
    ----------
    file_loc : str
        Localização do arquivo da planilha
    print_cols : bool, opcional
        Flag para imprimir as colunas no console (padrão é False)

    Retorna
    -------
    list
        Lista de strings com os títulos das colunas
    """
    file_data = pd.read_excel(file_loc)
    col_headers = list(file_data.columns.values)

    if print_cols:
        print("\n".join(col_headers))

    return col_headers

def main():
    parser = argparse.ArgumentParser(description=__doc__)
    parser.add_argument(
        'input_file',
        type=str,
        help="Arquivo da planilha para imprimir as colunas"
    )
    args = parser.parse_args()
    get_spreadsheet_cols(args.input_file, print_cols=True)

if __name__ == "__main__":
    main()
```

## Formatos de Docstrings

Docstrings podem ser estruturadas com elementos comuns como `Arguments`, `Returns` e `Attributes`, dependendo do estilo escolhido. Esses formatos padronizados ajudam tanto os desenvolvedores quanto os analisadores de docstrings a entenderem rapidamente as funções. 

Abaixo, listamos os formatos mais populares:

| Tipo de Formatação          | Descrição                                                       | Apoiado por Sphinx | Especificação Formal |
|-----------------------------|-----------------------------------------------------------------|---------------------|-----------------------|
| **Documentação do Google**   | Forma de documentação recomendada pelo Google                  | Sim                 | Não                   |
| **reStructuredText**         | Padrão oficial do Python, robusto, mas menos intuitivo         | Sim                 | Sim                   |
| **NumPy/SciPy**              | Combinação de `reStructuredText` e estilo Google               | Sim                 | Sim                   |
| **Epytext**                  | Adaptação Python do Epydoc, muito popular entre desenvolvedores Java | Não oficialmente   | Sim                   |

Escolher um formato e mantê-lo consistente no projeto é essencial para uma boa documentação. A seguir, temos exemplos de cada tipo.

### Exemplo de Docstrings no Formato Google

```python
"""Obtém e imprime as colunas de cabeçalho da planilha

Args:
    file_loc (str): A localização do arquivo da planilha
    print_cols (bool): Flag para imprimir as colunas no console
        (padrão é False)

Returns:
    list: lista de strings representando as colunas de cabeçalho
"""
```

### Exemplo de Docstrings no Formato reStructuredText
```
"""Obtém e imprime as colunas de cabeçalho da planilha

:param file_loc: A localização do arquivo da planilha
:type file_loc: str
:param print_cols: Flag para imprimir as colunas no console
    (padrão é False)
:type print_cols: bool
:returns: lista de strings representando as colunas de cabeçalho
:rtype: list
"""
```

### Exemplo de Docstrings no Formato NumPy/SciPy
```
"""Obtém e imprime as colunas de cabeçalho da planilha

Parameters
----------
file_loc : str
    Localização do arquivo da planilha
print_cols : bool, optional
    Flag para imprimir as colunas no console (padrão é False)

Returns
-------
list
    lista de strings representando as colunas de cabeçalho
"""
```

### Exemplo de Docstrings no Formato Epytext
```
"""Obtém e imprime as colunas de cabeçalho da planilha

@type file_loc: str
@param file_loc: A localização do arquivo da planilha
@type print_cols: bool
@param print_cols: Flag para imprimir as colunas no console
    (padrão é False)
@rtype: list
@returns: lista de strings representando as colunas de cabeçalho
"""
```

# Documentação de Projetos Python

Projetos Python podem variar em tamanho e propósito. A documentação deve ser adaptada às necessidades do usuário e ao tipo de projeto. Abaixo, apresentamos um layout recomendado para organizar o projeto e sua documentação:

```plaintext
project_root/
│
├── project/              # Código fonte do projeto
├── docs/                 # Documentação adicional
├── README                # Resumo do projeto
├── HOW_TO_CONTRIBUTE     # Orientação para novos contribuidores
├── CODE_OF_CONDUCT       # Código de conduta do projeto
├── examples.py           # Exemplos de uso do projeto
```

## Tipos de Projetos
Os projetos podem ser divididos em três categorias principais: Privado, Compartilhado e Público/Código Aberto. Cada tipo tem necessidades específicas de documentação.

### Projetos Privados
Projetos privados são destinados ao uso pessoal e geralmente não são compartilhados. Nesse caso, a documentação pode ser mínima.

README: Um breve resumo do projeto e seu propósito, com requisitos de instalação e operação.
examples.py: Um exemplo simples de como usar o projeto.
Mesmo sendo privados, documente o suficiente para facilitar a compreensão de seu próprio código no futuro.

### Projetos Compartilhados
Projetos compartilhados envolvem uma colaboração limitada entre algumas pessoas. A documentação ajuda na integração de novos membros e na comunicação de alterações importantes.

README: Um resumo do projeto com requisitos e mudanças relevantes.
* examples.py: Exemplos de uso do projeto.
* HOW_TO_CONTRIBUTE: Instruções para novos colaboradores se familiarizarem com o projeto.
* Projetos Públicos e de Código Aberto
* Projetos públicos e de código aberto são destinados a um público mais amplo. Aqui, a documentação é essencial para garantir que o projeto seja utilizável por todos.

README: Inclua um resumo, requisitos, links adicionais e relatórios de bugs. Consulte o tutorial de Dan Bader para boas práticas.
* HOW_TO_CONTRIBUTE: Explique como os novos contribuidores podem ajudar.
* CODE_OF_CONDUCT: Defina como colaboradores devem interagir entre si.
* Licença: Um arquivo descrevendo a licença do projeto.
* docs/: Pasta com documentação adicional detalhada.

### Estrutura da Pasta docs
Para organizar a pasta docs, siga as diretrizes de Daniele Procida apresentadas na PyCon 2017. A documentação deve incluir quatro seções principais:

* Tutoriais: Passo a passo para levar o leitor a concluir um projeto ou exercício significativo, focado no aprendizado.
* Guias de Instruções: Receitas práticas para resolver problemas comuns.
* Referências: Informações detalhadas e técnicas sobre tópicos específicos, úteis para compreensão.
* Explicações: Documentação técnica sobre classes, funções, APIs e outros detalhes internos.

A tabela abaixo mostra como as diferentes seções da documentação se relacionam entre si e qual é a finalidade de cada uma:

| Mais útil quando estamos estudando | Mais útil quando estamos codificando |
|------------------------------------|--------------------------------------|
| **Passo prático**                  | **Tutoriais**                       | **Guias de Instruções**              |
| **Conhecimento Teórico**           | **Explicação**                      | **Referência**                       |

Ao organizar seu projeto dessa forma, você garante que os usuários tenham acesso rápido e fácil às respostas para suas dúvidas. Dessa maneira, eles poderão navegar pelo conteúdo com clareza, encontrando rapidamente as informações de que precisam.

