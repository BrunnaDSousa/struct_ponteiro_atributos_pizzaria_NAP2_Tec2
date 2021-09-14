# struct_ponteiro_atributos_pizzaria_NAP2_Tec2
atributos, itens, struct  ordenacao,ponteiros  adastrar 5 atributos para os 20 itens  realizar uma pesquisa solicitada pelo usuário por um dos atributos você define o atributo a ser usado para a pesquisa e retornar para o usuário em tela os 5 atributos relacionados ao registro da pesquisa 


/*
Universidade Federeal Rural da Amazonia
Docente: Aleksandra Silva
Discente: Brunna Danielle Santos de Sousa 
Tecnicas de programacao II - Tarefa - segunda possibilidade - NAP2 – Tarefa 2
*/

/*
    a) As mesmas funcionalidades anteriores: 
1) cadastrar 5 atributos para os 20 itens 
2) realizar uma pesquisa solicitada pelo usuário por um dos atributos (você define o atributo a ser usado para a pesquisa) e retornar para o usuário em tela os 5 atributos relacionados ao registro da pesquisa 
3) utilizar um dos algoritmos de ordenação visto na disciplina para realizar a ordenação de um dos atributos e exibir estes atributos ordenados na tela como saída para o usuário
  
Os mesmos requisitos anteriores serão observados: 
1)	O programa deve conter uma struct para definição dos 5 atributos
2)	Os 5 atributos devem contemplar os diferentes tipos suportados pela linguagem C que são: inteiro, float, caractere/string. 
3)	Comentários que tornem possível ler e compreender as principais ações realizadas no programa 
4)	No mínimo uma função para realizar qualquer uma das funcionalidades do programa 

Adicionalmente, o programa deve: 
a.	Possuir ponteiros em dois locais diferentes do programa; 
b.	Comentários nas linhas do programa que possuem os ponteiros e uma breve descrição de sua utilidade (no máximo 2 linhas de comentários)  


*/


//PIZZARIA 

#include <stdio.h>
#include <stdlib.h>

struct tp_endereco{ //dados de entrega/endereco
    
    int numero;
    char rua [40];
    char bairro[40];
    char cidade[40];
    char estado[3];
    int cep;
    char referencia[40];
};

struct tp_dados_pizza{
    int localPedido; // se foi por wpp, ligação etc
    char tamanhoPizza [40]; 
    int forno; //saber se e a lenha ou industrial
    char sabor[40];
    char borda[40]; //com ou sem borda
    char bebida [40];
    char acompanhamento[40];
    int brinde; //se deseja receber um brinde para o pet ou cupom
    char gorjeta[40];
    char reclamacao[40]; //sugestao ou reclamacao

}; 

struct tp_data_nascimento{ //para o cadastro pessoal do cliente
    int dia;
    int mes;
    int ano;
};

struct cadastro_client{
    char nome_cliente [40];
    int telefone;
    char nome_pai [40];
    char nome_mae [40];
    char pet [40]; //se tem animal de estimação.. saber o nome

    //struct dentro de struct 
    struct tp_endereco endereco; //pode usar como tipo de dado dentro do cadastro cliente
    struct tp_dados_pizza dadosPizza; 
    struct tp_data_nascimento data_nascimento;//pra coisar a data nascimento com dia, mes e ano
    
} cad_cliente[2]; //vetor pra poder armazenar mais cliente = 2

typedef struct { //para o ponteiro
    int atributos;  
    float itens; 
    int matricula;
}tTecII;


//oções da parte de MENU do programa
void opcaoUsuario();
void inicio(); //tela padrao dizendo sobre os dados do trabalho
void cadastroCliente(); 
void cadastroLocal();
void cadastroPizza();
void pesquisar();
void ordenacao();


