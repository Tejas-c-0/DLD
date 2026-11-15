# 2:4 Decoder

## 1. Verilog design code
```verilog
module dec2to4(din, dout);
input [1:0] din;
output reg [3:0] dout;

always @ (din)
case (din)
  2'b00: dout = 4'b0001;
  2'b01: dout = 4'b0010;
  2'b10: dout = 4'b0100;
  2'b11: dout = 4'b1000;
  default: dout = 4'bxxxx;
endcase
endmodule
```

## 2. Verilog testbench code
```verilog
module dec2to4_tb();
reg [1:0] din;
wire [3:0] dout;

dec2to4 g1(din, dout);

initial
begin
  #0  din=0;
  #10 din=0;
  #10 din=1;
  #10 din=2;
  #10 din=3;
end

initial
  $monitor($time, "din=%b, dout=%b", din, dout);

initial
  #100 $finish;
endmodule
```
