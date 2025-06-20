# Gramática

funcao → **'funzione'** NOME '(' (declaracaoFuncao)? ')' bloco? **'fermare'**

declaracaoFuncao → tipo ID | tipo ID ',' declaracaoFuncao

bloco → linha bloco | linha

linha → escrever | ler | declaracao ';' | ifelse | while | for | atribuicao ';' | chamadaFunc

chamadaFunc → NOME '(' argumentos? ')' ';'

argumentos → exprChamadaFunc (',' exprChamadaFunc)\*

exprChamadaFunc → ID | NUM | TEXTO | chamadaFunc

escrever → **'carattere'** '<<' (TEXTO | '$' ID) ('.' ('$' ID | TEXTO))\* ';'

ler → **'leggere'** 'xD' TEXTO ID? ';'ler → **'leggere'** 'xD' TEXTO ID? ';'

declaracao → tipo ID operadorAtribuicao expressao

ifelse → **'se'** condicao '{' bloco '}' (**'altrimenti'** '{' bloco '}')?

while → **'mentre'** condicao bloco | **'fare'** '{' bloco '}' **'mentre'** condicao ';'

for → **'per'** '(' declaracao ';' condicao ';' atribuicao ';' ')' bloco

atribuicao → ID opAtribuicao expressao

expressao → fator (opMat fator)?

fator → ID | NUM | TEXTO | '(' expressao ')' | NUMDECIMAL

condicao → fator opRelacional fator ((**'o'** | **'e'**) condicao)\* | '(' condicao ')'

tipo → **'intero'** | **'galleggiante'** | **'stringa'** | **'booleano'**

opRelacional → '>' | '<' | '==' | '!=' | '>=' | '<='

opAtribuicao → '=' | '+=' | '-=' | '\*=' | '/=' | '%='

opMat → '+' | '-' | '\*' | '/' | '%'

ID → '\_' (a-z | A-Z)+

NOME → (a-z | A-Z)+

NUM → (0-9)+

NUMDECIMAL → (0-9)+ '.' (0-9)+

TEXTO → '"' (0-9 | a-z | A-Z | ' ' )+ '"'

---

# Como Compilar e Rodar o Compilador

## Requisitos

- Java 11 ou superior
- Maven (opcional, mas recomendado para build)

## Compilar o Projeto

No terminal, execute:

```
mvn clean package
```

O projeto será compilado e os arquivos .class ficarão em `target/classes`.

## Rodar o Compilador (Offline)

Para rodar o compilador localmente (linha de comando), execute:

```
java -cp target/classes compiler.main.Main
```

Você pode adaptar o Main.java para aceitar argumentos de entrada/saída conforme desejar.

## Rodar o Servidor HTTP (Java Puro)

O projeto possui um servidor HTTP simples, sem Spring Boot, implementado em `compiler.server.CompilerServer`.

Para rodar o servidor:

```
java -cp target/classes compiler.server.CompilerServer
```

O servidor será iniciado na porta 8080. Você pode enviar requisições POST para `http://localhost:8080/compile` com o código a ser compilado no corpo da requisição (texto puro).

### Exemplo de requisição com curl:

```
curl -X POST --data-binary @src/main/resources/codigo.txt http://localhost:8080/compile
```

---

# Estrutura do Projeto

- src/main/java: código-fonte principal
- src/main/resources: arquivos de recursos (ex: codigo.txt)
- target/: arquivos gerados na compilação (ignorado no git)
- pom.xml: configuração do Maven
- README.md: este arquivo

---

# Observações

- O projeto NÃO depende de Spring Boot para rodar o servidor.
- O .gitignore está configurado para manter apenas o mínimo essencial: src/, pom.xml e README.md.
- Para dúvidas ou sugestões, abra uma issue ou entre em contato.
