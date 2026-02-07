let inventario = []; 
let ventasTotalesDia = 0;

function registrarMedicamento() {
    let nombre = prompt("Ingrese el nombre del medicamento:").toLowerCase();
    
    let existe = inventario.find(med => med.nombre === nombre);
    if (existe) {
        alert("Este medicamento ya existe, use la opción de vender o actualice el stock manualmente.");
        return;
    }

    let cantidad = parseInt(prompt("Ingrese la cantidad inicial:"));
    let precio = parseFloat(prompt("Ingrese el precio unitario:"));

    if (isNaN(cantidad) || isNaN(precio) || cantidad < 0 || precio < 0) {
        alert("Error, ingrese cantidades y precios validos.");
        return;
    }

    let nuevoMedicamento = {
        nombre: nombre,
        cantidad: cantidad,
        precio: precio
    };

    inventario.push(nuevoMedicamento);
    alert(`${nombre} registrado con exito.`);
}

function consultarInventario() {
    if (inventario.length === 0) {
        alert("El inventario esta vacio.");
        return;
    }

    let mensaje = "Inventario actual:\n\n";
    inventario.forEach((med, index) => {
        mensaje += `${index + 1}. ${med.nombre.toUpperCase()} | Stock: ${med.cantidad} | Precio: $${med.precio}\n`;
    });

    alert(mensaje);
}

function venderMedicamento() {
    let nombreBusqueda = prompt("Ingrese el nombre del medicamento para vender:").toLowerCase();
    
    let medicamento = inventario.find(med => med.nombre === nombreBusqueda);

    if (!medicamento) {
        alert("El medicamento no existe en el inventario.");
        return;
    }

    let cantidadVenta = parseInt(prompt(`Hay ${medicamento.cantidad} unidades de ${medicamento.nombre}. Cuantas desea vender?`));

    if (isNaN(cantidadVenta) || cantidadVenta <= 0) {
        alert("Cantidad invalida.");
    } else if (cantidadVenta > medicamento.cantidad) {
        alert("Stock insuficiente, solo quedan " + medicamento.cantidad + " unidades.");
    } else {
        medicamento.cantidad -= cantidadVenta;
        let totalVenta = cantidadVenta * medicamento.precio;
        ventasTotalesDia += totalVenta;
        
        alert(`Venta realizada, total a cobrar: $${totalVenta}. Quedan ${medicamento.cantidad} unidades.`);
    }
}

function mostrarTotalVentas() {
    alert(`El total de ventas acumulado en el dia es: $${ventasTotalesDia}`);
}


function iniciarSistema() {
    let continuar = true;

    while (continuar) {
        let opcion = prompt(
            "Juan Farmacia - sistema de gestion\n" +
            "Seleccione una opcion:\n" +
            "1. Registrar medicamento\n" +
            "2. Consultar inventario\n" +
            "3. Vender medicamento\n" +
            "4. Ver total ventas del dia\n" +
            "5. Salir"
        );

        switch (opcion) {
            case "1":
                registrarMedicamento();
                break;
            case "2":
                consultarInventario();
                break;
            case "3":
                venderMedicamento();
                break;
            case "4":
                mostrarTotalVentas();
                break;
            case "5":
                continuar = false;
                alert("Adios, Juan");
                break;
            default:
                alert("Opcion no valida, intente de nuevo.");
        }
    }
}

iniciarSistema();
