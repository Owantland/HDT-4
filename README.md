AbstractList

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: AbstractList.java
// Breve Descripcion: clase abtracta de las listas para metodos en comun
//*****************************************************************
public abstract class AbstractList<E> implements List<E>
{
   public AbstractList()
   // post: does nothing
   {
   }

   public boolean isEmpty()
   // post: returns true iff list has no elements
   {
      return size() == 0;
   }
  
  public boolean contains(E value)
  // pre: value is not null
  // post: returns true iff list contains an object equal to value
  {
	return -1 != indexOf(value);
  }
}

CircularList
//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: CircularList.java
// Breve Descripcion: clase de tipo lista que puede al terminar un lista se
//direcciona al principio porque apunta siempre al final para dar vueltas
//*****************************************************************
public class CircularList<E> extends AbstractList<E>{


protected Node<E> tail; 
protected int count;

public CircularList()
// pre: constructs a new circular list
{
   tail = null;
   count = 0;
}

public void addFirst(E value)
// pre: value non-null
// post: adds element to head of list
{
   Node<E> temp = new Node<E>(value);
   if (tail == null) { // first value added
       tail = temp;
       tail.setNext(tail);
   } else { // element exists in list
       temp.setNext(tail.next());
       tail.setNext(temp);
   }
   count++;
}


public void addLast(E value)
// pre: value non-null
// post: adds element to tail of list
{
   // new entry:
   addFirst(value);
   tail = tail.next();
}


// lo dificil es quitar el elemento de la cola

public E removeLast()
// pre: !isEmpty()
// post: returns and removes value from tail of list
{
   Node<E> finger = tail;
   while (finger.next() != tail) {
       finger = finger.next();
   }
   // finger now points to second-to-last value
   Node<E> temp = tail;
   if (finger == tail)
   {
       tail = null;
   } else {
       finger.setNext(tail.next());
       tail = finger;
   }
   count--;
   return temp.value();
}

   

    @Override
    public void clear() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E getFirst() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E getLast() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E removeFirst() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E remove(E value) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public void add(E value) {
        // new entry:
        addFirst(value);
        tail = tail.next();
    }

    @Override
    public E remove() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E get() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public int indexOf(E value) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public int lastIndexOf(E value) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E get(int i) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E set(int i, E o) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public void add(int i, E o) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E remove(int i) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public int size() {
        return count;
    }

}

DoubleLinkedList

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: DoubleLinkedList.java
// Breve Descripcion: Es la lista double que recorre la lista de arriba para abajo
//y de vice versa
//*****************************************************************
public class DoubleLinkedList<E> extends AbstractList<E>{
protected int count;
protected DoubleLinkedNode<E> head;
protected DoubleLinkedNode<E> tail;

public DoubleLinkedList()
// post: constructs an empty list
{
   head = null;
   tail = null;
   count = 0;
}


public void addFirst(E value)
// pre: value is not null
// post: adds element to head of list
{
   // construct a new element, making it head
   head = new DoubleLinkedNode<E>(value, head, null);
   // fix tail, if necessary
   if (tail == null) tail = head;
   count++;
}


public void addLast(E value)
// pre: value is not null
// post: adds new value to tail of list
{
   // construct new element
   tail = new DoubleLinkedNode<E>(value, null, tail);
   // fix up head
   if (head == null) head = tail;
   count++;
}


public E removeLast()
// pre: list is not empty
// post: removes value from tail of list
{
   DoubleLinkedNode<E> temp = tail;
   tail = tail.previous();
   if (tail == null) {
       head = null;
   } else {
       tail.setNext(null);
   }
   count--;
   return temp.value();
}

    @Override
    public int size() {
        return count;
    }

    @Override
    public void clear() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E getFirst() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E getLast() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E removeFirst() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E remove(E value) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public void add(E value) {
         // construct new element
        tail = new DoubleLinkedNode<E>(value, null, tail);
        // fix up head
        if (head == null) head = tail;
        count++;
    }

    @Override
    public E remove() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E get() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public int indexOf(E value) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public int lastIndexOf(E value) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E get(int i) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E set(int i, E o) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public void add(int i, E o) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E remove(int i) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }
}

DoubleLinkedNode
//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: DoubleLinkedNode.java
// Breve Descripcion: clase auxiliar de la clase DoubleLinkedList para poder
//recorrer la lista
//*****************************************************************
public class DoubleLinkedNode<E>
{
protected E data;
protected DoubleLinkedNode<E> nextElement;
protected DoubleLinkedNode<E> previousElement;

public DoubleLinkedNode(E v, DoubleLinkedNode<E> next, DoubleLinkedNode<E> previous)
{
    data = v;
    nextElement = next;
    if (nextElement != null)
        nextElement.previousElement = this;
    previousElement = previous;
    if (previousElement != null)
        previousElement.nextElement = this;
}

public DoubleLinkedNode(E v)
// post: constructs a single element
{
    this(v,null,null);
}