int main(){ //menu principal

    int opcaoUsuario;

    do{
        inicio(); //chamando a tela padrao especificando o trab
        printf("--- MENU (escolha uma opcao)--- \n\n");
        
        printf("Pizzaria *The Good Neighbourhood* \n");

        printf("1-Cadastro do Cliente\n");
        printf("2-Cadastro do Local\n");
        printf("3-Cadastro da Pizza\n");
        printf("4-Pesquisar o item *JA CADASTRADO* (Cliente + Local + Pizza)\n");
        printf("5-Ordenacao dos produtos\n");
        printf("0- SAIR ");
        scanf("%d", &opcaoUsuario);

        switch (opcaoUsuario){
            case 1:
                cadastroCliente(); //opcao para poder cadastrar o cliente
                break;
            case 2:
                cadastroLocal(); //opcao para poder cadastrar o Local
                break;
            case 3:
                cadastroPizza(); //opcao para poder cadastrar a Pizza
                break;
            case 4:
                pesquisar();
                break;  
            case 5:
                ordenacao();
                break;
                
            case 0:
                printf("---------ATENCAO---------\n");
                printf ("Fim do Programa!\n"); //+ponteiro
                printf(" Obrigado!   Pizzaria *The Good Neighbourhood* \n");
                printf("-------------------------\n");

                    //ponteiros
                    tTecII brunna;

                    tTecII *ptrAluno = &brunna;

                    //atribuindo valores para os membros da struct "brunna"
                    brunna.atributos = 5;
                    brunna.itens = 20;

                    //exibindo dados usando a struct diretamente usando ponteiro
                    printf("foram usados: %d atributos e %.2f itens\n", brunna.atributos, brunna.itens);


                getch();
                break;
            
            default:
                printf ("Opção Inválida!\n"); //caso nao seja escolhido as opcoes certas
                getch();
                break;
        } 

    }while (opcaoUsuario != 0); //para encerrar
    
    system("pause");
    return 0;
}

void inicio(){ //tela padrao com as informações do programa/trabalho
    printf("-------------------------------------------------\n");
    printf("*Tarefa 2 do Nap 2 - 2 Possibilidade - Tecnicas de Programacao II - 2020.2*\n");
    printf("Universidade Federal Rural da Amazonia - UFRA\n");
    printf("Docente: Aleksandra Silva\n");
    printf("Discente: Brunna Danielle Santos de Sousa\n ");

        //ponteiros
            tTecII dadosMatricula;

            tTecII *ptrdados = &dadosMatricula;

            //atribuindo valores para os membros da struct "matricula"
            dadosMatricula.matricula = 2020037262;

            //exibindo dados usando um ponteiro para struct 
            printf("Matricula: %d \n", (*ptrdados).matricula);

            //outro modo de escrever ponteiros
            //printf("Matricula: %d \n", dadosMatricula.matricula);
    printf("-------------------------------------------------\n\n");
}

void cadastroCliente(){
    int opcaoUsuario;
    do{ //cadastramento dos dados pessoais do cliente

       int i;

        printf("\n\n ----- Cadastro dos Clientes ----- \n\n");

        //Armazenando os dados do cadastro dentro da struct cad_cliente
        for(i=0; i<2; i++){ //loop para somente 2 clientes 


            printf("\n\n---------------- %d ---------------\n", i+1);

            printf("\nNome do cliente...............:");
            fflush(stdin); //boffer do teclado
            gets(cad_cliente[i].nome_cliente); //nome_cliente = variavel interna

            printf("\nDigite o telefone do cliente..:");
            scanf("%d", &cad_cliente[i].telefone);

            //data_nascimento = separado
            printf("\nDia de nascimento.....:");
            scanf("%d", &cad_cliente[i].data_nascimento.dia);

            printf("\nMes de nascimento.....:");
            scanf("%d", &cad_cliente[i].data_nascimento.mes);

            printf("\nAno de nascimento.....:");
            scanf("%d", &cad_cliente[i].data_nascimento.ano);

            printf("\nNome do pai...................:");
            fflush(stdin); 
            gets(cad_cliente[i].nome_pai); 

            printf("\nNome da mae...................:");
            fflush(stdin); 
            gets(cad_cliente[i].nome_mae); 

            printf("\nNome do pet (se tiver)........:");
            fflush(stdin); 
            gets(cad_cliente[i].pet); 

        }//fim da coleta

        
        printf("0 - SAIR = Ir pro Menu Principal\n");
        scanf("%d", &opcaoUsuario);

    }while (opcaoUsuario != 0);
}

