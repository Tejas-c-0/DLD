# 4:2 Encoder

The manual includes both a basic encoder and a priority encoder.

## 1. Basic encoder — Verilog design code

**Manual accuracy note:** The printed basic encoder declares a 2-bit output but attempts to assign `dout[2]` and `dout[3]`, which are outside that vector. The code below is a functional 4:2 encoder implementation, not a verbatim copy of that faulty snippet.

```verilog
module enc4_2(din, dout);
input [3:0] din;
output reg [1:0] dout;

always @ (din)
begin
  case (din)
    4'b0001: dout = 2'b00;
    4'b0010: dout = 2'b01;
    4'b0100: dout = 2'b10;
    4'b1000: dout = 2'b11;
    default: dout = 2'bxx;
  endcase
end
endmodule
```

## 2. Basic encoder — Verilog testbench code
```verilog
module enc4_2_tb();
reg [3:0] din;
wire [1:0] dout;

enc4_2 g1(din, dout);

initial
begin
  din=0;
  #10 din=1;
  #10 din=2;
  #10 din=4;
  #10 din=8;
end

initial
  $monitor($time, "din=%b, dout=%b", din, dout);

initial
  #150 $finish;
endmodule
```

## 3. 4:2 priority encoder — Verilog design code
```verilog
module priority_encoderbehave(A, Y);
input [3:0] Y;
output reg [1:0] A;

always @(Y)
begin
  casex(Y)
    4'b0001: A = 2'b00;
    4'b001x: A = 2'b01;
    4'b01xx: A = 2'b10;
    4'b1xxx: A = 2'b11;
    default: $display("Error!");
  endcase
end
endmodule
```

## 4. 4:2 priority encoder — Verilog testbench code
```verilog
module PriorityEncoder_Test();
reg [3:0] Y;
wire [1:0] A;

priority_encoderbehave g1(.Y(Y), .A(A));

initial
begin
  #0  Y=0;
  #10 Y=4'b0000;
  #10 Y=4'b1000;
  #10 Y=4'b0100;
  #10 Y=4'b0010;
  #10 Y=4'b0001;
  #10 Y=4'b1010;
  #10 Y=4'b1111;
end

initial
  $monitor("time=%0t A=%b : Y=%b", $time, A, Y);

initial
  #100 $finish;
endmodule
```