   public DoubleLinkedNode<E> next()
   // post: returns reference to next value in list
   {
      return nextElement;
   }
   
   public DoubleLinkedNode<E> previous()
   // post: returns reference to next value in list
   {
      return previousElement;
   }

   public void setNext(DoubleLinkedNode<E> next)
   // post: sets reference to new next value
   {
      nextElement = next;
   }

   public E value()
   // post: returns value associated with this element
   {
      return data;
   }

   public void setValue(E value)
   // post: sets value associated with this element
   {
      data = value;
   }

}

DriverCalculadora
//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: DriverCalculadora.java
// Breve Descripcion: Driver para la clase calculadora
//*****************************************************************

import java.util.Scanner; 

public class DriverCalculadora
{
	public static void main (String[] args)
	{       
                //Pre: se ingresa la opcion deseada y el el nombre del archivo donde esta la operacion
                //deseada a ejecutar
                //Post: imprime el resultado
            
                //hace ingreso de la opcion deseada
                String opcion1;
                Scanner input = new Scanner (System.in);
                System.out.print("Que metodo desea usar?");
                System.out.print("1. ArrayList");
                System.out.print("2. Vector");
                System.out.print("3.Lista (cualquier numero o letra para escoger opcion)");
                opcion1 = input.next();
		input.nextLine();
                //se instancia la calculadora
		Calculadora miCalculadora = new Calculadora("datos", opcion1);
                //se inicia el calculo
		int resultado = miCalculadora.operar();
                //se imprime el resultado
		System.out.println(resultado + "");
	}
}

Lista
//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: List.java
// Breve Descripcion: interface con las que se guiara a las clases list
//*****************************************************************
public interface List<E> 
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


Node

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: Node.java
// Breve Descripcion: clase auxiliar a la clase Singlelinked
//*****************************************************************
public class Node<E>
{
   protected E data; // value stored in this element
   protected Node<E> nextElement; // ref to next

   public Node(E v, Node<E> next)
   // pre: v is a value, next is a reference to 
   //      remainder of list
   // post: an element is constructed as the new 
   //      head of list
   {
       data = v;
       nextElement = next;
   }

   public Node(E v)
   // post: constructs a new tail of a list with value v
   {
      this(v,null);
   }

   public Node<E> next()
   // post: returns reference to next value in list
   {
      return nextElement;
   }

   public void setNext(Node<E> next)
   // post: sets reference to new next value
   {
      nextElement = next;
   }

   public E value()
   // post: returns value associated with this element
   {
      return data;
   }

   public void setValue(E value)
   // post: sets value associated with this element
   {
      data = value;
   }
}

SingleLinkedList

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: SingleLinkedList.java
// Breve Descripcion: es la clase List que trabaja de solo una direccion
//*****************************************************************
public class SingleLinkedList<E> extends AbstractList<E>
{

   protected int count; // list size
   protected Node<E> head; // ref. to first element

   public SingleLinkedList()
   // post: generates an empty list
   {
      head = null;
      count = 0;
   }
   
   public int size()
   // post: returns number of elements in list
  {
    return count;
  }
  
  public void addLast(E value)
  // post: value is added to beginning of list
  {
     // note order that things happen:
     // head is parameter, then assigned
     head = new Node<E>(value, head);
     count++;
  }
  
  public E removeLast()
  // pre: list is not empty
  // post: removes and returns value from beginning of list
 {
     Node<E> temp = head;
     head = head.next(); // move head down list
     count--;
     return temp.value();
  }
  
  public E removeFirst() {
   Node<E> temp = head;
   
   temp = temp.next();
   count--;
   
   return temp.value();
  }
  
  public E getFirst()
  // pre: list is not empty
  // post: returns first value in list
  {
      return head.value();
  }
  
  public void addFirst(E value)
  // post: adds value to end of list
  {
      // location for new value
      Node<E> temp = new Node<E>(value,null);
      if (head != null)
     {
         // pointer to possible tail
         Node<E> finger = head;
         while (finger.next() != null)
         {
                finger = finger.next();
         }
		 
         finger.setNext(temp);
      } else head = temp;
	  
	  count++;
	  
   }
   
   
   public boolean contains(E value)
   // pre: value is not null
   // post: returns true iff value is found in list
  {
      Node<E> finger = head;
	  
      while (finger != null &&
             !finger.value().equals(value))
     {
          finger = finger.next();
      }
      return finger != null;
   }

