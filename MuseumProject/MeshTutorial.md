# How to render your mesh for rviz
This tutorial is about how to visualize our fingertip model in rviz and make it look smoother.


## 1.from Solidworks19 to urdf  
First of all, you need to generate a `.urdf` file for rviz visulization. 
Luckily, if you have a solidworks model, you can find a open-source plugin which can help you complete this.
- Install Solidworks 2019-2020
- Install [sw_urdf_exporter](http://wiki.ros.org/sw_urdf_exporter)
- Set the axis and coordinate for each single unit
- Generate your own model.


## 2.Visualize it in rviz



## 3. Make the mesh smoother
- configure OpenGL  
    1. Download openGL  
    
            sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
            sudo apt-get update
            sudo apt-get upgrade
            sudo apt-get install cmake libx11-dev xorg-dev libglu1-mesa-dev freeglut3-dev libglew1.5 libglew1.5-dev libglu1-mesa libglu1-mesa-dev libgl1-mesa-glx libgl1-mesa-dev libglfw3-dev libglfw3
     2. make a new file to check openGL
    
            mkdir testgl
            cd testgl
            gedit test.c
        
     3. copy the following code into your `test.c`  


    ```c++
        #include <GL/glut.h>
        void init(void)
        {
            glClearColor(0.0, 0.0, 0.0, 0.0);
            glMatrixMode(GL_PROJECTION);
            glOrtho(-5, 5, -5, 5, 5, 15);
            glMatrixMode(GL_MODELVIEW);
            gluLookAt(0, 0, 10, 0, 0, 0, 0, 1, 0);

            return;
        }

        void display(void)
        {
            glClear(GL_COLOR_BUFFER_BIT);
            glColor3f(1.0, 0, 0);
            glutWireTeapot(3);
            glFlush();

            return;
        }

        int main(int argc, char *argv[])
        {
            glutInit(&argc, argv);
            glutInitDisplayMode(GLUT_RGB | GLUT_SINGLE);
            glutInitWindowPosition(0, 0);
            glutInitWindowSize(300, 300);
            glutCreateWindow("OpenGL 3D View");
            init();
            glutDisplayFunc(display);
            glutMainLoop();

            return 0;
        }  
    ```
        4. Compile your program and run it.
        
            gcc -o test test.c -lGL -lGLU -lglut
            ./test
