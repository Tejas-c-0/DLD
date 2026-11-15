# 8:3 Encoder

The manual includes an encoder without priority and an encoder with priority.

## 1. 8:3 encoder without priority — Verilog design code
```verilog
module encwtoutprio(a, en, y);
input [7:0] a;
input en;
output reg [2:0] y;

always @(a or en)
begin
  if(!en)
    y=3'bzzz;
  else
    case(a)
      8'b00000001: y=3'b000;
      8'b00000010: y=3'b001;
      8'b00000100: y=3'b010;
      8'b00001000: y=3'b011;
      8'b00010000: y=3'b100;
      8'b00100000: y=3'b101;
      8'b01000000: y=3'b110;
      8'b10000000: y=3'b111;
    endcase
end
endmodule
```

## 2. 8:3 encoder without priority — Verilog testbench code
```verilog
module enc_tb();
reg [7:0] a;
reg en;
wire [2:0] y;

encwtoutprio u1(a, en, y);

initial
begin
  #0  en=1'b0; a=8'b00000001;
  #30 a=8'b00000010;
  #30 a=8'b00000100;
  #30 a=8'b00001000;
  #30 a=8'b00010000;
  #30 a=8'b00100000;
  #30 a=8'b01000000;
  #30 a=8'b10000000;
  #30 en=1'b1; a=8'b00000001;
  #30 a=8'b00000010;
  #30 a=8'b00000100;
  #30 a=8'b00001000;
  #30 a=8'b00010000;
  #30 a=8'b00100000;
  #30 a=8'b01000000;
  #30 a=8'b10000000;
end

initial
  $monitor($time, "a=%b, en=%b, y=%b", a, en, y);

initial
  #1000 $finish;
endmodule
```

## 3. 8:3 priority encoder — Verilog design code
```verilog
module encwtprio(a, en, y);
input [7:0] a;
input en;
output reg [2:0] y;

always @(a, en)
begin
  if(en==1)
    y=3'bzzz;
  else
    casex(a)
      8'b00000001: y=3'b000;
      8'b0000001x: y=3'b001;
      8'b000001xx: y=3'b010;
      8'b00001xxx: y=3'b011;
      8'b0001xxxx: y=3'b100;
      8'b001xxxxx: y=3'b101;
      8'b01xxxxxx: y=3'b110;
      8'b1xxxxxxx: y=3'b111;
    endcase
end
endmodule
```

## 4. 8:3 priority encoder — Verilog testbench code
```verilog
module prienc_tb();
reg [7:0] a;
reg en;
wire [2:0] y;

encwtprio u1(a, en, y);

initial
begin
  #0  en=1'b0; a=8'b00000001;
  #30 a=8'b10000010;
  #30 a=8'b00000101;
  #30 a=8'b00001011;
  #30 a=8'b0001xxxx;
  #30 a=8'b00101000;
  #30 a=8'b01001000;
  #30 a=8'b10001011;
  #30 en=1'b1; a=8'b00000001;
  #30 a=8'b00000010;
  #30 a=8'b00000101;
  #30 a=8'b00001011;
  #30 a=8'b0001xxxx;
  #30 a=8'b0010xxxx;
  #30 a=8'b01001000;
  #30 a=8'b10001011;
end

initial
  $monitor($time, "a=%b, en=%b, y=%b", a, en, y);

initial
  #1000 $finish;
endmodule
```

**Manual note:** The priority encoder's enable polarity and testbench values are reproduced from the manual. Check the manual's intended enable convention with your instructor before FPGA implementation.
