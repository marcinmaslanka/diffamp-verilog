Differential Amplifier Verilog-A Model

This repository contains the Verilog-A model for a Differential Amplifier designed for use in Cadence Virtuoso. The model includes the behavior of the amplifier with non-linear saturation characteristics using a hyperbolic tangent (tanh) function for the differential voltage input.
Features:

    Differential amplifier behavior with a gain parameter.

    Offset voltage for output shifting.

    Nonlinear saturation modeling using the tanh function.

    Simulation-ready in Cadence Virtuoso.
    
  ![diffamp](https://github.com/user-attachments/assets/298f2950-7566-4e68-86e0-af28dbc2f4d9)


Table of Contents:

    Getting Started

    Verilog-A Model Description

    How to Use

    Simulation in Cadence Virtuoso

    License

Getting Started

To get started with the differential amplifier model, follow these steps:

    Clone the Repository: Clone this repository to your local machine using the following command:

    git clone https://github.com/yourusername/differential-amplifier-verilog-a.git

    Add Verilog-A Model to Cadence Virtuoso: Copy the Verilog-A code (diffamp.va) from this repository to your Cadence Virtuoso project.

    Include Verilog-A File: In your Cadence project, create a new cellview for the model and paste the Verilog-A code.

Verilog-A Model Description

The Verilog-A code models a Differential Amplifier with the following parameters:

    gain: The gain of the amplifier, which defines how much the input difference is amplified.

    vcc: The supply voltage of the amplifier. This parameter sets the upper limit of the output voltage.

    offset: An offset voltage that shifts the output, simulating a DC bias or level shift.

Verilog-A Code:

`include "constants.vams"
`include "discipline.h"

module diffamp(out, in1, in2);
    output out;        // Output node of the differential amplifier
    input  in1, in2;   // Differential input nodes

    electrical out, in1, in2;  // Declare electrical connections for the nodes

    // Parameters:
    parameter real gain = 40;   // Gain of the differential amplifier
    parameter real vcc = 3;     // Supply voltage in volts (V)
    parameter real offset = 1.5; // Offset voltage in volts (V)

    analog begin
        // Differential amplifier behavior:
        V(out) <+ offset + (vcc/2) * tanh(gain / vcc * (V(in1) - V(in2)));
        // The tanh function ensures that the output is within a reasonable range
        // and exhibits a saturating behavior as the input difference increases.
    end
endmodule

Parameters:

    gain: The amplification factor for the differential input.

    vcc: Supply voltage, which determines the maximum output swing.

    offset: A DC offset that shifts the output voltage.

Functionality:

    The differential amplifier amplifies the difference between in1 and in2.

    The output voltage is governed by a hyperbolic tangent function that models saturation when the difference between inputs becomes large.

    The amplifier behavior mimics a real-world operational amplifier with a non-linear response.

How to Use

    Open Cadence Virtuoso: Open Cadence Virtuoso and create a new library or use an existing library.

    Create a New Cell for Verilog-A:

        From the Library Manager, create a new cellview.

        Set the View Name to veriloga and the Tool to Verilog-A.

    Paste the Verilog-A Code:

        Copy the Verilog-A code from the repository and paste it into the editor.

    Save and Check the Model:

        Save the Verilog-A code and run the Check and Save process to validate the syntax.

    Instantiate the Model in a Schematic:

        Open your schematic in Cadence Virtuoso.

        Use the component you just created by instantiating it in your schematic.

        Connect the input and output nodes to simulate the differential amplifier in the circuit.

Simulation in Cadence Virtuoso

    Set Up ADE (Analog Design Environment):

        From the Cadence Virtuoso toolbar, go to Launch ADE.

        Set up the simulation parameters (e.g., transient analysis or DC analysis).

    Run the Simulation:

        Set the desired simulation type (e.g., transient, AC sweep).

        Choose the outputs to plot (e.g., output voltage).

        Click Run to simulate the circuit and observe the behavior of the differential amplifier.

    Analyze the Results:

        After the simulation, observe the voltage at the output node.

        The output should exhibit the expected behavior based on the input difference, with saturation limits determined by the gain and supply voltage.

License

This project is licensed under the MIT License - see the LICENSE file for details.
