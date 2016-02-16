# archivos
creacion de archivos
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.IO;

namespace archivos
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
            textBox2.Enabled = false;
        }
        TextWriter archivo;
        String ruta, leer;

        private void button1_Click(object sender, EventArgs e)
        {
            if (textBox1.Text != "")
            {

                FolderBrowserDialog fod = new FolderBrowserDialog();
                fod.Description = "Seleccione la ruta del documento";
                fod.RootFolder = Environment.SpecialFolder.Desktop;
                if (fod.ShowDialog() == DialogResult.OK)
                {
                    ruta = fod.SelectedPath;
                    String mensaje;
                    mensaje = richTextBox1.Text;
                    archivo = new StreamWriter(ruta + "\\" + textBox1.Text + ".txt");
                    archivo.Write(mensaje);
                    archivo.Close();
                }
            }
            else MessageBox.Show("NO A ASIGNADO UN NOMBRE ");

            textBox1.Clear();
        }

        private void button2_Click(object sender, EventArgs e)
        {
            richTextBox1.Text = "";

            OpenFileDialog open = new OpenFileDialog();
            open.Filter = " Archivos txt(*.txt)|*.txt";
            open.Title = "Archivos .txt";
            if (open.ShowDialog() == DialogResult.OK)
            {
                leer = open.FileName;
                textBox2.Text = leer;
                StreamReader file = new StreamReader(leer);
                while (file.Peek() != -1)
                {
                    richTextBox1.Text += file.ReadLine() + "\n";
                }
                file.Close();
            }
            open.Dispose();
        }

        private void button3_Click(object sender, EventArgs e)
        {
            textBox2.Text = leer;

            String mensaje;
            mensaje = richTextBox1.Text;
            archivo = new StreamWriter(leer);
            archivo.Write(mensaje);
            archivo.Close();
            MessageBox.Show("SE HAN GUARDADO LOS CAMBIOS");
            richTextBox1.Clear();
            textBox2.Clear();
        }
    }
}
