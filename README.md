//# PRACTICA8

import java.util.HashMap;
import java.util.Scanner;


class Producto{

	String nombre;
	float precio;
	int cantDisp;
	int id_prod;

	boolean verificaDisponibilidad(int cantReq){
		if(cantReq<=cantDisp)
			return true;
		else
			return false;
	}

	void incrementarStock(int cant){
		cantDisp+=cant;
	}

	void decrementarStock(int cant){
		if(verificaDisponibilidad(cant))
			cantDisp-=cant;
		else
			System.out.println("Stock insuficiente");
	}

	public String toString(){
		return "Producto: "+nombre+"\nPrecio: "+precio;
	}
}

class Papeleria extends Producto{
	String tamanio;
	int cantHojas;
	String color;

	void defTamanoPapel(int alto, int ancho){
		if(alto==28 && ancho==22)
			tamanio="Carta";
		else if(alto==34 && ancho==22)
			tamanio="Oficio";
		else if(alto==28 && ancho==44)
			tamanio="Doble Carta";
		else
			tamanio="Pliego";
	}
}

class DeEscritura extends Producto{
	String tipopunta;
	String material;
	String formapunta;
	}

class HerramientasComputo extends Producto{

}

class Cuaderno extends Papeleria{
	String tipoguia;
}

class PaqueteHojas extends Papeleria{

}

class Pluma extends DeEscritura{
	String color;
}

class Lapiz extends DeEscritura{
	String color;
}

class Marcador extends DeEscritura{
	String uso;
	String color;
}

class Calculadora extends HerramientasComputo{
	String marca;
}

class Computadora extends HerramientasComputo{
	String SO;
	String color;
}

class Cliente{
	String nombre;
	String email;
	String direccion;
	String formaPago;
	String celular;

	void actualizarDatos(String direccion, String celular){
		this.direccion=direccion;
		this.celular=celular;
	}

	Cliente(String n,String email){
		nombre=n;
		this.email=email;
	}
}

class Proveedor{
	String nombre;
	String RFC;
	String email;
	String direccion;
	String celular;

	Proveedor(String n, String rfc){
		nombre=n;
		this.RFC=rfc;
	}
}


class CarritoCompras{

	HashMap<String, Float> utiles = new HashMap <String, Float> ();	
	Cliente cliente;
	float costoTotal;
	//Producto articulos[];
	//int cont;

	CarritoCompras(Cliente c){
		cliente=c;
		//articulos=new Producto[10];
	}

	void agregarACarrito(Producto p, Producto c){
		if(utiles.size() < 10){
			if(p.verificaDisponibilidad(1)){
				/*articulos[cont]=p;
				cont++;*/
				utiles.put(p.nombre , p.precio);

				p.decrementarStock(1);
			}	
		}else{
			System.out.println("Espacio insuficiente en carrito");
		}
	}

	void quitardelCarrito(Producto p){

		for(String i : utiles.keySet()){
			if(i== p.nombre){
				utiles.remove(i);
				recorreCarrito(i);
				//cont--;
			}
		}
	}

	void recorreCarrito(String index){
		for(String i : utiles.keySet()){
				//articulos[i]=articulos[i+1];
			System.out.println (utiles.get(i));
		}
	}

	void calcularCostoCarrito(){
		costoTotal=0;
		for(String i : utiles.keySet()){
			costoTotal =utiles.get(i) + costoTotal;
		}
	}

	void mostrarCarrito(){

		System.out.println("Carrito de "+cliente.nombre+":\n");

		for(String i : utiles.keySet()){
			System.out.println("Product."+ i + "$" + utiles.get(i) );
		}
	}

	public String toString(){
		return "Carrito de "+cliente.nombre+":\n"+super.toString();
	}
}

class TiendaOnline{

