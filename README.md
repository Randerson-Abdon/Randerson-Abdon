class Aluno {
    public String n;
    public double nt;
    public boolean bolsista;

    public Aluno(String n, double nt, boolean bolsista) {
        this.n = n;
        this.nt = nt;
        this.bolsista = bolsista;
    }
}

class AlunoBolsista extends Aluno {
    public double bolsa;

    public AlunoBolsista(String n, double nt) {
        super(n, nt, true);
        this.bolsa = 1000.0;
    }
    
    @Override
    public String toString() {
        return n + " - Bolsa: R$" + bolsa;
    }
}

interface Repositorio {
    void salvar(Aluno a);
    void deletar(int id);
    List<Aluno> buscarTodos();
}

class RepositorioAluno implements Repositorio {
    private List<Aluno> lista = new ArrayList<>();

    public void salvar(Aluno a) {
        lista.add(a);
    }

    public void deletar(int id) {
        lista.remove(id);
    }

    public List<Aluno> buscarTodos() {
        return lista;
    }
}

class AlunoService {
    private RepositorioAluno repo = new RepositorioAluno();

    public void cadastrar(String n, double nt, boolean bolsista) {
        Aluno a = new Aluno(n, nt, bolsista);
        repo.salvar(a);
    }

    public void calcularMedia() {
        double soma = 0;
        for (Aluno a : repo.buscarTodos()) {
            soma += a.nt;
        }
        System.out.println("Média geral: " + (soma / repo.buscarTodos().size()));
    }

    public void notificarAlunos() {
        for (Aluno a : repo.buscarTodos()) {
            if (a.nt < 6.0) {
                System.out.println("Aluno " + a.n + " REPROVADO.");
            } else {
                System.out.println("Aluno " + a.n + " APROVADO.");
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        AlunoService service = new AlunoService();
        service.cadastrar("Ana", 8.5, false);
        service.cadastrar("Carlos", 4.0, false);
        service.cadastrar("Lucas", 7.2, true);

        service.calcularMedia();
        service.notificarAlunos();
    }
}
