import java.util.*;

public class Persona {
    private int id;
    private String nombreCompleto;
    private int edad;
    private int prioridad;
    private Set<Persona> amigos;

    public Persona(int id, String nombreCompleto, int edad, int prioridad) {
        this.id = id;
        this.nombreCompleto = nombreCompleto;
        this.edad = edad;
        this.prioridad = prioridad;
        this.amigos = new HashSet<>();
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getNombreCompleto() {
        return nombreCompleto;
    }

    public void setNombreCompleto(String nombreCompleto) {
        this.nombreCompleto = nombreCompleto;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }

    public int getPrioridad() {
        return prioridad;
    }

    public void setPrioridad(int prioridad) {
        this.prioridad = prioridad;
    }

    public Set<Persona> getAmigos() {
        return amigos;
    }

    public void setAmigos(Set<Persona> amigos) {
        this.amigos = amigos;
    }

    public void agregarAmigo(Persona amigo) {
        amigos.add(amigo);
    }

    public void eliminarAmigo(Persona amigo) {
        amigos.remove(amigo);
    }
}

public class SocialNetwork {
    private Queue<Persona> colaEspera;
    private PriorityQueue<Persona> colaPrioridad;
    private Stack<Persona> pilaEliminados;

    public SocialNetwork() {
        this.colaEspera = new LinkedList<>();
        this.colaPrioridad = new PriorityQueue<>(Comparator.comparingInt(Persona::getPrioridad));
        this.pilaEliminados = new Stack<>();
    }

    public void agregarPersona(Persona persona) {
        // Verificar si ya existe una persona con el mismo nombre completo
        if (colaEspera.stream().anyMatch(p -> p.getNombreCompleto().equals(persona.getNombreCompleto())) ||
                colaPrioridad.stream().anyMatch(p -> p.getNombreCompleto().equals(persona.getNombreCompleto())) ||
                pilaEliminados.stream().anyMatch(p -> p.getNombreCompleto().equals(persona.getNombreCompleto()))) {
            throw new IllegalArgumentException("Ya existe una persona con el mismo nombre completo");
        }
        colaEspera.add(persona);
    }

    public List<Persona> buscarPersona(int id, boolean buscarEnColaEspera) {
        List<Persona> resultados = new ArrayList<>();
        Queue<Persona> colaBuscar = buscarEnColaEspera ? colaEspera : colaPrioridad;
        for (Persona persona : colaBuscar) {
            if (persona.getId() == id) {
                resultados.add(persona);
            }
        }
        return resultados;
    }


