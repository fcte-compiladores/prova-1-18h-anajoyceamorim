De modo abstrato, o compilador é um programa que converte código de uma
linguagem para outra. Como se fosse uma função do tipo `compilador(str) -> str`.
No caso de compiladores que emitem código de máquina ou bytecode, seria mais
preciso dizer `compilador(str) -> bytes`, mas a idéia básica é a mesma.

De forma geral o processo é dividido em etapas como abaixo

```python
def compilador(x1: str) -> str | bytes:
    x2 = lex(x1)        # análise léxica
    x3 = parse(x2)      # análise sintática
    x4 = analysis(x3)   # análise semântica
    x5 = optimize(x4)   # otimização
    x6 = codegen(x5)    # geração de código
    return x6
```

Defina brevemente o que cada uma dessas etapas realizam e marque quais seriam os
tipos de entrada e saída de cada uma dessas funções. Explique de forma clara o
que eles representam. Você pode usar exemplos de linguagens e/ou compiladores
conhecidos para ilustrar sua resposta. Salve sua resposta nesse arquivo.

# lex(?) -> ?
A função `lex` realiza a **análise léxica**: transforma o código fonte em uma lista de tokens.  
Cada token representa uma unidade léxica da linguagem (como palavras-chave, identificadores, números, etc).

Exemplo:  
Entrada: `"var x = 42;"`  
Saída: `[Token("VAR", "var"), Token("ID", "x"), Token("EQUAL", "="), Token("NUMBER", "42"), Token("SEMICOLON", ";")]`  
Esse processo remove espaços, detecta erros lexicais e organiza o texto bruto em blocos com significado.
 
# parse(?) -> ?
A função `parse` realiza a **análise sintática**: transforma a lista de tokens em uma **árvore sintática abstrata (AST)**.  
A AST representa a estrutura do programa segundo as regras da gramática.

Exemplo:  
Entrada: `[Token("NUMBER", "1"), Token("PLUS", "+"), Token("NUMBER", "2")]`  
Saída: `BinOp(Literal(1), Literal(2), op=add)`  
Essa etapa detecta erros de estrutura (como parênteses malformados) e organiza o código de forma hierárquica.

# analysis(?) -> ?
A função `analysis` realiza a **análise semântica**: verifica se o programa tem sentido logicamente.  
Exemplos de verificações:  
- Se variáveis foram declaradas antes de usar;  
- Se os tipos são compatíveis nas operações (ex: não somar string com número);  
- Se funções são chamadas com o número correto de argumentos.  

Essa etapa pode enriquecer a AST com informações de escopo e tipo.

# optimize(?) -> ?
A função `optimize` transforma a AST em uma versão mais eficiente sem alterar seu comportamento.  
Exemplos de otimizações:  
- Eliminar código morto (instruções que nunca são executadas);  
- Substituir `x + 0` por `x`;  
- Transformações para usar menos memória ou instruções mais rápidas.  

Essa etapa é importante para melhorar o desempenho do programa gerado.

# codegen(?) -> ?
A função `codegen` realiza a **geração de código**, convertendo a AST em código final.  
Esse código pode ser:  
- **Assembly ou código de máquina** (GCC, Clang);  
- **Bytecode** para VMs (Python, Java);  
- **Código-fonte** em outra linguagem (TypeScript → JavaScript).  

É a etapa final do compilador — a que produz a saída executável ou interpretável.