void cadastroLocal(){  //numero rua bairro cidade estado  cep  referencia
    int opcaoUsuario;
    do{ //cadastramento dos dados do Local do cliente

       int i;

        printf("\n\n ----- Cadastro do Local ----- \n\n");

        for(i=0; i<2; i++){ //loop para somente 2 clientes 

            printf("\n\n---------------- %d ---------------\n", i+1);

            printf("\nNumero da casa...............................:");
            scanf("%d", &cad_cliente[i].endereco.numero);

            printf("\nRua..........................................:");
            fflush(stdin); 
            gets(cad_cliente[i].endereco.rua); 

            printf("\nBairro.......................................:");
            fflush(stdin); 
            gets(cad_cliente[i].endereco.bairro); 

            printf("\nCidade.......................................:");
            fflush(stdin); 
            gets(cad_cliente[i].endereco.cidade); 

            printf("\nEstado.......................................:");
            fflush(stdin); 
            gets(cad_cliente[i].endereco.estado);

            printf("\nCep..........................................:");
            scanf("%d", &cad_cliente[i].endereco.cep);
            
            printf("\nReferencia (local proximo)...................:");
            fflush(stdin); 
            gets(cad_cliente[i].endereco.rua); 


        }//fim da coleta

        
        printf("0 - SAIR = Ir pro Menu Principal\n");
        scanf("%d", &opcaoUsuario);

    }while (opcaoUsuario != 0);
}

void cadastroPizza(){
    int opcaoUsuario;
    do{ //cadastramento dos dados da Pizza do cliente

       int i;

        printf("\n\n ----- Cadastro da Pizza ----- \n\n");  

        for(i=0; i<2; i++){ //loop para somente 2 clientes 

            printf("\n\n---------------- %d ---------------\n", i+1);
            
            printf("\nDe que forma foi entrado em contato (wpp/ligacao)...............:"); //forma que o cliente entrou em contato
            scanf("%d", &cad_cliente[i].dadosPizza.localPedido);

            printf("\nTamanho da Pizza...............:");
            fflush(stdin); 
            gets(cad_cliente[i].dadosPizza.tamanhoPizza); 

            printf("\ntipo de forno (lenha ou industrial).............................:"); //2 tipos de forno 
            scanf("%d", &cad_cliente[i].dadosPizza.forno);

            printf("\nSabor da Pizza...............:");
            fflush(stdin); 
            gets(cad_cliente[i].dadosPizza.sabor); 

            printf("\nTipo de Borda...............:"); //caso o cliente deseje botar borda na pizza dele
            fflush(stdin); 
            gets(cad_cliente[i].dadosPizza.borda); 

            printf("\nBebida...............:");
            fflush(stdin); 
            gets(cad_cliente[i].dadosPizza.bebida); 

            printf("\nAcompanhamento...............:"); //caso o cliente deseje algum acompanhamento
            fflush(stdin); 
            gets(cad_cliente[i].dadosPizza.acompanhamento); 

            printf("\nDeseja Brinde (Pet ou Cupom).............................:"); //caso o cliente tenha pet o brinde vai para ele, se nao tiver vai ser um cupom de desconto
            scanf("%d", &cad_cliente[i].dadosPizza.brinde);

            printf("\nGorjeta...............:");
            fflush(stdin); 
            gets(cad_cliente[i].dadosPizza.gorjeta); 

            printf("\nReclamacao ou Sugestao (observacao no modo geral)...............:"); //opniao do cliente
            fflush(stdin); 
            gets(cad_cliente[i].dadosPizza.reclamacao); 
             

        }//fim da coleta

        
        printf("0 - SAIR = Ir pro Menu Principal\n");
        scanf("%d", &opcaoUsuario);

    }while (opcaoUsuario != 0);
}

