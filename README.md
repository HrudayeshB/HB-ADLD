# Advanced Digital Logic Design (ADLD)
This is my repo that stores all my assignments and some projects related to Digital logic design, These are verilog codes to be tested in the VCS - Synopsys software available in college PCs, I have written and tested in Icarus verilog and GTKwave.

## Important Compilation Flags for VCS and Icarus Verilog

## VCS (Synopsys) Flags

1. **`-v`**  
   Enable verbose output. Displays detailed information during compilation.

2. **`-Mupdate`**  
   Incremental compilation: updates only modified files without recompiling the entire project.

3. **`-Rpp`**  
   Enable the Post Processing step (used for performance improvements during simulation).

4. **`-full64`**  
   Enables 64-bit mode for VCS, which is required for compiling larger designs on 64-bit systems.

5. **`-debug_acc+all`**  
   Enables full debugging capabilities for the simulation, which is useful for viewing signal activity and debugging your design. This flag also provides better visibility into hierarchy and variable names during debugging.

6. **`-l <log_file>`**  
   Specifies a file to log the compilation output.

7. **`-timescale=<timeunit>/<timeprecision>`**  
   Set the time scale for the simulation. Example: `-timescale=1ns/1ps`.

8. **`-o <output_file>`**  
   Specify the name of the output file for the compiled simulation.

9. **`-P <config_file>`**  
   Include a configuration file to define settings for the simulation environment.

10. **`+incdir+<path>`**  
    Adds a directory to the list of places to search for `include` files.

11. **`-f <file_list>`**  
    Compile multiple files listed in a text file. This is useful for large projects where many files are involved.

12. **`+define+<macro>`**  
    Define a macro for the Verilog source code during compilation.


## Icarus Verilog (iverilog) Flags

1. **`-g2005-sv`**  
   Enable SystemVerilog features based on the IEEE 2005 standard.

2. **`-o <output_file>`**  
   Specify the name of the compiled simulation output file.

3. **`-Wall`**  
   Enable all warnings. It's useful for catching potential issues in the code.

4. **`-s <module_name>`**  
   Specify the top-level module for simulation. This is helpful when your design has multiple modules, and you need to specify which one is the top module.

5. **`-y <directory>`**  
   Add a directory where Verilog files are located, especially if you're using design libraries.

