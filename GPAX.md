namespace WinFormASS
{
    public partial class Form1 : Form
    {
        private List<double> gpaxList = new List<double>();
        private GPACalculator calculator = new GPACalculator();
        public Form1()
        {
            InitializeComponent();
        }

        private void label1_Click(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {
            try
            {
                double gpax = double.Parse(textBox1.Text);
                gpaxList.Add(gpax);
                calculator.AddGPAX(gpax);

                UpdateDisplay();
                textBox1.Clear();
            }
            catch (FormatException)
            {
                MessageBox.Show("please enter a valid GPAX ", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
            catch (OverflowException)
            {
                MessageBox.Show("GPAX must be between 0 and 4.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void UpdateDisplay()
        {
            textBox1.Text = calculator.CalculateAverageGPAX().ToString("0.00");
            textBox3.Text = calculator.GetCount().ToString();
            textBox4.Text = calculator.GetMaxGPAX().ToString("0.00");
            textBox5.Text = calculator.GetMinGPAX().ToString("0.00");
            textBox2.Text = calculator.CalculateAverageGPAX().ToString();
        }
    }
}

        
    

