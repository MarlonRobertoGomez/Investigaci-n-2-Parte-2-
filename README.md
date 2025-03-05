Builder
public class Auto
{
    public string Modelo { get; set; }
    public string Motor { get; set; }
    public string Color { get; set; }
    public int NumeroPuertas { get; set; }

    public override string ToString()
    {
        return $"Auto: {Modelo}, Motor: {Motor}, Color: {Color}, Puertas: {NumeroPuertas}";
    }
}
public interface IAutoBuilder
{
    void SetModelo(string modelo);
    void SetMotor(string motor);
    void SetColor(string color);
    void SetNumeroPuertas(int puertas);
    Auto Build();
}
public class AutoBuilder : IAutoBuilder
{
    private Auto _auto = new Auto();

    public void SetModelo(string modelo) => _auto.Modelo = modelo;
    public void SetMotor(string motor) => _auto.Motor = motor;
    public void SetColor(string color) => _auto.Color = color;
    public void SetNumeroPuertas(int puertas) => _auto.NumeroPuertas = puertas;
    public Auto Build() => _auto;
}
public class Director
{
    private IAutoBuilder _builder;

    public Director(IAutoBuilder builder)
    {
        _builder = builder;
    }

    public void ConstruirAutoDeportivo()
    {
        _builder.SetModelo("Deportivo");
        _builder.SetMotor("V8");
        _builder.SetColor("Rojo");
        _builder.SetNumeroPuertas(2);
    }

    public void ConstruirAutoFamiliar()
    {
        _builder.SetModelo("Familiar");
        _builder.SetMotor("V4");
        _builder.SetColor("Azul");
        _builder.SetNumeroPuertas(4);
    }
}
class Program
{
    static void Main(string[] args)
    {
        IAutoBuilder builder = new AutoBuilder();
        Director director = new Director(builder);

        // Construir un Auto Deportivo
        director.ConstruirAutoDeportivo();
        Auto autoDeportivo = builder.Build();
        Console.WriteLine(autoDeportivo);

        // Construir un Auto Familiar
        builder = new AutoBuilder();  // Resetear el builder
        director = new Director(builder);
        director.ConstruirAutoFamiliar();
        Auto autoFamiliar = builder.Build();
        Console.WriteLine(autoFamiliar);
    }
}

Abstract Factory
// Producto abstracto: Auto
public interface IAuto
{
    void MostrarModelo();
}

// Producto abstracto: Moto
public interface IMoto
{
    void MostrarModelo();
}
// Implementación concreta de Auto - Toyota
public class ToyotaAuto : IAuto
{
    public void MostrarModelo()
    {
        Console.WriteLine("Toyota Corolla");
    }
}

// Implementación concreta de Auto - Honda
public class HondaAuto : IAuto
{
    public void MostrarModelo()
    {
        Console.WriteLine("Honda Civic");
    }
}

// Implementación concreta de Moto - Toyota
public class ToyotaMoto : IMoto
{
    public void MostrarModelo()
    {
        Console.WriteLine("Toyota Moto 125cc");
    }
}

// Implementación concreta de Moto - Honda
public class HondaMoto : IMoto
{
    public void MostrarModelo()
    {
        Console.WriteLine("Honda CBR 500R");
    }
}
// Fábrica Abstracta
public interface IFabricaVehiculos
{
    IAuto CrearAuto();
    IMoto CrearMoto();
}
// Fábrica concreta de Toyota
public class ToyotaFactory : IFabricaVehiculos
{
    public IAuto CrearAuto()
    {
        return new ToyotaAuto();
    }

    public IMoto CrearMoto()
    {
        return new ToyotaMoto();
    }
}

// Fábrica concreta de Honda
public class HondaFactory : IFabricaVehiculos
{
    public IAuto CrearAuto()
    {
        return new HondaAuto();
    }

    public IMoto CrearMoto()
    {
        return new HondaMoto();
    }
}
class Program
{
    static void Main(string[] args)
    {
        // Fábrica de Toyota
        IFabricaVehiculos toyotaFactory = new ToyotaFactory();
        IAuto toyotaAuto = toyotaFactory.CrearAuto();
        IMoto toyotaMoto = toyotaFactory.CrearMoto();

        toyotaAuto.MostrarModelo();
        toyotaMoto.MostrarModelo();

        // Fábrica de Honda
        IFabricaVehiculos hondaFactory = new HondaFactory();
        IAuto hondaAuto = hondaFactory.CrearAuto();
        IMoto hondaMoto = hondaFactory.CrearMoto();

        hondaAuto.MostrarModelo();
        hondaMoto.MostrarModelo();
    }
}
