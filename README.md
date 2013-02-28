Project
=======



#ifdef __APPLE_CC__
#include <GLUT/glut.h>
#else
#include <GL/glut.h>
#endif
#include <cmath>

void init (void){
  glClearColor(0.0,0.0,0.0,0.0);
	glMatrixMode(GL_PROJECTION);
	gluOrtho2D(0.0,400.0,0.0,300.0);
}

void Keyboard (unsigned char key,int x,int y)
{
	switch (key)
	{
	case 'r':
		glClearColor(1.0,0.0,0.0,0.0);
		glutPostRedisplay();
		break;
	case 'g':
		glClearColor(0.0,1.0,0.0,0.0);
		glutPostRedisplay();
		break;
	case 'b':
		glClearColor(0.0,0.0,1.0,0.0);
		glutPostRedisplay();
		break;
	case 'n':
			glClearColor(0.0,0.0,0.0,0.0);
		glutPostRedisplay();
		break;
		case 'w':
			glClearColor(1.0,1.0,1.0,1.0);
		glutPostRedisplay();
		break;
	case 'e':
		exit(0);
		break;
	default:
		break;
	}
}

void myWireSphere(GLfloat radius, int slices, int stacks) {
  glPushMatrix();
  glRotatef(-90.0, 1.0, 0.0, 0.0);
  glutWireSphere(radius, slices, stacks);
  glPopMatrix();
}

static int year = 0, day = 0;
void display() {
  glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
  glPushMatrix();

  
  glColor3f(1.0, 1.0, 0.0);		//ກຳນົດສີດວງຕາເວັນ
  myWireSphere(1.0, 100, 100);	//ກຳນົດຂະໜາດ,ເສັ້ນແວງ,ເສັ້ນຂະໜານຂອງຕະເວັນ

  glRotatef((GLfloat)year, 0.0, 1.0, 0.0);	//ກຳນົດການໝູນຮອບ
  glTranslatef (2.0, 0.0, 0.0);	//ກຳນົດໄລຍະຫ່າງການໜູນຂອງດາວອ້ອມດວງຕາເວັນ
  glRotatef((GLfloat)day, 0.0, 1.0, 0.0);		//ການໜູນອ້ອມຕົວມັນເອງຂອງດາວ
  glColor3f(1.9, 0.5, 0.0);
  myWireSphere(0.4, 15, 15);	 //ກຳນົດຂະໜາດ,ເສັ້ນແວງ,ເສັ້ນຂະໜານຂອງດາວເຄາະ
  
   glRotatef((GLfloat)year, 0.0, 1.0, 0.0);
  glTranslatef (4.0, 0.0, 0.0);
  glRotatef((GLfloat)day, 0.0, 1.0, 0.0);	
  glColor3f(2.0, 0.0, 1.0);
  myWireSphere(0.4, 15, 15);

   glRotatef((GLfloat)year, 0.0, 1.0, 0.0);
  glTranslatef (6.0, 0.0, 0.0);
  glRotatef((GLfloat)day, 0.0, 1.0, 0.0);	
  glColor3f(0.0, 1.0, 1.0);
  myWireSphere(0.4, 15, 15);

   glRotatef((GLfloat)year, 0.0, 1.0, 0.0);
  glTranslatef (5.0, 0.0, 0.0);
  glRotatef((GLfloat)day, 0.0, 1.0, 0.0);	
  glColor3f(0.0, 0.5, 1.9);
  myWireSphere(0.4, 15, 15);

  glColor3f(1, 1, 1);
  glBegin(GL_LINES);
    glVertex3f(0, -0.3, 0);
    glVertex3f(0, 0.3, 0);
  glEnd();

  glPopMatrix();
  glFlush();
  glutSwapBuffers();
}

static GLfloat u = 0.0;                 
static GLfloat du = 0.1;              

void timer(int v) {
  u += du;
  day = (day + 1) % 360;
  year = (year + 2) % 360;
  glLoadIdentity();
  gluLookAt(20*cos(u/8.0)+12,5*sin(u/8.0)+1,10*cos(u/8.0)+2, 0,0,0, 0,1,0);
  glutPostRedisplay();
  glutTimerFunc(1000/30, timer, v);
}


void reshape(GLint w, GLint h) {
  glViewport(0, 0, w, h);
  glMatrixMode(GL_PROJECTION);
  glLoadIdentity();
  gluPerspective(60.0, (GLfloat)w/(GLfloat)h, 1.0, 40.0);
  glMatrixMode(GL_MODELVIEW);
}


int main(int argc, char** argv) {
  glutInit(&argc, argv);
  glutInitDisplayMode (GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
  glutInitWindowSize(800, 600);
  glutCreateWindow("CS8 Group");
  init();
  glutDisplayFunc(display);
  glutKeyboardFunc(Keyboard);
  glutReshapeFunc(reshape);
  glutTimerFunc(100, timer, 0);
  glEnable(GL_DEPTH_TEST);
  glutMainLoop();
}
