# 3:8 Decoder

## 1. Verilog design code
```verilog
module decoder3to8(Data_in, Data_out);
input [2:0] Data_in;
output reg [7:0] Data_out;

always @(Data_in)
case (Data_in)
  3'b000: Data_out = 8'b00000001;
  3'b001: Data_out = 8'b00000010;
  3'b010: Data_out = 8'b00000100;
  3'b011: Data_out = 8'b00001000;
  3'b100: Data_out = 8'b00010000;
  3'b101: Data_out = 8'b00100000;
  3'b110: Data_out = 8'b01000000;
  3'b111: Data_out = 8'b10000000;
  default: Data_out = 8'b00000000;
endcase
endmodule
```

## 2. Verilog testbench code
```verilog
module tb_decoder();
reg [2:0] Data_in;
wire [7:0] Data_out;

decoder3to8 g1(Data_in, Data_out);

initial
begin
  #0  Data_in=3'b000;
  #10 Data_in=3'b001;
  #10 Data_in=3'b010;
  #10 Data_in=3'b011;
  #10 Data_in=3'b100;
  #10 Data_in=3'b101;
  #10 Data_in=3'b110;
  #10 Data_in=3'b111;
end

initial
  $monitor($time, "Data_in=%b, Data_out=%b", Data_in, Data_out);

initial
  #100 $finish;
endmodule
```
