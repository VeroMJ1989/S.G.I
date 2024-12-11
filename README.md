#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Estructura para representar un producto
struct Producto {
    int id;
    string nombre;
    int cantidad;
    double precio;
};
// Clase para la gestión de inventarios
class Inventario {
private:
    vector<Producto> productos;
public:
    // Agregar un nuevo producto
    void agregarProducto(int id, string nombre, int cantidad, double precio) {
        Producto nuevoProducto = {id, nombre, cantidad, precio};
        productos.push_back(nuevoProducto);
        cout << "Producto agregado con éxito.\n";
    }
    // Mostrar todos los productos
    void mostrarProductos() {
        if (productos.empty()) {
            cout << "El inventario está vacío.\n";
            return;
        }
        cout << "ID\tNombre\t\tCantidad\tPrecio\n";
        for (const auto &producto : productos) {
            cout << producto.id << "\t" << producto.nombre << "\t\t" << producto.cantidad << "\t\t$" << producto.precio << "\n";
        }
    }
    // Buscar un producto por ID
    void buscarProducto(int id) {
        for (const auto &producto : productos) {
            if (producto.id == id) {
                cout << "Producto encontrado:\n";
                cout << "ID: " << producto.id << "\nNombre: " << producto.nombre
                     << "\nCantidad: " << producto.cantidad << "\nPrecio: $" << producto.precio << "\n";
                return;
            }
        }
        cout << "Producto con ID " << id << " no encontrado.\n";
    }
    // Eliminar un producto por ID
    void eliminarProducto(int id) {
        for (auto it = productos.begin(); it != productos.end(); ++it) {
            if (it->id == id) {
                productos.erase(it);
                cout << "Producto eliminado con éxito.\n";
                return;
            }
        }
        cout << "Producto con ID " << id << " no encontrado.\n";
    }
};
// Función principal
int main() {
    Inventario inventario;
    int opcion;
    do {
        cout << "\nSistema de Gestión de Inventarios\n";
        cout << "1. Agregar producto\n";
        cout << "2. Mostrar productos\n";
        cout << "3. Buscar producto\n";
        cout << "4. Eliminar producto\n";
        cout << "5. Salir\n";
        cout << "Seleccione una opción: ";
        cin >> opcion;
        switch (opcion) {
            case 1: {
                int id, cantidad;
                string nombre;
                double precio;
                cout << "Ingrese el ID del producto: ";
                cin >> id;
                cin.ignore(); // Limpiar el buffer
                cout << "Ingrese el nombre del producto: ";
                getline(cin, nombre);
                cout << "Ingrese la cantidad: ";
                cin >> cantidad;
                cout << "Ingrese el precio: ";
                cin >> precio;
                inventario.agregarProducto(id, nombre, cantidad, precio);
                break;
            }
            case 2:
                inventario.mostrarProductos();
                break;
            case 3: {
                int id;
                cout << "Ingrese el ID del producto a buscar: ";
                cin >> id;
                inventario.buscarProducto(id);
                break;
            }
            case 4: {
                int id;
                cout << "Ingrese el ID del producto a eliminar: ";
                cin >> id;
                inventario.eliminarProducto(id);
                break;
            }
            case 5:
                cout << "Saliendo del sistema.\n";
                break;
            default:
                cout << "Opción no válida. Intente de nuevo.\n";
        }
    } while (opcion != 5);

    return 0;
}
