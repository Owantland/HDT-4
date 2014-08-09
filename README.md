Calculadora

import java.util.InputMismatchException;

//****************************************************************
// Autores: Andrea Barrera Carne: 13655 Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 21/7/14
// Nombre de Archivo: Calculadora.java
// Breve Descripcion: Clase que representa una calculadora y hace las operaciones requeridas
//*****************************************************************

public class Calculadora
{
//Atributos
	private Archivo miArchivo;
	private StackVector<Integer> miVector;
	private String datos, simbolo;
	private int dato1 = 0, dato2= 0, resultado= 0;
	private int contador;
	
	//Constructor
	public Calculadora (String texto)
	{
		miArchivo = new Archivo (texto);
		miVector = new StackVector <Integer>();
		datos = miArchivo.leerArchivo();
	}
	
	public int operar()
	{
		String[] elemento = datos.split(" ");
		contador = 0;
		int n = elemento.length;
		int i = 0;
		while (i < n)
		{
			if (contador < 2)
			{
				try
				{
					int dato = Integer.parseInt(elemento[i]);
					miVector.push(dato);
					contador = contador + 1;
				}
				
				catch (InputMismatchException e)
				{
					System.out.println("Orden incorrecto");
					break;
				}
				catch (NumberFormatException e)
				{
					System.out.println("Orden incorrecto");
					break;
				}
			}
			
			else
			{
				try
				{
					simbolo = elemento[i];
					dato1 = miVector.pop();
					dato2 = miVector.pop();
					contador = 1;
					if (simbolo.equals("+"))
					{
						resultado = dato1 + dato2;
						miVector.push(resultado);
					}
					if (simbolo.equals("*"))
					{
						resultado = dato1 * dato2;
						miVector.push(resultado);
					}
					if (simbolo.equals("/"))
					{
						resultado = dato1/dato2;
						miVector.push(resultado);
					}
					if (simbolo.equals("-"))
					{
						resultado = dato1 - dato2;
						miVector.push(resultado);
					}
				}
				
				catch (InputMismatchException e)
				{
					System.out.println("Orden incorrecto");
				}
			}
			i++;
		}
		return resultado;
	}

}
		
		//Tomado a base de lo visto en: 
		//http://stackoverflow.com/questions/24725374/java-postfix-calculator-push-pop-method-with-a-string-array
		//http://stackoverflow.com/questions/7450815/postfix-evaluation-using-stacks
		
		
		
		
Archivo
//****************************************************************
// Autores: Andrea Barrera Carne: 13655 Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 21/7/14
// Nombre de Archivo: Archivo.java
// Breve Descripcion: Clase que se encarga de cargar el archivo de texto para poder usarlo en la calculadora
//*****************************************************************
import java.io.*;
public class Archivo 
{
    //ATRIBUTOS
    private File archivo;
    private BufferedReader br;
    private FileReader fr;

    //Constructor
    //Busca el archivo y prepara un filereader y bufferreader para poder transformarlo a String
    public Archivo(String texto)
    {
            archivo = new File(texto+".txt");
            if(!archivo.exists())
            {
                    System.out.print("El archivo no se encuentra");
            }
            else
            {
                    try
                    {
                            fr = new FileReader(archivo);
                            br = new BufferedReader(fr);
                    }
                    catch (Exception e)
                    {
                            System.out.println(e.getMessage());
                    }
            }

    }

    //Metodo que se encarga de convertir los datos del texto en String
    //Metodo basado en un metodo de Mykong
    //Encontrado en: http://www.mkyong.com/java/how-to-read-file-from-java-bufferedreader-example/
    public String leerArchivo()
    {
            String datos = new String("");
            try
            {
                    String SLine;
                    while((SLine=br.readLine())!=null)
                    {
                            datos = SLine;
                    }
                    fr.close();
            }
            catch (Exception e)
            {
                    System.out.println(e.getMessage());
            }

            return datos;
    }
}


DriverCalculadora
//****************************************************************
// Autores: Andrea Barrera Carne: 13655 Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 21/7/14
// Nombre de Archivo: DriverCalculadora.java
// Breve Descripcion: Driver para la clase calculadora
//*****************************************************************

public class DriverCalculadora
{
	public static void main (String[] args)
	{
		Calculadora miCalculadora = new Calculadora("datos");
		int resultado = miCalculadora.operar();
		System.out.println(resultado + "");
	}
}


Lista

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: Lista.java
// Breve Descripcion: Interface que describe los metodos esperados de una lista
//*****************************************************************

public interface Lista<E> //Tomado del ejemplo subido a Blackboard por Douglas Barrios
{
	
	 public int size();
	   // post: returns number of elements in list

	   public boolean isEmpty();
	   // post: returns true iff list has no elements

	   public void clear();
	   // post: empties list

	   public void addFirst(E value);
	   // post: value is added to beginning of list

	   public void addLast(E value);
	   // post: value is added to end of list

	   public E getFirst();
	   // pre: list is not empty
	   // post: returns first value in list

	   public E getLast();
	   // pre: list is not empty
	   // post: returns last value in list

	   public E removeFirst();
	   // pre: list is not empty
	   // post: removes first value from list

	   public E removeLast();
	   // pre: list is not empty
	   // post: removes last value from list

	   public E remove(E value);
	   // post: removes and returns element equal to value
	   // otherwise returns null

	   public void add(E value);
	   // post: value is added to tail of list

	   public E remove();
	   // pre: list has at least one element
	   // post: removes last value found in list

	   public E get();
	   // pre: list has at least one element
	   // post: returns last value found in list

	   public boolean contains(E value);
	   // pre: value is not null
	   // post: returns true iff list contains an object equal to value

	   public int indexOf(E value);
	   // pre: value is not null
	   // post: returns (0-origin) index of value,
	   // or -1 if value is not found

	   public int lastIndexOf(E value);
	   // pre: value is not null
	   // post: returns (0-origin) index of value,
	   // or -1 if value is not found

	   public E get(int i);
	   // pre: 0 <= i < size()
	   // post: returns object found at that location

	   public E set(int i, E o);
	   // pre: 0 <= i < size()
	   // post: sets ith entry of list to value o;
	   // returns old value

	   public void add(int i, E o);
	   // pre: 0 <= i <= size()
	   // post: adds ith entry of list to value o

	   public E remove(int i);
	   // pre: 0 <= i < size()
	   // post: removes and returns object found at that location

	   //public Iterator<E> iterator();
	   // post: returns an iterator allowing
	   // ordered traversal of elements in list

}



		
