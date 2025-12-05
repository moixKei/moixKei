<h2 align="center">🌸 Xiomara — Desarrolladora Full Stack</h2> 
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&pause=1000&color=F4A7C1&center=true&vCenter=true&width=500&lines=Full+Stack+Developer;Clean+Code+%26+Aesthetic+Designs;Java+%7C+Kotlin+%7C+C%23+%7C+React" />
</p>

## 🌺 Sobre Mí

```kotlin
object Kei {
    const val NAME = "Xiomara"
    val SPECIALTIES = listOf("Backend", "Frontend", "Mobile")
    val TECH_STACK = listOf("Java", "Kotlin", "C#", "React", "SQL", "Postman", ".NET")

    fun passion() = "Crear soluciones limpias, escalables y bien diseñadas"
    fun focus() = "Desarrollo full stack y apps empresariales"
}
```

Soy una desarrolladora centrada en backend empresarial, frontend moderno y apps móviles.
Apasionada por crear arquitecturas sólidas, APIs eficientes y experiencias intuitivas.
Busco siempre el equilibrio entre robustez técnica y diseño elegante 🌸.

---

## 🛠 Tech Stack

### Backend & Lenguajes

<img src="https://skillicons.dev/icons?i=java,kotlin,cs,spring,hibernate,net" />

### Frontend & Bases de Datos

<img src="https://skillicons.dev/icons?i=react,angular,js,html,css,mysql,mongodb" />

### Herramientas

<img src="https://skillicons.dev/icons?i=git,github,vscode,visualstudio,eclipse,idea,postman" />

---

## 📊 GitHub Stats

<div align="center"> <img src="https://github-readme-stats.vercel.app/api?username=moixKei&show_icons=true&hide_border=true&bg_color=0d1117&title_color=ec4899&icon_color=f472b6&text_color=f3f4f6&hide=issues&count_private=true&include_all_commits=true" width="400" /> <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=moixKei&layout=compact&hide_border=true&bg_color=0d1117&title_color=ec4899&text_color=f3f4f6&langs_count=8&hide=html,css,scss" width="350" /> <img src="https://streak-stats.demolab.com/?user=moixKei&theme=rose&hide_border=true&background=0D1117&ring=EC4899&fire=EC4899&currStreakLabel=EC4899" /> </div>

---

## 🌸 Proyectos Destacados

### mcAulley Management — Sistema Educativo