void pesquisar(){ //Opção para aparecer na tela o que foi cadastrado de dados dos clientes
    int opcaoUsuario;
    do{ 

       int i;

        printf("\n\n ----- Pesquisa o que foi cadastrado----- \n\n");


        for(i=0; i<2; i++){

            printf("\n\n---------------- %d ---------------\n", i+1);

            //5 atributos
            printf("\n Nome........: %s", cad_cliente[i].nome_cliente);
            printf("\n Telefone do cliente........: %d", cad_cliente[i].telefone);

            printf("\n Nome do pai........: %s", cad_cliente[i].nome_pai);
            printf("\n Nome da mae........: %s", cad_cliente[i].nome_mae);
            printf("\n Nome do pet........: %s", cad_cliente[i].pet);


            //20 itens
            printf("\n Dia de nasc do cliente: %d", cad_cliente[i].data_nascimento.dia);
            printf("\n Mes de nasc do cliente: %d", cad_cliente[i].data_nascimento.mes);
            printf("\n Ano de nasc do cliente: %d", cad_cliente[i].data_nascimento.ano); 

            printf("\n Numero........: %d", cad_cliente[i].endereco.numero);
            printf("\n Rua........: %s", cad_cliente[i].endereco.rua);
            printf("\n Bairro........: %s", cad_cliente[i].endereco.bairro);
            printf("\n Cidade........: %s", cad_cliente[i].endereco.cidade);
            printf("\n Estado........: %s", cad_cliente[i].endereco.estado);
            printf("\n Cep........: %d", cad_cliente[i].endereco.cep);
            printf("\n Local de Referencia........: %s", cad_cliente[i].endereco.rua);

            printf("\n Forma de contato........: %d", cad_cliente[i].dadosPizza.localPedido);
            printf("\n Tamanho da Pizza........: %s", cad_cliente[i].dadosPizza.tamanhoPizza);
            printf("\n Preferencia de Forno........: %d", cad_cliente[i].dadosPizza.forno);
            printf("\n Sabor da Pizza........: %s", cad_cliente[i].dadosPizza.sabor);
            printf("\n Tipo de Borda........: %s", cad_cliente[i].dadosPizza.borda);
            printf("\n Bebida........: %s", cad_cliente[i].dadosPizza.bebida);
            printf("\n Acompanhamento........: %s", cad_cliente[i].dadosPizza.acompanhamento);
            printf("\n Brinde........: %d", cad_cliente[i].dadosPizza.brinde);
            printf("\n Gorjeta........: %s", cad_cliente[i].dadosPizza.gorjeta);
            printf("\n Reclamacao ou Sugestao........: %s", cad_cliente[i].dadosPizza.reclamacao);
             

            printf("\n---------------------------------\n");  
        }

        
        printf("0 - SAIR = Ir pro Menu Principal\n");
        scanf("%d", &opcaoUsuario);

    }while (opcaoUsuario != 0);
}


void ordenacao(){
    int opcaoUsuario;
    do{ 

       int vetor [2], aux;

        //pedindo a informação para o usuario
        for(int i=0; i<2; i++){
            printf("Digite o %d numero que deseja ordenar: ", i+1);
            scanf("%d", &vetor[i]);

        }

        //fazendo a ordenação
        for(int x = 0; x<2; x++){
            for(int y = x; y<2; y++){
                if(vetor[x] > vetor [y]){
                    aux = vetor [x];
                    vetor [x] = vetor [y];
                    vetor[y] = aux;
                }
            }
        }

        //mostrando na tela do usuario 
        printf("*Ordenacao Concluida! \n");
        for(int i=0; i<2; i++){
            printf("numero %d =  %d\n", i+1, vetor[i]);
        }

        
        printf("0 - SAIR = Ir pro Menu Principal\n");
        scanf("%d", &opcaoUsuario);

    }while (opcaoUsuario != 0);
}