	public static void main(String[] a){

		Scanner sc= new Scanner(System.in);
		System.out.println ("Buen dia ingrese su nombre y email, por favor");
		
		String nombreU = sc.next();
		String email = sc.next();

		Cliente c = new Cliente( nombreU, email);
		CarritoCompras carro = new CarritoCompras(c);

		int cas;	
		
		do{

			System.out.println("\nELIGE DEL MENU: \n1. Agregar al carrito\n2.Quitar del carrito\n3.Mostrar el carrito\n4.Calcular costo total\n5.Salir ");
			cas = sc.nextInt();
			if (cas == 1)
		{ 
			
			System.out.println ("\n¿De que categoria desea comprar? ");
			System.out.println ("Empezamos con sus compras\n" + "En la tienda hay:\n(M) Materiales de escritura -> Plumas, lapices, plumones,etc.\n(H) Herramientas de Computo -> Calculadoras, computadoras, etc\n(P) Papeleria -> Cuadernos, paquetes de hojas");
			
			String opcion = sc.next();
			switch (opcion) {

				case "M" :
					 System.out.println("DE ESCRITURA\n Lapices (a)  Pluma (b)   Marcadores (c) ");
					 String op1 = sc.next();
			    switch (op1){

					 	case "a" :
					 	System.out.println ("LAPICES. Indique el tipo de punta y color\n ");
					 	String tipoP = sc.next();
					 	String colorL = sc.next();

					 	Lapiz p1 = new Lapiz();
					 	p1.nombre = "Lapiz";
					 	p1.precio = 15f;
					 	p1.color = colorL;
					 	p1.incrementarStock (10);
					 	carro.agregarACarrito(p1, p1);
					 	break;

					 	case "b" :
					 	System.out.println("PLUMAS. Indique tipo de punta y color\n");
					 	String tipoPL= sc.next();
					 	String colorPL= sc.next();

					 	Pluma p2 = new Pluma();
					 	p2.nombre = "Pluma";
					 	p2.precio = 10f;
					 	p2.color = colorPL;
					 	p2.incrementarStock(2);
					 	carro.agregarACarrito(p2, p2);
					 	break;

					 	case "c":
					 	System.out.println("MARCADORES. Indique uso (decoracion o resaltado), punta y color");
					 	String usoM = sc.next();
					 	String tipoPM = sc.next();
					 	String colorM = sc.next();

					 	Marcador p3= new Marcador();
					 	p3.nombre = "Marcador";
					 	p3.precio = 20f;
					 	p3.color = colorM;
					 	p3.uso = usoM;

					 	carro.agregarACarrito(p3, p3);
					 	break;

					 	default:
					 	System.out.println ("OPCION INVALIDA");


					 }
				break; 
		        case "H":
		        System.out.println("Herramientas de Computo -> Calculadoras (C) , computadoras (O)");
					 String op2 = sc.next();
			    switch (op2){

					 	case "C" :
					 	System.out.println ("CALCULADORA. Indique la marca\n ");
					 	String marcaC = sc.next();
					 	
					 	Calculadora p4 = new Calculadora();
					 	p4.nombre = "Calculadora";
					 	p4.precio = 500f;
					 	p4.marca = marcaC;
					 	p4.incrementarStock (3);
					 	carro.agregarACarrito(p4, p4);
					 	break;

					 	case "O" :
					 	System.out.println("COMPUTADORAS. Indique la marca y el color\n");
					 	String marcaCo= sc.next();
					 	String colorCo= sc.next();

					 	Computadora p5 = new Computadora();
					 	p5.nombre = "Computadora";
					 	p5.precio = 3600f;
					 	p5.color = colorCo;
					 	p5.SO = marcaCo;
					 	p5.incrementarStock(6);
					 	carro.agregarACarrito(p5, p5);
					 	break;

					 	default:
					 	System.out.println ("OPCION INVALIDA");

				}

				break;
				case "P":
				System.out.println ("Papeleria -> Cuadernos (U), paquetes de hojas (H)");
				String op3 = sc.next();
			    switch (op3){

					 	case "U" :
					 	System.out.println ("CUADERNOS. Indique color, cantidad y tamano (alto y ancho) \n ");
					 	String colorCu = sc.next();
					 	int cantidadH = sc.nextInt();
					 	int anchoLC = sc.nextInt();
					 	int altoLC = sc.nextInt();
					 						 	
					 	Cuaderno p6 = new Cuaderno();
					 	p6.nombre = "Cuaderno";
					 	p6.precio = 80f;
					 	p6.color = colorCu;
					 	p6.cantHojas = cantidadH;
					 	p6.defTamanoPapel (anchoLC, altoLC);
					 	p6.incrementarStock (7);
					 	carro.agregarACarrito(p6, p6);
					 	break;

					 	case "H" :
					 	System.out.println("PAQUETE DE HOJAS.  Indique color, cantidad y tamano (alto y ancho)\n");
					 	String colorH= sc.next();
					 	int cantidadHoj= sc.nextInt();
					 	int anchoH = sc.nextInt();
					 	int altoH = sc.nextInt();
					 	

					 	PaqueteHojas p7 = new PaqueteHojas();
					 	p7.nombre = "Paquete de hojas";
					 	p7.precio = 100f;
					 	p7.color = colorH;
					 	p7.cantHojas = cantidadHoj;
					 	p7.defTamanoPapel (anchoH, altoH);
					 	p7.incrementarStock (5);
					 	carro.agregarACarrito(p7, p7);
					 	break;

					 	default:
					 	System.out.println ("OPCION INVALIDA");

				}
            }

        }

         else if (cas == 2){
        	System.out.println ("¿QUE DESEA QUITAR DEL CARRITO?\n");
        	carro.mostrarCarrito();
        	
        	String obj = sc.next();
        	Producto obj1= 
        	carro.quitardelCarrito(obj);
        }

        else if(cas == 3){
        	System.out.println ("ESTOS SON SUS PRODUCTOS\n");
        	carro.mostrarCarrito();
        }

        else if (cas == 4){
        	carro.calcularCostoCarrito();
        	System.out.println("EL TOTAL DE SU COMPRA ES:" + carro.costoTotal);

        }

		}while(cas != 5);
	}

}
	






