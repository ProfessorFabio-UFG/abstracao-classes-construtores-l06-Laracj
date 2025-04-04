Main 

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        Produto[] p = new Produto[5];

        p[0] = new Produto(001, "Jogo Batalha Naval", 10, "jogo", 100.00);
        p[1] = new Produto(002, "Jogo Master", 20, "jogo", 150.00);
        p[2] = new Produto(003, "Jogo Quebra-Cabeça", 30, "jogo", 50.00);

        for (int i = 3; i < p.length; i++) {
            System.out.println("Digite o código do produto:");
            int codigo = sc.nextInt();
            System.out.println("Digite o nome do produto: ");
            String nome = sc.next();
            System.out.println("Digite a quantidade do produto: ");
            int quantidade = sc.nextInt();
            System.out.println("Digite o tipo do produto: ");
            String tipo = sc.next();
            System.out.println("Digite o preco do produto: ");
            double preco = sc.nextDouble();

            p[i] = new Produto(codigo, nome, quantidade, tipo, preco);

        }

        boolean loop = true;
        while (loop) {
            System.out.println("Digite o numero da acao que deseja executar:"
                    + "\n(1)Vender"
                    + "\n(2)Comprar"
                    + "\n(3)Consultar"
                    + "\n(4)Inserir"
                    + "\n(5)Comparar");

            int opcao = sc.nextInt();
            System.out.println("Digite o codigo do produto: ");
            int num = sc.nextInt() - 1;

            if (opcao == 1) {

                System.out.println("Digite a quantidade a ser vendida: ");
                int quantidade = sc.nextInt();

                if (p[num].vender(quantidade) > 0) {
                    System.out.println("Total: " + p[num].vender(quantidade));
                } else {
                    System.out.println(p[num].vender(quantidade));
                }
            } else if (opcao == 2) {

                System.out.println("Alterar preco?"
                        + "(1) Sim"
                        + "(2) Nao");
                int aux = sc.nextInt();

                if (aux == 1) {
                    System.out.println("Digite a quantidade: ");
                    int quantidade = sc.nextInt();
                    System.out.println("Novo preco: ");
                    double preco = sc.nextDouble();

                    p[num].comprar(quantidade, preco);
                } else {
                    System.out.println("Digite a quantidade: ");
                    int quantidade = sc.nextInt();
                    p[num].comprar(quantidade);
                }

            } else if (opcao == 3) {
                System.out.println(p[num].consultar());
            } else if (opcao == 4) {
                System.out.println("Digite o nome do produto: ");
                String nome = sc.nextLine();
                System.out.println("Digite a quantidade do produto: ");
                int quantidade = sc.nextInt();
                System.out.println("Digite o tipo do produto: ");
                String tipo = sc.nextLine();
                System.out.println("Digite o preco do produto: ");
                double preco = sc.nextDouble();

                p[num].inserir(nome, tipo, quantidade, preco);
            }else{
                System.out.println("Digite o codigo do Produto que deseja comparar com o Produto "+(num+1));
                int aux = sc.nextInt();

                System.out.println(p[num].igual(p[aux]));
            }

            System.out.println("(1)Sair"
                    + "\n(2)Continuar");
            opcao = sc.nextInt();

            if(opcao == 1){
                loop = false;
            }

        }

    }
    }






    Classe Produto



    public class Produto {

    int codigo;
    String nome, tipo;
    int quantidade;
    double preco;

    Produto(int codigo) {
        this.codigo = codigo;
    }

    Produto(int codigo, String nome) {
        this.codigo = codigo;
        this.nome = nome;
    }

    Produto(int codigo, String nome, int quantidade) {
        this.codigo = codigo;
        this.nome = nome;
        this.quantidade = quantidade;
    }

    Produto(int codigo, String nome, int quantidade, String tipo, double preco) {
        this.codigo = codigo;
        this.nome = nome;
        this.tipo = tipo;
        this.quantidade = quantidade;
        this.preco = preco;
    }

    double vender(int quantidade) {
        if (this.quantidade >= quantidade) {
            this.quantidade = this.quantidade - quantidade;
            return preco * quantidade;
        } else {
            System.out.println("Não tem estoque do produto");
            return 0;
        }
    }

    void comprar(int qunantidade, double preco) {
        this.quantidade = this.quantidade + qunantidade;
        this.preco = preco;
    }

    void comprar(int qunantidade) {
        this.quantidade = this.quantidade + qunantidade;
    }

    void inserir(String nome, String tipo, int quantidade, double preco) {
        this.nome = nome;
        this.tipo = tipo;
        this.quantidade = quantidade;
        this.preco = preco;
    }

    boolean igual(Produto produto) {
        if (this.nome.equals(produto.nome) && this.tipo.equals(produto.tipo)) {
            return true;
        } else {
            return false;
        }
    }

    public String consultar() {
        return "Codigo: " + this.codigo
                + "\nNome: " + this.nome
                + "\nQuantidade" + this.quantidade
                + "\nTipo" + this.tipo
                + "\nPreco" + this.preco;
    }
}
