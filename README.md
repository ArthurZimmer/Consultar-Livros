# Consultar-Livros
Um programa simples em C que utiliza a manipulação de arquivos. Faz a gravação, consulta, e exclusão de dados como nome do livro, autor, preço e código. Utiliza como banco de dados um simples documento .txt, sua interação também é pelo console.

    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    typedef struct Registro {
        char nome[50];
        char autor[50];
        char valor[50];
        char codigo[50];
    } Registro;
    
    Registro GetRegistro() {
        Registro registro;
        printf("\ndigite o nome do livro: ");
        fgets(registro.nome, 50, stdin);
            
    printf("digite o autor do livro: ");
    fgets(registro.autor, 50, stdin);
    
    printf("digite o valor do livro: ");
    fgets(registro.valor, 50, stdin);
    
    printf("digite o codigo do livro: ");
    fgets(registro.codigo, 50, stdin);
    
    return registro;
    }
    
    void ConsultarPorAutor(char autor[]) {
        FILE *livros;
        Registro registro;
        int encontrou = 0;

    if ((livros = fopen("c:\\biblioteca\\registro-livros.txt", "r")) == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return;
    }

    while (fscanf(livros, "%s%s%s%s", registro.nome, registro.autor, registro.valor, registro.codigo) != EOF) {
        if (strcmp(registro.autor, autor) == 0) {
            printf("\n\tCodigo: %s\n", registro.codigo);
            printf("\tTitulo: %s\n", registro.nome);
            printf("\tAutor: %s\n", registro.autor);
            printf("\tValor: R$ %s\n", registro.valor);
            encontrou = 1;
        }
    }

    if (!encontrou) {
        printf("Nenhum livro encontrado com o autor '%s'.\n", autor);
    }

    fclose(livros);
    }
    
    void ConsultarPorNome(char nome[]) {
        FILE *livros;
        Registro registro;
        int encontrou = 0;

    if ((livros = fopen("c:\\biblioteca\\registro-livros.txt", "r")) == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return;
    }

    while (fscanf(livros, "%s%s%s%s", registro.nome, registro.autor, registro.valor, registro.codigo) != EOF) {
        if (strcmp(registro.nome, nome) == 0) {
            printf("\n\tCodigo: %s\n", registro.codigo);
            printf("\tTitulo: %s\n", registro.nome);
            printf("\tAutor: %s\n", registro.autor);
            printf("\tValor: R$ %s\n", registro.valor);
            encontrou = 1;
        }
    }

    if (!encontrou) {
        printf("Nenhum livro encontrado com o nome '%s'.\n", nome);
    }

    fclose(livros);
    }
    
    void ConsultarPorValor(char valor[]) {
        FILE *livros;
        Registro registro;
        int encontrou = 0;

    if ((livros = fopen("c:\\biblioteca\\registro-livros.txt", "r")) == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return;
    }

    while (fscanf(livros, "%s%s%s%s", registro.nome, registro.autor, registro.valor, registro.codigo) != EOF) {
        if (strcmp(registro.valor, valor) == 0) {
            printf("\n\tCodigo: %s\n", registro.codigo);
            printf("\tTitulo: %s\n", registro.nome);
            printf("\tAutor: %s\n", registro.autor);
            printf("\tValor: R$ %s\n", registro.valor);
            encontrou = 1;
        }
    }

    if (!encontrou) {
        printf("Nenhum livro encontrado com o valor '%s'.\n", valor);
    }

    fclose(livros);
    }
    
    int main() {
        int opcao;
        char autor[50], nome[50], valor[50];
        char resposta;
        
    printf("\n1 - Inserir registro\n2 - Consultar por autor\n3 - Consultar por nome do livro\n4 - Consultar por valor\n5 - Excluir todos\n6 - Sair\n\nDigite a opcao que deseja prosseguir: ");
    scanf("%d", &opcao);
    getchar();

    if (opcao == 1) {
        Registro registro;
        FILE *livros;

        if ((livros = fopen("c:\\biblioteca\\registro-livros.txt", "a")) == NULL) {
            printf("Erro ao abrir o arquivo.\n");
            exit(1);
        }

        do {
            registro = GetRegistro();
            fprintf(livros, "%s%s%s%s", registro.nome, registro.autor, registro.valor, registro.codigo);
            printf("Mais um livro (s/n)? ");
            char resposta = getchar();
            getchar(); 
        } while (resposta != 'n' && resposta != 'N');

        fclose(livros);
    } 
    
    else if (opcao == 2) {
        printf("Digite o autor que deseja consultar: ");
        fgets(autor, 50, stdin);
        autor[strcspn(autor, "\n")] = '\0'; 
        
        ConsultarPorAutor(autor);
    }
    
    else if (opcao == 3) {
        printf("Digite o nome do livro que deseja consultar: ");
        fgets(nome, 50, stdin);
        nome[strcspn(nome, "\n")] = '\0';
        
        ConsultarPorNome(nome);
    }

    else if (opcao == 4) {
        printf("Digite o valor que deseja consultar: ");
        fgets(valor, 50, stdin);
        valor[strcspn(valor, "\n")] = '\0'; 
        
        ConsultarPorValor(valor);
    }
    
    else if (opcao == 5) {
        if (remove("c:\\biblioteca\\registro-livros.txt") == 0) {
            printf("\nRegistros excluidos com sucesso.\n\n");
        } else {
            printf("\nErro ao excluir o arquivo.\n\n");
        }
    }
    
    else {
        exit(0);
    }

    return 0;
    }
