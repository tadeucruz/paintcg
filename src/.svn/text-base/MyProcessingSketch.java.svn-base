import java.util.ArrayList;
import java.util.HashSet;

import javax.transaction.xa.Xid;

import processing.core.*;
import interfascia.*;

public class MyProcessingSketch extends PApplet {

	private int controle = -1;
	private ArrayList<Integer> controleXY = new ArrayList<Integer>();
	private int cont = 0;
	private int r=0;

	GUIController c;
	IFButton b1, b2,b3,b4;
	IFLabel l;
	IFTextField t;

	public void setup() {
		size(800, 600);
		background(150);
		// GUI
		c = new GUIController(this);

		b4 = new IFButton("Limpar", 40, 15, 40, 17);
		b1 = new IFButton("DDA", 40, 40, 40, 17);
		b2 = new IFButton("Bres", 40, 65, 40, 17);
		b3 = new IFButton("Bres Circulo", 40, 90, 40, 40);
		t = new IFTextField("Text Field", 70, 140, 40);
		l = new IFLabel("Raio: ", 40, 150);

		b1.addActionListener(this);
		b2.addActionListener(this);
		b3.addActionListener(this);
		b4.addActionListener(this);
		t.addActionListener(this);


		c.add(b1);
		c.add(b2);
		c.add(b3);
		c.add(b4);
		c.add(t);
		c.add(l);

	}

	public void actionPerformed(GUIEvent e) {
		if (e.getSource() == b1) {
			controle = 0; //DDA
			controleXY.clear();
		} else if (e.getSource() == b2) {
			controle = 1; //Bres
			controleXY.clear();
		}
		else if (e.getSource() == b3) {
			controle = 2; //Bres Cric
			controleXY.clear();
		}
		else if (e.getSource() == b4) {
			controleXY.clear();
		}
		else if (e.getSource() == t) {
			r = Integer.parseInt(t.getValue());
			controleXY.clear();
		}
	}

	public void draw() {
		stroke(0);
		if (controle == 0) {// DDA
			if (mousePressed) {
				if (controleXY.size() >= 4) {
					controleXY.clear();
				} else if (!controleXY.contains(mouseX)
						&& !controleXY.contains(mouseX)) {
					controleXY.add(mouseX);
					controleXY.add(mouseY);
					System.out.println("Click Feito");
				}
			}
			if (controleXY.size() == 4) {
				int x1 = controleXY.get(0);
				int y1 = controleXY.get(1);
				int x2 = controleXY.get(2);
				int y2 = controleXY.get(3);
				DDA(x1, y1, x2, y2);
				System.out.println("DDA FEITO");
				controleXY.clear();
			}
		} else if (controle == 1) { //Bres
			if (mousePressed) {
				if (controleXY.size() >= 4) {
					controleXY.clear();
				} else if (!controleXY.contains(mouseX)
						&& !controleXY.contains(mouseX)) {
					controleXY.add(mouseX);
					controleXY.add(mouseY);
					System.out.println("Click Feito");
				}
			}
			if (controleXY.size() == 4) {
				int x1 = controleXY.get(0);
				int y1 = controleXY.get(1);
				int x2 = controleXY.get(2);
				int y2 = controleXY.get(3);
				bres_gen(x1, y1, x2, y2);
				System.out.println("Bres FEITO");
				controleXY.clear();
			}
		}else if (controle == 2) { //Bres Circ
			if (mousePressed) {	
				circBres(mouseX, mouseY, r);
				System.out.println(r);
				System.out.println("Feito Bres Circ");
			}
		}
		
	}

	private void DDA(int x1, int y1, int x2, int y2) {
		int dx, dy, passos, k;
		float x_incr, y_incr, x, y;
		dx = x2 - x1;
		dy = y2 - y1;
		if (abs(dx) > abs(dy)) {
			passos = abs(dx);
		} else {
			passos = abs(dy);
		}
		x_incr = (float) dx / passos;
		y_incr = (float) dy / passos;
		x = x1;
		y = y1;
		point(x, y);
		for (int i = 0; i <= passos; i++) {
			x = x + x_incr;
			y = y + y_incr;
			point(x, y);
		}
	}

	public void bres_gen(int x1, int y1, int x2, int y2) {
		int dx, dy, x, y, i, const1, const2, p, incrx, incry;
		dx = x2 - x1;
		dy = y2 - y1;
		if (dx >= 0)
			incrx = 1;
		else {
			incrx = -1;
			dx = -dx;
		}
		if (dy >= 0)
			incry = 1;
		else {
			incry = -1;
			dy = -dy;
		}
		x = x1;
		y = y1;
		point(x, y);
		if (dy < dx) {
			p = 2 * dy - dx;
			const1 = 2 * dy;
			const2 = 2 * (dy - dx);
			for (i = 0; i < dx; i++) {
				x += incrx;
				if (p < 0)
					p += const1;
				else {
					y += incry;
					p += const2;
				}
				point(x, y);
			}
		} else {
			p = 2 * dx - dy;
			const1 = 2 * dx;
			const2 = 2 * (dx - dy);
			for (i = 0; i < dy; i++) {
				y += incry;
				if (p < 0)
					p += const1;
				else {
					x += incrx;
					p += const2;
				}
				point(x, y);
			}
		}
	}
	
	public void circBres(int xc, int yc,int r){
		int x,y,p;
		x = 0;
		y=r;
		p = 3-2*r;
		while (x<y) {
			if (p <0) { 
				p = p+4*x+6;
			}else { 
				p=p+4*(x-y)+10;
				y=y-1;
			}
			x=x+1;
			plot_circle_points(xc, yc, x, y);
		}
	}
	
	public void plot_circle_points(int xc, int yc,int x, int y){
		point(xc+x, yc+y);
		point(xc+x, yc+y);
		point(xc-x, yc+y);
		point(xc+x, yc-y);
		point(xc-x, yc-y);
		point(xc+y, yc+x);
		point(xc-y, yc+x);
		point(xc+y, yc-x);
		point(xc-y, yc-x);
	}

}
