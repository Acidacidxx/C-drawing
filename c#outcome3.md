# C-drawing
This is a list of code made by Acidacidxx 


using System;

using System.Collections.Generic;

using System.ComponentModel;

using System.Data;

using System.Drawing;

using System.Linq;

using System.Text;

using System.Threading.Tasks;

using System.Windows.Forms;

using System.Drawing.Drawing2D;

 

 

//desiner name:16SDxuan

//design
date:2018-5-28

//This program has
several functions such as drawing different shapes, curve and straight line.And
it also can use eraser or clear the screen. In addition, save and open file are
available.If the user has problems using this program, the HELP option is on
the menu on the top of the interface, there are text and a video help for users
to choose.

namespace WindowsFormsApplication1

{

    public partial class Form1 : Form

    {

        //declare
a startpoint and a endpoint

        Point startPt, endPt;

        //declare
a graphic

        Graphics g;

        //declare
a bool variable to not draw in the beginning

        bool down = false;

        //declare
a variable named type to control functions

        int type;

        //declare
a image to draw

        Image im;

        //declare
a pen

        Pen pen = new Pen(Color.Black, 5);

        //declare
a variable named color to store a color user choose

        Color color;

        //declare
a list

        List<Point> plist = new List<Point>();

 

        //this
form load has declared a bitmap that can draw and a graphic

        private void Form1_Load(object sender, EventArgs e)

        {

            //delcared
a bitmap to draw

            im = new Bitmap(paintpage.Width, paintpage.Height);

            //declared
a graphic

            g = Graphics.FromImage(im);

        }

 

        public Form1()

        {

            InitializeComponent();

        }

        //this
event has described when the mouse is down what will happen

        private void pictureBox7_MouseDown(object sender, MouseEventArgs e)

        {

            //explain
the startpoint and endpoint

            startPt.X = e.X;

            startPt.Y = e.Y;

            //the
playlist will be cleared

            plist.Clear();

            plist.Add(e.Location);

        }

        //this
event has described when the mouse is up what will happen in the program

        private void pictureBox7_MouseUp(object sender, MouseEventArgs e)

        {

            //declared
a brush and its color was already set in the beginning 

            SolidBrush brush = new SolidBrush(colorDialog1.Color);

            endPt.X = e.X;

            endPt.Y = e.Y;

            //this
loop statement is to choose what funtion will be used and drawed on the page

            //this
loop will be activated only if the down is true and the user licked left mouse
to draw

            if (down==true && e.Button == MouseButtons.Left)

            {

                //pen
color is set to black

                color = colorDialog1.Color;

 

                //this
loop is to switch what funtion will be used ,different type will have different
funtion

                switch (type)

                {

                    //case
1 is to draw a straight line

                    case 1:

                        

                        g.DrawLine(pen,
startPt, endPt);

                        break;

                }

                //this
if loop is to draw when the fillornot check box is checked 

                if (fillornot.Checked)

                {

                    //this
if is to draw a rectangle

                    if (type == 4)

                    {

                        //following statement is to choose where the pen is
landed in the beginning 

                        //in the top right coner

                        if (endPt.X -
startPt.X < 0 && endPt.Y - startPt.Y > 0)

                            g.FillRectangle(brush,
endPt.X, startPt.Y, Math.Abs(endPt.X
- startPt.X), Math.Abs(endPt.Y -
startPt.Y));

                        //in the top left corner

                        else if (endPt.X -
startPt.X > 0 && endPt.Y - startPt.Y < 0)

                            g.FillRectangle(brush,
startPt.X, endPt.Y, Math.Abs(endPt.X
- startPt.X), Math.Abs(endPt.Y -
startPt.Y));

                        else if (endPt.X -
startPt.X < 0 && endPt.Y - startPt.Y < 0)

                            g.FillRectangle(brush,
endPt.X, endPt.Y, Math.Abs(endPt.X
- startPt.X), Math.Abs(endPt.Y -
startPt.Y));

                        else
g.FillRectangle(brush, startPt.X, startPt.Y, Math.Abs(endPt.X - startPt.X), Math.Abs(endPt.Y - startPt.Y));

                    }

                    //this
if loop is to draw a triangle

                    else if (type == 5)

                    {

                        //the followint statement is to determine where the pen
has landed in the beginning 

                        Point a = new Point(startPt.X,
endPt.Y);

                        Point b = new Point(startPt.X + (endPt.X
- startPt.X) / 2, startPt.Y);

                        Point c = new Point(endPt.X, endPt.Y);

                        Point[] array = { a, b, c
};

                        g.FillPolygon(brush,
array);

                    }

                    //this
if loop is used to draw a circle

                    else if (type == 6)

                        g.FillEllipse(brush,
startPt.X, startPt.Y, (endPt.X - startPt.X), (endPt.Y - startPt.Y));//as same as the Rectangle

                }

                //this
else loop is to draw when the fillornot checkbox is not checked

                else

                {

                    //this
if is to draw a rectangle

                    if (type == 4)

                    {

                        //following statement is to choose where the pen is
landed in the beginning 

                        //in the top right coner

                        if (endPt.X -
startPt.X < 0 && endPt.Y - startPt.Y > 0)

                            g.DrawRectangle(pen,
endPt.X, startPt.Y, Math.Abs(endPt.X
- startPt.X), Math.Abs(endPt.Y -
startPt.Y));

                        else if (endPt.X -
startPt.X > 0 && endPt.Y - startPt.Y < 0)

                            g.DrawRectangle(pen,
startPt.X, endPt.Y, Math.Abs(endPt.X
- startPt.X), Math.Abs(endPt.Y -
startPt.Y));

                        else if (endPt.X -
startPt.X < 0 && endPt.Y - startPt.Y < 0)

                            g.DrawRectangle(pen,
endPt.X, endPt.Y, Math.Abs(endPt.X
- startPt.X), Math.Abs(endPt.Y -
startPt.Y));

                        else g.DrawRectangle(pen, startPt.X, startPt.Y, Math.Abs(endPt.X -
startPt.X), Math.Abs(endPt.Y -
startPt.Y));

                    }

                    //this
if loop is to draw a triangle

                    else if (type == 5)

                    {

                        //the followint statement is to determine where the pen
has landed in the beginning 

                        Point a = new Point(startPt.X,
endPt.Y);

                        Point b = new Point(startPt.X + (endPt.X
- startPt.X) / 2, startPt.Y);

                        Point c = new Point(endPt.X, endPt.Y);

                        Point[] array = { a, b, c
};

                        g.DrawPolygon(pen,
array);

                    }

                    //this
if loop is used to draw a circle

                    else if (type == 6)

                      

                    g.DrawEllipse(pen,
startPt.X, startPt.Y, (endPt.X - startPt.X), (endPt.Y - startPt.Y));//as same as the Rectangle

                }

 

                pictureBox1.BackgroundImage = im;

                pictureBox1.Refresh();

            }

        }

