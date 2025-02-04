namespace WinFormASS // กำหนด namespace ของโปรแกรม
{
    public partial class Form1 : Form // คลาสหลักของฟอร์ม
    {
        private List<double> gpaxList = new List<double>(); // รายการเก็บค่า GPAX
        private GPACalculator calculator = new GPACalculator(); // สร้างอ็อบเจกต์ของ GPACalculator
        
        public Form1()
        {
            InitializeComponent(); // เรียกใช้เมธอดสำหรับตั้งค่า UI
        }

        private void button1_Click(object sender, EventArgs e) // อีเวนต์ที่ทำงานเมื่อกดปุ่ม
        {
            try
            {
                double gpax = double.Parse(textBox1.Text); // แปลงค่าจากกล่องข้อความเป็น double
                gpaxList.Add(gpax); // เพิ่มค่า GPAX ลงในรายการ
                calculator.AddGPAX(gpax); // เพิ่มค่า GPAX ไปยัง GPACalculator

                UpdateDisplay(); // อัปเดตค่าที่แสดงผล
                textBox1.Clear(); // ล้างข้อมูลในกล่องข้อความ
            }
            catch (FormatException) // ดักจับข้อผิดพลาดเมื่อป้อนค่าผิดรูปแบบ
            {
                MessageBox.Show("please enter a valid GPAX ", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
            catch (OverflowException) // ดักจับข้อผิดพลาดเมื่อค่าเกินขอบเขตที่กำหนด
            {
                MessageBox.Show("GPAX must be between 0 and 4.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void UpdateDisplay() // เมธอดสำหรับอัปเดตการแสดงผล
        {
            textBox1.Text = calculator.CalculateAverageGPAX().ToString("0.00"); // แสดงค่าเฉลี่ย
            textBox3.Text = calculator.GetCount().ToString(); // แสดงจำนวนข้อมูล
            textBox4.Text = calculator.GetMaxGPAX().ToString("0.00"); // แสดงค่าสูงสุด
            textBox5.Text = calculator.GetMinGPAX().ToString("0.00"); // แสดงค่าต่ำสุด
            textBox2.Text = calculator.CalculateAverageGPAX().ToString(); // แสดงค่าเฉลี่ยอีกครั้ง
        }
    }
}

using System;
using System.Collections.Generic;
using System.Linq;

namespace WinFormASS
{
    internal class GPACalculator // คลาสสำหรับคำนวณ GPAX
    {
        private List<double> gpaxList = new List<double>(); // รายการเก็บค่า GPAX

        public void AddGPAX(double gpax) // เมธอดเพิ่มค่า GPAX
        {
            gpaxList.Add(gpax);
        }

        public double CalculateAverageGPAX() // คำนวณค่าเฉลี่ย GPAX
        {
            if (gpaxList.Count == 0) return 0;
            return gpaxList.Average();
        }

        public int GetCount() // คืนค่าจำนวนข้อมูล
        {
            return gpaxList.Count;
        }

        public double GetMaxGPAX() // คืนค่ามากที่สุด
        {
            if (gpaxList.Count == 0) return 0;
            return gpaxList.Max();
        }

        public double GetMinGPAX() // คืนค่าน้อยที่สุด
        {
            if (gpaxList.Count == 0) return 0;
            return gpaxList.Min();
        }
    }
}
