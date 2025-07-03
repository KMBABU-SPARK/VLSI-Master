# 📘 Verilog HDL – Beginner-Friendly Digital Design Language

Verilog is a **Hardware Description Language (HDL)** used to design and simulate **digital electronic circuits** like adders, multiplexers, counters, and even entire CPUs. Instead of physically connecting wires and gates, Verilog allows you to **write code to describe how a circuit behaves**.

This repository is designed to help **students and beginners** learn Verilog from scratch. It includes:

- ✅ Simple Verilog modules (AND, OR, MUX, etc.)
- 🧪 Testbenches for simulation
- 💻 Example circuits for hands-on practice
- 🛠️ Simulation outputs using tools like **Icarus Verilog** and **GTKWave**

---

Feel free to explore, modify, and use the files for your learning or digital design projects. Contributions and feedback are welcome!


### 🧾 Example-1
Q1-design a 16 bit adder and display its waveform
## 16BIT ADDER FLOW CHART

![Circuit Diagram](https://github.com/KMBABU-SPARK/VLSI-Master/blob/523ca55183cfbf5de04d33f772e4e9ba373d9639/topic1/16BITADDER.png)


```verilog
//here we have designed 16 bit adder using four 4 bit adders
module alu(x,y,z,sign,zero,carry,parity,overflow);
input [15:0]x;
input [15:0]y;
output[15:0]z;
output sign,zero,carry,parity,overflow;
wire c[3:1];

alu4bit m1(z[3:0],c[1],x[3:0],y[3:0],1'b0);
alu4bit m2(z[7:4],c[2],x[7:4],y[7:4],c[1]);
alu4bit m3(z[11:8],c[3],x[11:8],y[11:8],c[2]);
alu4bit m4(z[15:12],carry,x[15:12],y[15:12],c[3]);

assign sign=z[15];
assign zero=~|z;
assign parity=~^z;
assign overflow=(x[15]&y[15]&~z[15]|~x[15]&~y[15]&z[15]);
endmodule

// And the 4bit adder is designed using four 4 single bit full adder
module alu4bit(z,cout,x,y,cin);
input [3:0]x,y;
output[3:0]z;
output cout;
input cin;
wire c[3:1];

fulladder n0(z[0],c[1],x[0],y[0],1'b0);
fulladder n1(z[1],c[2],x[1],y[1],c[1]);
fulladder n2(z[2],c[3],x[2],y[2],c[2]);
fulladder n3(z[3],cout,x[3],y[3],c[3]);

endmodule
// Here is the code of basic unit of 16bit adder circuit
//1 bit full adder code
//GATE LEVEL DESCRIPTION 
module fulladder(sum,cout,x,y,cin);
input x,y,cin;
output sum,cout;
wire s1,c1,c2;

xor g1(s1,x,y);
xor g2(sum,s1,cin);
and g3(c1,s1,cin);
and g4(c2,x,y);
xor g5(cout,c1,c2);
endmodule

//HERE COMES THE TESTBENCH TO CHECK THE CIRCUIT

module alutest;
reg [15:0]x;
reg [15:0]y;
wire [15:0]z;
wire sign,zero,carry, parity,overflow;
alu uut(x,y,z,sign,zero,carry,parity,overflow);
initial begin
$dumpfile("alu.vcd");
$dumpvars(0,alutest);
$monitor($time,"x=%h,y=%h,z=%h,sign=%b,carry=%b,parity=%b,overflow=%b",x,y,z,sign,carry,parity,overflow);
#5 x=16'h0056;
y=16'h0001;
#5 x=16'h0100;
y=16'h0101;
#5 x=16'h000b;
y=16'h0001;
#5 x=16'h000c;
y=16'h0001;
#5 x=16'h000d;
y=16'h1111;
#5 x=16'h000e;
y=16'h1001;
#5 $finish;
end
endmodule

