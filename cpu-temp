using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using OpenHardwareMonitor.Hardware;


namespace tempature_checker
{
    public partial class Form1 : Form
    {
        Computer computer1;
        public Form1()
        {
            InitializeComponent();
            computer1 = new Computer() { CPUEnabled=true };
            computer1.Open();
        }

        private void timer1_Tick(object sender, EventArgs e)
        {    
            String temp = "";

            foreach (var hardwareItem in computer1.Hardware)
            {
                if (hardwareItem.HardwareType == HardwareType.CPU)
                {
                    hardwareItem.Update();
                    foreach (IHardware subHardware in hardwareItem.SubHardware)
                        subHardware.Update();

                    foreach (var sensor in hardwareItem.Sensors)
                    {
                        if (sensor.SensorType == SensorType.Temperature)
                        {

			temp += String.Format("{0} Temperature = {1}\r\n", sensor.Name,
			sensor.Value.HasValue ? sensor.Value.Value.ToString() : "no value");

                        }
                    }
                }
            }
            label1.Text = temp;
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            timer1.Start();
        }
    }
}