        //this
event is to draw a curve line and use eraser

        private void pictureBox7_MouseMove(object sender, MouseEventArgs e)

        {

            //this
if loop will be activated only if the down is true and the user use left mouse
to click

            if (down==true && e.Button == MouseButtons.Left)

            {

                //this
if is to draw a curve line

                if (type == 2)

                {

                    color = colorDialog1.Color;

                    endPt.X = e.X;

                    endPt.Y = e.Y;

                    plist.Add(e.Location);

                    this.Refresh();

                    pen.StartCap = LineCap.Round;

                    pen.EndCap = LineCap.Round;

                    g.DrawCurve(pen,
plist.ToArray());

                }

                //this
if is to use the eraser

                if (type == 3)

                {

                    //the
pen color has been set to white

                   pen.Color = Color.White;

                   

                    endPt.X = e.X;

                    endPt.Y = e.Y;

                    plist.Add(e.Location);

                    this.Refresh();

                    pen.StartCap = LineCap.Round;

                    pen.EndCap = LineCap.Round;

                    g.DrawCurve(pen,
plist.ToArray());

                }

 

 

            }

            paintpage.BackgroundImage = im;

            paintpage.Refresh();

        }

 

        //this
button is for user to click to draw a straight line

        private void button2_Click(object sender, EventArgs e)

        {

            down = true;

            type = 1;

        }

        //this
button is for user to click to draw a curve line

        private void button1_Click(object sender, EventArgs e)

        {

            down = true;

            type = 2;

        }

        //this
button is for user to click to draw a rectangle

        private void button3_Click(object sender, EventArgs e)

        {

            down = true;

            type = 4;

        }

        //this
button is for user to click to draw a triangle

        private void button4_Click(object sender, EventArgs e)

        {

            down = true;

            type = 5;

        }

        //this
button is for user to click to use eraser

        private void button6_Click(object sender, EventArgs e)

        {

            down = true;

            type = 3;

        }

        //this
button is for user to click to stop drawing

        private void button7_Click(object sender, EventArgs e)

        {

            down = false;

        }

        //this
button is for user to click to choose a color they'd like to use

        private void pictureBox6_Click(object sender, EventArgs e)

        {

            //the
color choosing window will show

            colorDialog1.ShowDialog();

            crtclr.BackColor =
colorDialog1.Color;

            //the
pen color will be changed to whatever the user has choosen

            pen.Color = colorDialog1.Color;

        }

