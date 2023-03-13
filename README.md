# Belinsky
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Data.SqlClient;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace ФИЛИАЛ
{
    public partial class Авторизация : Form
    {
        public Авторизация()
        {
            InitializeComponent();
        }

        private void woiti_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection("Data Source=QWE-200123;Initial Catalog=Филиал;Integrated Security=True");
            SqlDataAdapter sda = new SqlDataAdapter("Select* From Преподаватели where Код= '" + login.Text + "' and Пароль = '" + parol.Text + "'", con);
            DataTable dt = new DataTable();
            sda.Fill(dt);
            if (textBox4.Text == this.Text)
                MessageBox.Show("Добро пожаловать " + dt.Rows[0][1].ToString());
            if (textBox4.Text != this.Text)
                MessageBox.Show("Код введен не верно!");
            else
            if (dt.Rows.Count == 1)
            {
                Главная form3 = new Главная(dt.Rows[0][1].ToString());
                form3.Show();
                this.Hide();
            }
            

        }

        private void button1_Click(object sender, EventArgs e)
        {
            ГлавнаяСтудент form7 = new ГлавнаяСтудент();
            form7.Show();
            this.Hide();
        }

        private void Авторизация_Load(object sender, EventArgs e)
        {
            parol.Enabled = false;
            textBox4.Enabled = false;
            woiti.Enabled = false;
        }

        private void login_TextChanged(object sender, EventArgs e)
        {

        }

        private void login_KeyDown(object sender, KeyEventArgs e)
        {
            if (e.KeyCode == Keys.Enter)
            {
                SqlConnection connection = new SqlConnection(@"Data Source=QWE-200123;Initial Catalog=Филиал;Integrated Security=True");
                SqlDataAdapter adapter = new SqlDataAdapter("Select * FROM Преподаватели where Код ='" + login.Text + "'", connection);
                DataTable dt = new DataTable();
                adapter.Fill(dt);
                if (dt.Rows.Count == 1)
                {

                    parol.Enabled = true;
                    textBox4.Enabled = true;
                    woiti.Enabled = true;
                    parol.Focus();
                }
                else
                    MessageBox.Show("Логин отсутствует в БД");
            }
        }

        private void parol_KeyDown(object sender, KeyEventArgs e)
        {
            if (e.KeyCode == Keys.Enter)
            {
                SqlConnection connection = new SqlConnection(@"Data Source=QWE-200123;Initial Catalog=Филиал;Integrated Security=True");
                SqlDataAdapter adapter = new SqlDataAdapter("Select * FROM Преподаватели where Пароль ='" + parol.Text + "'", connection);
                DataTable dt = new DataTable();
                adapter.Fill(dt);
                if (dt.Rows.Count == 1)
                {
                    Random rnd = new Random();
                    Text = String.Empty;
                    string ALF = "1234";
                    for (int i = 0; i < 4; ++i)
                        Text += ALF[rnd.Next(ALF.Length)];
                    MessageBox.Show(Text);


                }
                else
                    MessageBox.Show("Пароль введен неверно");
            }
        }

        private void pictureBox1_Click(object sender, EventArgs e)
        {
            Random rnd = new Random();
            Text = String.Empty;
            string ALF = "5678";
            for (int i = 0; i < 4; ++i)
                Text += ALF[rnd.Next(ALF.Length)];
            MessageBox.Show(Text);
        }
    }
}