6. **`-I <directory>`**  
   Add a directory for searching `include` files (similar to VCS's `+incdir+`).

7. **`-D <macro>`**  
   Define a macro during compilation, similar to C/C++ preprocessors.

8. **`-pfileline=1`**  
   Preprocess the Verilog source to include file and line number annotations.

9. **`-t <timescale>`**  
   Set the default timescale for modules (example: `-t 1ns/1ps`).

10. **`-c <file_list>`**  
    Specify a file that contains a list of Verilog source files to compile.

## General Tips for Compilation

- **Optimization and Debugging**: Always use debugging flags like `-debug_acc+all` (VCS) or `-Wall` (Icarus) to catch potential issues early in the development process.
- **Incremental Compilation**: Use incremental compilation flags like `-Mupdate` (VCS) to save time on recompiling unmodified files.
- **Timescale**: Define timescale appropriately using `-timescale` (VCS) or `-t` (Icarus), especially when dealing with high-precision timing in simulations.

These flags cover the most useful and common options for both VCS and Icarus Verilog to help you compile, simulate, and debug Verilog designs efficiently.


# Makefiles

## Using the Makefile for Compilation

This project includes a Makefile (for VCS) that allows you to compile any number of Verilog design files along with a specified testbench file. The testbench must always be the last argument in the command.

### Instructions

1. **Download the Makefile**:
   Download the `Makefile` provided in this repository.

2. **Place the Makefile**:
   Save the `Makefile` in the same directory where your Verilog design files and testbench are located. This allows the Makefile to access the source files during compilation.


### Compilation for VCS (Synopsys) only.

1. **Compile Design Files and Testbench**:
   To compile your design files and the testbench, run the following command in the terminal:

   ```bash
   make design1.v design2.v testbench.v
   ```

## Using the Makefile with Design and Testbench Folders

This is Makefile_2.0, it is set up to compile all Verilog files in the `design` and `testbench` folders. The following steps outline how to use it.

### Instructions:

1. **Prepare Directories**:
   - Place all your Verilog design files (`*.v`) in the `design` folder.
   - Place your testbench file(s) (`*.v`) in the `testbench` folder.
   - Also rename the `Makefile_2.0` to `Makefile` and place it in the same directory.

2. **Run Compilation**:
   - Open a terminal in the directory containing the `Makefile`.
   - Run the following command to compile all files:
 
     ```bash
     make
     ```

3. **Clean Up**:
   - To remove all generated files, run:
  
     ```bash
     make clean
     ```

This setup automatically compiles all the design files in the `design` folder and the testbench files in the `testbench` folder.

## Makefile for Icarus Verilog and VCS

Makefile for Icarus for easy compilation and simulation, follow the steps:

1. Prepare `design` and `testbench` folders in the project folder same as for the VCS Makefile_2.0 and same for Icarus Verilog.

2. Download and rename `icarus_Makefile` (for Icarus) and `Makefile_3.0` (for VCS) to `Makefile` and place it in project directory

3. To compile the design and run the simulation:

     ```bash
     make run
     ```
     
    This will also create the `waveform.vcd` in the new `output` folder along with other output files

4. To View the waveform:

     ```bash
     make wave
     ```
     
    This opens GTKWave (for Icarus), DVE (for VCS) and shows waveforms

5. To clean any generated files (`output`):

     ```bash
     make clean
     ```
## Alias single Makefile

To use a single `Makefile` across all project directories, instead of including a copy in each project folder, we can create an alias to the location of original `Makefile`:

Add this line to your `.bashrc` or `.zshrc`, and change the path to Makefile accordingly and source the file or restart terminal: 

```bash
     alias icv='make -f path/to/Makefile'
```

Now you can use as follows (provided you have created `design` and `testbench` folders in yout project directory):

To compile:
```bash
     icv run
```

To show Waveforms:
```bash
     icv wave
```

To clear Output generated files:
```bash
     icv clean
```



# Verilog Simulation with Icarus Verilog and GTKWave

This guide explains how to install Icarus Verilog and GTKWave on Ubuntu, simulate Verilog designs, and view the resulting waveforms.

## 1. Installing Icarus Verilog

Icarus Verilog (`iverilog`) is a free, open-source Verilog simulation and synthesis tool.

### Steps to Install:

1. Update package lists:
    ```bash
    sudo apt update
    ```

3. Install Icarus Verilog:
    ```bash
    sudo apt install iverilog
    ```

4. Verify the installation:
    ```bash
    iverilog -v
    ```

## 2. Installing GTKWave

GTKWave is a waveform viewer used to visualize signal activity during simulations.

### Steps to Install:

1. Install GTKWave:
    ```bash
    sudo apt install gtkwave
    ```

2. Verify the installation:
    ```bash
    gtkwave --version
    ```

## 3. Running a Verilog Simulation

### Example Verilog Design and Testbench

1. **Create a Verilog file (`mux.v`)**:
    ```verilog
    module mux(
        input a, b, sel,
        output y
    );

	assign y = sel ? b : a;
   
    endmodule
    ```

2. **Create a testbench (`tb_name.v`)**:
    ```verilog
    module tb_name;
    reg a, b, sel;
    wire y;

	mux uut (a, b, sel, y);
    
    initial begin
        // Open a dump file for waveform output
        $dumpfile("waveform.vcd");
        $dumpvars(0, tb_name);
        
        // Initialize inputs
        a = 1; b = 0; sel = 0;
        #10 sel = 1;
        #10 sel = 0;

        // Run simulation for some time
        #10 $finish;
    end
    
    endmodule
    ```

### Compile and Simulate the Design

1. Compile the Verilog code and testbench:
    ```bash
    iverilog -o example_tb.vvp mux.v tb_name.v
    ```

2. Run the simulation:
    ```bash
    vvp tb_name.vvp
    ```

3. The simulation will generate a waveform file named `waveform.vcd`.

## 4. Viewing the Waveform with GTKWave

1. Open the waveform file in GTKWave:
    ```bash
    gtkwave waveform.vcd
    ```

2. In GTKWave, add the signals you want to view and analyze the waveform.

### Example Workflow Summary:

1. Write Verilog code and testbench (`mux.v` and `tb_name.v`) for design and testbench files.
2. Compile with Icarus Verilog using `iverilog` to generate the simulation file (`.vvp`).
3. Run the simulation with `vvp`, which generates the waveform file (`waveform.vcd`).
4. Open the waveform file using GTKWave to analyze the signals.

---

### To change Font family and size of waves and signals in GTKWave

1. Create a (`.gtkwaverc`) file in home directory and edit the file use any editor (here: (`nano`)).
	```bash
    nano ~/.gtkwaverc
    ```

2. Edit the file as per requirement, save and exit:
	```bash
    [wave]
    fontname_waves = Monospace 12

    [signal]
    fontname_signals = Monospace 12
    ```

3. Restart GTKWave or reload the (`.gtkwaverc`) file by running:
	```bash
    gtkwave --rcfile ~/.gtkwaverc
    ```

This will apply the changes to the wave and signal section

## Additional Information

- **Icarus Verilog Documentation**: [https://iverilog.fandom.com/wiki/Main_Page](https://iverilog.fandom.com/wiki/Main_Page)
- **GTKWave Documentation**: [http://gtkwave.sourceforge.net/](http://gtkwave.sourceforge.net/)

This guide helps you get started with simulating Verilog designs using Icarus Verilog and viewing the results with GTKWave.