        //this
button is for user to adjust the size of pen and eraser

        private void trackBar1_Scroll(object sender, EventArgs e)

        {

            pen.Width = changesize.Value;

            //and
lable15 will show the current size of pen or eraser

            label5.Text = Convert.ToString(changesize.Value);

            

        }

 

        //this
button is for user to click to use eraser

        private void button5_Click(object sender, EventArgs e)

        {

            down = true;

            type = 6;

        }

        //this
button is for user to open a new picture they'd like to continue to draw

        private void openToolStripMenuItem_Click(object sender, EventArgs e)

        {

            OpenFileDialog OFD = new OpenFileDialog();

            if (OFD.ShowDialog() == DialogResult.OK)

            {

                string file = OFD.FileName;

                paintpage.BackgroundImage = Image.FromFile(file);

                paintpage.BackgroundImageLayout
= ImageLayout.Zoom;

                im = Image.FromFile(file);

                g = Graphics.FromImage(im);

            }

        }

        //this
button is for user to show the the information about the producer

        private void producersInfoToolStripMenuItem_Click(object sender, EventArgs e)

        {

            MessageBox.Show(" Zhao Xuan
\r\n 16SD \r\n SCN:187115477 ");

 

        }

 

        private void helpToolStripMenuItem1_Click(object sender, EventArgs e)

        {

            

        }

        //this
button is for user to click to change the pen color to yellow

        private void label9_Click(object sender, EventArgs e)

        {

            pen.Color = clryellow.BackColor;

            colorDialog1.Color = clryellow.BackColor;

            crtclr.BackColor = pen.Color;

        }

        //this
button is for user to click to change the pen color to red

        private void label11_Click(object sender, EventArgs e)

        {

            pen.Color = clrred.BackColor;

            colorDialog1.Color =
clrred.BackColor;

            crtclr.BackColor = pen.Color;

        }

        //this
button is for user to click to change the pen color to green

        private void label7_Click(object sender, EventArgs e)

        {

            pen.Color = clrgrn.BackColor;

            colorDialog1.Color =
clrgrn.BackColor;

            crtclr.BackColor = pen.Color;

        }

        //this
button is for user to click to change the pen color to blue

        private void label8_Click(object sender, EventArgs e)

        {

            pen.Color = clrblue.BackColor;

            colorDialog1.Color =
clrblue.BackColor;

            crtclr.BackColor = pen.Color;

 

        }

 

        private void checkBox1_CheckedChanged(object sender, EventArgs e)

        {

 

        }

        //this
button is for user to click to clear the draw page to start over

        private void button8_Click(object sender, EventArgs e)

        {

            paintpage.BackColor = Color.White;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        

            paintpage.BackgroundImage = null;

            paintpage.Refresh();

            g.Clear(Color.White);

        }

        //this
button is for user to click to get video help

        private void videoHelpToolStripMenuItem_Click(object sender, EventArgs e)

        {

            Form11 frm11 = new Form11();

            this.Hide();

            frm11.ShowDialog(this);

        }

        //this
button is for user to click to get a text help from the producer

        private void textHelpToolStripMenuItem_Click(object sender, EventArgs e)

        {

            MessageBox.Show("[1]Click the
curve button in the draw options to draw a curve line \r\n [2]Click the Line
button in the draw options to draw a straight line \r\n [3]Click the Rectangle
button in the draw options to draw a Rectangle \r\n [4]Click the Triangle button
in the draw options to draw a triangle \r\n [5]Click the Ellipes button in the
draw options to draw a Ellipes \r\n [6]Check the fill checkbox to draw filled
pictures \r\n [7]Click the Eraser button in the Options section to use a eraser
\r\n [8]Click the cancle button in the Options section to take a step back \r\n
[9]Click the clear button in the Options section to clear the draw section \r\n
[10]Drag the track bar to adjust the size of pen and eraser \r\n [11]Click the
picturebox to choose other color you want to use \r\n [12]Click four color
block to choose color we placed for you \r\n");

        }

        //this
button is for user to click to save the picture they have drawed to their
computer

        private void saveToolStripMenuItem_Click(object sender, EventArgs e)

        {

            SaveFileDialog SFD = new SaveFileDialog();

            SFD.Filter = "画图（*.bmp;*.dib)|*.bmp|GIF|*.gif|PNG(*.Png)|*.Png";

            if (SFD.ShowDialog() == DialogResult.OK)

            {

                string file = SFD.FileName;

                Bitmap bmp = new Bitmap(paintpage.BackgroundImage);

                bmp.Save(file);

            }

        }

 

 

        

    }

}





































































































































































































































































































































































































































































































































































































































































