    @Override
    public void clear() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E getLast() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    

    @Override
    public E remove(E value) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public void add(E value) {
         // location for new value
      Node<E> temp = new Node<E>(value,null);
      if (head != null)
     {
         // pointer to possible tail
         Node<E> finger = head;
         while (finger.next() != null)
         {
                finger = finger.next();
         }
		 
         finger.setNext(temp);
      } else head = temp;
	  
	  count++;
    }

    @Override
    public E remove() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E get() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public int indexOf(E value) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public int lastIndexOf(E value) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E get(int i) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E set(int i, E o) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public void add(int i, E o) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public E remove(int i) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }
   
}

Stack

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: Stack.java
// Breve Descripcion: es la interface con la que se trabajaran las Stack
//*****************************************************************
public interface Stack<E>
{
   public void push(E item);
   // post: el item es agregado al stack. Sera
   //       el proximo en salir

   public E pop();
   // pre: stack no esta vacio
   // post: el elemento ingresado mas recientemente
   //       es retirado.

   public E peek();
   //pre: stack no esta vacio
   //post: el valor mas reciente es retornado
   //      pero no es sacado del stack.

   public boolean empty();
   //post: regresa true si el stack esta vacio

   public int size();
   //post: regresa la cantidad de elementos
   //      en el stack
}

StackArrayList

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: StackArrayList.java
// Breve Descripcion: es la clase Stack que trabaja con un Array
//*****************************************************************
import java.util.ArrayList;

public class StackArrayList<E>
 extends AbstractStack<E>
{
	protected ArrayList<E> data;

	public StackArrayList()
	// post: constructs a new, empty stack
	{
		data = new ArrayList<E>();
	}

	public void push(E item)
	// post: the value is added to the stack
	//          will be popped next if no intervening push
	{
		data.add(item);
	}

	public E pop()
	// pre: stack is not empty
	// post: most recently pushed item is removed and returned
	{
		return data.remove(size()-1);
	}

	public E peek()
	// pre: stack is not empty
	// post: top value (next to be popped) is returned
	{
		return data.get(size() - 1);
	}
	
	public int size()
	// post: returns the number of elements in the stack
	{
		return data.size();
	}
  
	
}

StackFactory

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: StackFactory.java
// Breve Descripcion: ayuda a la eleccion de cualquier elemento del factory para
//utilizar en la calculadora
//*****************************************************************
import java.util.Scanner;
import javax.swing.JOptionPane;

class StackFactory<E> {
//selecciona la implementacion a utilizar para un stack
//se utiliza el patron Factory
   public Stack<E> getStack(String entry) {
    // seleccion de la implementacion a utilizar:
	if (entry.equals("1"))
      return new StackArrayList<E>(); //regresa ArrayList
        else if (entry.equals("2"))
      return new StackVector<E>(); //regresa Vector
        else 
      return new StackList<E>(); //se va a StackList

   }
}

StackList

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: StackFactory.java
// Breve Descripcion: ayuda a la eleccion de cualquier elemento del factory para
//utilizar en la calculadora
//*****************************************************************
import java.util.Scanner;
import javax.swing.JOptionPane;

class StackFactory<E> {
//selecciona la implementacion a utilizar para un stack
//se utiliza el patron Factory
   public Stack<E> getStack(String entry) {
    // seleccion de la implementacion a utilizar:
	if (entry.equals("1"))
      return new StackArrayList<E>(); //regresa ArrayList
        else if (entry.equals("2"))
      return new StackVector<E>(); //regresa Vector
        else 
      return new StackList<E>(); //se va a StackList

   }
}

StackVEctor

//****************************************************************
// Autores: Otto Wantland Carne: 13663 Diego Rodriguez Carne: 13111
// Seccion: 20
//Fecha 31/7/14
// Nombre de Archivo: StackVector.java
// Breve Descripcion: Es la clase Stack que trabaja con vectores
//*****************************************************************
import java.util.Vector;

public class StackVector<E>
 extends AbstractStack<E>
{
	protected Vector<E> data;

	public StackVector()
	// post: constructs a new, empty stack
	{
		data = new Vector<E>();
	}

	public void push(E item)
	// post: the value is added to the stack
	//          will be popped next if no intervening push
	{
		data.add(item);
	}

	public E pop()
	// pre: stack is not empty
	// post: most recently pushed item is removed and returned
	{
		return data.remove(size()-1);
	}

	public E peek()
	// pre: stack is not empty
	// post: top value (next to be popped) is returned
	{
		return data.get(size() - 1);
	}
	
	public int size()
	// post: returns the number of elements in the stack
	{
		return data.size();
	}
  
	
}