[![Repo](https://img.shields.io/badge/%F0%9F%94%97_Repositorio-f9a8d4?style=for-the-badge\&logo=github\&logoColor=white)](https://github.com/moixKei/mcAulley_management)

**Tecnologías:** Java • JPA • Hibernate • MySQL

<details>
<summary>🌸 Ver código</summary>

```java
@Entity
@Table(
    name = "tb_alumnas",
    uniqueConstraints = {
        @UniqueConstraint(columnNames = "dni", name = "uk_alumna_dni"),
        @UniqueConstraint(columnNames = "correo", name = "uk_alumna_correo")
    }
)
@Getter
@Setter
@ToString
public class Alumna {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id_alumna")
    private Integer idAlumna; // Nombre más descriptivo

    @Column(name = "nombre", nullable = false, length = 100)
    private String nombre;

    @Column(name = "apellido", nullable = false, length = 100)
    private String apellido;

    @Column(name = "dni", nullable = false, unique = true, length = 15)
    private String dni;

    @Column(name = "correo", length = 100)
    private String correo;

    @Column(name = "celular", length = 20)
    private String celular;

    @Column(name = "direccion", length = 200)
    private String direccion;

    @Column(name = "fecha_registro", updatable = false)
    private LocalDate fechaRegistro;

    @Column(name = "fecha_actualizacion")
    private LocalDateTime fechaActualizacion;

    @Column(name = "activo")
    private Boolean activo = true;

    // Constructor por defecto
    public Alumna() {
        this.fechaRegistro = LocalDate.now();
        this.activo = true;
    }

    // Constructor con parámetros básicos
    public Alumna(String nombre, String apellido, String dni) {
        this();
        this.nombre = nombre;
        this.apellido = apellido;
        this.dni = dni;
    }

    // Método helper para nombre completo
    public String getNombreCompleto() {
        return this.nombre + " " + this.apellido;
    }

    // Método helper para validar datos básicos
    public boolean esValida() {
        return this.nombre != null && !this.nombre.trim().isEmpty() &&
               this.apellido != null && !this.apellido.trim().isEmpty() &&
               this.dni != null && !this.dni.trim().isEmpty();
    }

    // Callback antes de persistir
    @PrePersist
    protected void onCreate() {
        if (this.fechaRegistro == null) {
            this.fechaRegistro = LocalDate.now();
        }
        this.fechaActualizacion = LocalDateTime.now();
        if (this.activo == null) {
            this.activo = true;
        }
    }

    // Callback antes de actualizar
    @PreUpdate
    protected void onUpdate() {
        this.fechaActualizacion = LocalDateTime.now();
    }
}
```

</details>

---

### Gestor de Gastos Personales — Android

[![Repo](https://img.shields.io/badge/%F0%9F%94%97_Repositorio-f9a8d4?style=for-the-badge\&logo=github\&logoColor=white)](https://github.com/moixKei/Gestor_Gasto)

**Tecnologías:** Kotlin • Room • Material Design

<details>
<summary>🌸 Ver código</summary>

```kotlin
class GastoViewModel : ViewModel() {

    private val gestorGastos = GestorGastos()

    // LiveData para la UI
    private val _listaGastos = MutableLiveData<List<Gasto>>()
    val listaGastos: LiveData<List<Gasto>> = _listaGastos

    private val _totalGeneral = MutableLiveData<Double>()
    val totalGeneral: LiveData<Double> = _totalGeneral

    private val _mensajeError = MutableLiveData<String>()
    val mensajeError: LiveData<String> = _mensajeError

    private val _mensajeExito = MutableLiveData<String>()
    val mensajeExito: LiveData<String> = _mensajeExito

    private val _categoriaFiltro = MutableLiveData<String?>()
    val categoriaFiltro: LiveData<String?> = _categoriaFiltro

    private val _modoHistorial = MutableLiveData<ModoHistorial>(ModoHistorial.LISTA_NORMAL)
    val modoHistorial: LiveData<ModoHistorial> = _modoHistorial

    // Categorías disponibles
    val categorias = listOf("Alimentos", "Transporte", "Entretenimiento", "Compras", "Otros")

    init {
        actualizarDatos()
    }

    fun agregarGasto(descripcion: String, monto: Double, categoria: String) {
        try {
            val fecha = SimpleDateFormat("dd/MM/yyyy HH:mm", Locale.getDefault()).format(Date())
            val gasto = Gasto(
                descripcion = descripcion,
                monto = monto,
                categoria = categoria,
                fecha = fecha
            )

            gestorGastos.agregarGasto(gasto)
            actualizarDatos()
            _mensajeExito.value = "Gasto agregado correctamente"
        } catch (e: Exception) {
            _mensajeError.value = "Error al agregar gasto: ${e.message}"
        }
    }

    fun eliminarGasto(gasto: Gasto) {
        try {
            gestorGastos.eliminarGasto(gasto)
            actualizarDatos()
            _mensajeExito.value = "Gasto eliminado correctamente"
        } catch (e: Exception) {
            _mensajeError.value = "Error al eliminar gasto: ${e.message}"
        }
    }

    fun filtrarPorCategoria(categoria: String?) {
        _categoriaFiltro.value = categoria
        actualizarDatos()
    }

    fun cambiarModoHistorial(modo: ModoHistorial) {
        _modoHistorial.value = modo
    }

    fun limpiarMensajes() {
        _mensajeError.value = ""
        _mensajeExito.value = ""
    }

    private fun actualizarDatos() {
        val categoria = _categoriaFiltro.value
        val gastosFiltrados = gestorGastos.getGastosPorCategoria(categoria)

        _listaGastos.value = gastosFiltrados
        _totalGeneral.value = gestorGastos.calcularTotal()
    }

    // Métodos para obtener datos agrupados
    fun getGastosAgrupadosPorDia(): Map<String, List<Gasto>> {
        return gestorGastos.getGastosAgrupadosPorDia()
    }

    fun getGastosAgrupadosPorMes(): Map<String, List<Gasto>> {
        return gestorGastos.getGastosAgrupadosPorMes()
    }

    fun getTotalPorDia(): Map<String, Double> {
        return gestorGastos.getTotalPorDia()
    }

    fun getTotalPorMes(): Map<String, Double> {
        return gestorGastos.getTotalPorMes()
    }

    fun getEstadisticas(): Map<String, Double> {
        return gestorGastos.getEstadisticasPorCategoria()
    }

    // Método para obtener colores de categorías
    fun getColorCategoria(categoria: String): Int {
        return when (categoria) {
            "Alimentos" -> Color.parseColor("#4CAF50")  // Verde
            "Transporte" -> Color.parseColor("#2196F3")  // Azul
            "Entretenimiento" -> Color.parseColor("#9C27B0")  // Morado
            "Compras" -> Color.parseColor("#FF9800")  // Naranja
            "Otros" -> Color.parseColor("#795548")  // Marrón
            else -> Color.parseColor("#607D8B")  // Gris azulado
        }
    }

    enum class ModoHistorial {
        LISTA_NORMAL, POR_DIA, POR_MES
    }
}
```

</details>

---

### KitagawaStore — E-commerce API

[![Repo](https://img.shields.io/badge/%F0%9F%94%97_Repositorio-f9a8d4?style=for-the-badge\&logo=github\&logoColor=white)](https://github.com/moixKei/KitagawaStore_Plataform)

**Tecnologías:** C# • ASP.NET Core 

<details>
<summary>🌸 Ver código</summary>

```csharp
namespace app_API_proyecto.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class KitagawaController : ControllerBase
    {
        [HttpGet("productos")]
        public async Task<ActionResult<List<Producto>>> GetProductos()
        {
            var lista = await Task.Run(() => new ProductoDAO().GetProductos());
            return Ok(lista);
        }

        [HttpGet("categorias")]
        public async Task<ActionResult<List<Categoria>>> GetCategorias()
        {
            var lista = await Task.Run(() => new CategoriaDAO().GetCategorias());
            return Ok(lista);
        }

        [HttpGet("paises")]
        public async Task<ActionResult<List<Pais>>> GetPaises()
        {
            var lista = await Task.Run(() => new PaisDAO().GetPaises());
            return Ok(lista);
        }

        [HttpGet("productos/{id}")]
        public async Task<ActionResult<Producto>> GetProducto(int id)
        {
            var producto = await Task.Run(() => new ProductoDAO().GetProducto(id));
            if (producto == null)
                return NotFound($"No se encontró el producto con ID {id}");

            return Ok(producto);
        }

        [HttpPost("productos")]
        public async Task<ActionResult<string>> InsertProducto([FromBody] Producto reg)
        {
            if (!ModelState.IsValid)
                return BadRequest(ModelState);

            string mensaje = await Task.Run(() => new ProductoDAO().CreateProducto(reg));
            return Ok(mensaje);
        }

        [HttpPut("productos")]
        public async Task<ActionResult<string>> UpdateProducto([FromBody] Producto reg)
        {
            if (!ModelState.IsValid)
                return BadRequest(ModelState);

            string mensaje = await Task.Run(() => new ProductoDAO().UpdateProducto(reg));
            return Ok(mensaje);
        }
        [HttpGet("productos/categoria/{idCategoria}")]
        public async Task<ActionResult<List<Producto>>> GetProductosPorCategoria(int idCategoria)
        {
            var productos = await Task.Run(() => new ProductoDAO().GetProductosPorCategoria(idCategoria));

            if (productos == null || !productos.Any())
            {
                return NotFound($"No se encontraron productos para la categoría con ID {idCategoria}");
            }

            return Ok(productos);
        }

        [HttpDelete("productos/{id}")]
        public async Task<ActionResult<string>> DeleteProducto(int id)
        {
            if (id <= 0)
                return BadRequest("ID de producto no válido");

            try
            {
                string mensaje = await Task.Run(() => new ProductoDAO().DeleteProducto(id));

                // Verificar si el mensaje indica éxito o error
                if (mensaje.Contains("Error") || mensaje.Contains("no existe") || mensaje.Contains("No se puede"))
                {
                    return BadRequest(mensaje);
                }

                return Ok(mensaje);
            }
            catch (Exception ex)
            {
                return StatusCode(500, $"Error interno del servidor: {ex.Message}");
            }
        }
    }
}
```

</details>

---

## 📚 Skills & Metodología

### Competencias

* Arquitecturas empresariales
* Apps Android nativas
* Bases de datos & ORM
* MVC, Repository, DI
* SQL optimizado

### Aprendiendo

* Swift
* Microservicios
* Clean Architecture

### Forma de trabajo

```yaml
valores:
  - calidad
  - aprendizaje continuo
  - detalle
  - colaboración

workflow:
  - análisis
  - código limpio
  - documentación
  - testing
```

---

## 💌 Conecta Conmigo

<p align="center">
  <a href="https://www.linkedin.com/in/xiomara-borda-poma-91abba366/">
    <img src="https://img.shields.io/badge/LinkedIn-f472b6?style=for-the-badge&logo=linkedin&logoColor=white" />
  </a>
  <a href="mailto:xiomara.bordax@gmail.com">
    <img src="https://img.shields.io/badge/Email-ec4899?style=for-the-badge&logo=gmail&logoColor=white" />
  </a>
  <a href="https://github.com/moixKei">
    <img src="https://img.shields.io/badge/Portfolio-be185d?style=for-the-badge&logo=github&logoColor=white" />
  </a>
</p>

---

<div align="center">

<img src="https://komarev.com/ghpvc/?username=moixKei&color=f472b6" />

✨ *"Escribiendo el futuro, pétalo a pétalo, commit a commit"* 🌸

</div>
