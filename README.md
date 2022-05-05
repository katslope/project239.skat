# типовая задача №4

Лицеистка 10-3 класса, Смуглина Екатерина

## Описание

На плоскости задано множество точек, и множество окружностей. Множество точек образует все возможные прямые, которые могут быть построены парами точек множества. Найти такую прямую (и такие две точки, через которые она проходит) и такую окружность, что эта прямая пересекает указанную окружность, и при этом длина отрезка прямой, находящейся внутри окружности, максимальна. В качестве ответа: выделить найденные две точки, выделить найденную окружность, нарисовать прямую, которая через них проходит, а также выделить на этой прямой отрезок между двумя найденными точками пересечения.

package com.company;
import java.io.PrintStream;
import java.util.Scanner;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.awt.Graphics;
import javax.swing.JFrame;
class Tchk { 
   public int COx;
   public int COy;
   public Tchk (int a, int b) {
       COx = a;
       COy = b;
   }
   public static Pr makePryamaya(Tchk m, Tchk n) { 
       int a,b,c,d;
       a = m.COx;
       b = m.COy;
       c = n.COx;
       d = n.COy;
       return new Pr (b-d, c-a, a*d-b*c);
   }
   public int getX() {
       return COx;
   }
   public int getY() {
       return COy;
   }
}
class Pr {      
   public int A;
   public int B;
   public int C;
   public Pr (int a, int b, int c) {
       A = a;
       B = b;
       C = c;
   }
   public static double distToPoint(Pr m, int x, int y) {  
       int a,b,c;
       double o,p;
       a = m.A;
       b = m.B;
       c = m.C;
       o = (double)a;
       p = (double)b;
       return Math.abs(a*x+b*y+c)/Math.sqrt(o*o+p*p);
   }
}
public class Main {
   public static int Maxcount = 1000; 
   public static int BTchk = 0;      
   public static MyJFrame frame;     
   public static MyJFrame button;
   public static Tchk [] q = new Tchk[Maxcount];  
   public static Scanner in = new Scanner(System.in);
   public static PrintStream out = System.out;
   static class MyJFrame extends JFrame implements MouseListener {
       int radius;      
       int first = 0; 
       int second = 0;    
       int Count = 0; 
       int indicator = 0; 
       public void paint(Graphics g) {
           g.clearRect(0, 0, 1600, 900); 
           for (int i = 0; i < BTchk; i++)
           {
               g.drawOval((int) q[i].getX() - 2, (int) q[i].getY() - 2, 2, 2); 
               g.drawOval((int) q[i].getX() - 2, (int) q[i].getY() - 2, 1, 1);            }
           if (Count >= 2) { // если точек хотя бы две
                   radius = (int) Math.sqrt((q[1].COx - q[0].COx) * (q[1].COx - q[0].COx) + (q[1].COy - q[0].COy) * (q[1].COy - q[0].COy));  
               g.drawOval(q[0].COx - radius, q[0].COy - radius, 2 * radius, 2 * radius); 
               if (indicator == 1) {     
                   if (q[first].COx == q[second].COx)
                       g.drawLine(q[second].COx, 0,q[second].COx, 900); 
                   else
                   g.drawLine(0,(q[first].COx*q[second].COy-q[first].COy*q[second].COx)/(q[first].COx-q[second].COx), 1600,(q[first].COx*q[second].COy-q[first].COy*q[second].COx-1600*(q[second].COy-q[first].COy))/(q[first].COx-q[second].COx) ); 
               }
           }

       }
       public void solve () {
           Pr h; 
